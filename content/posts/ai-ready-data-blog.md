---
title: "AI-ready data: the metadata is the model"
date: 2026-10-18
type: "posts"
tags: ["ai", "data engineering", "snowflake"]
summary: "A practical definition of AI-ready data, tested in a Snowflake portfolio-analysis app built on free SEC filings."
draft: false
---

*A tested definition from a portfolio-analysis app I built on Snowflake Cortex Analyst, using free SEC data and a free trial account.*

A portfolio manager types "How much do IVV and VOO overlap?" A few seconds later the app answers: 96.8%, with 476 securities in common. It also shows the SQL it ran and the date the holdings are from.

IVV is BlackRock's iShares Core S&P 500 ETF and VOO is the Vanguard S&P 500 ETF. Both track the S&P 500, so a PM expects them to be nearly identical, which makes this a good sanity check. The gap from 100% is likely because the two funds report on different dates and hold slightly different extras, such as cash and futures.

Getting a language model to write that SQL was the easy part; text-to-SQL is close to a commodity now. What took the time was everything the model can't see: what each column means, which units it uses, and which of several conflicting records to trust. To me, that is what "AI-ready data" comes down to.

The phrase is everywhere at the moment, and it rarely comes with a definition. Vendors put it on product pages and AI projects are said to stall without it, but few people spell out what it takes. What follows is my definition, tested on one real build, with the code and the numbers so you can check it.

## What is AI-ready data?

For me, AI-ready data is data an AI can query correctly without a person checking every answer. In practice that means four things:

| Property | Meaning | In this project |
| --- | --- | --- |
| Trustworthy | Clean, typed, de-duplicated and tested against known facts | Views checked against published fees and known fund overlaps |
| Shaped | Organised around the questions people ask | One analytics view per question: overlap, holdings, changes, bond duration |
| Dated | Every answer says how old its data is | As-of date and filing date on every row |
| Described | Meaning, units, synonyms and rules written where the AI can read them | A semantic model over the analytics views |

The first three are ordinary data engineering. The fourth is metadata, and it is what makes a good warehouse usable by an AI. The industry calls this a semantic layer. Snowflake has semantic views, dbt has its semantic layer, and BI tools have had one for years. What has changed is the reader: it used to feed dashboards, and now it is most of what a language model sees.

Databricks and BigQuery have their own versions too, so none of this is Snowflake-only. I used Snowflake's, which keeps the examples below concrete and runnable.

## The build in one paragraph

The SEC publishes every US fund's holdings (Form N-PORT) and prospectus fees for free, in quarterly files of about 400 MB. A small Python loader keeps 24 funds and loads them into Snowflake, where the data moves through three layers: RAW is an exact copy, CURATED is typed and joined, and ANALYTICS has one view per question. Cortex Analyst turns a question into SQL using a semantic model, and a Streamlit app inside Snowflake shows the answer. Terraform, SQL migrations and test scripts make it repeatable, and the whole thing runs on a free trial.

## Why metadata matters most

The AI never sees your data, only your metadata. Cortex Analyst reads a YAML semantic model (table names, column descriptions, synonyms, rules and example queries) and writes SQL from that alone. When the metadata is vague, the SQL comes back wrong and looks just as confident.

![The AI reads the metadata; tested views make the answer true](/images/ai-ready-data-blog_img.png)

Besides the question itself, Cortex Analyst reads only the semantic model. The numbers come from views that people built and tested.

Five kinds of metadata did most of the work here:

1. Units. Every column ending in `_pct` is already a percentage, so 0.03 means 0.03%. One line in the model keeps the AI from multiplying by 100 and reporting a 3% fee.
2. Synonyms. People say "AUM", "fund size" or "assets"; the column is `NET_ASSETS`. Synonyms map the words people use onto the names engineers picked.
3. Business rules. "Latest" means the latest filing loaded, which differs by fund. A security can appear on several lines, so weights have to be summed per security. These rules sit in the model's instructions, where the AI can read them.
4. Verified queries. Four questions are paired with known-good SQL, and the AI reuses those patterns for similar questions.
5. Freshness and lineage. Every row records its source file and load time, and every answer shows its as-of date. Holdings become public about 60 days after the portfolio date, and a portfolio manager needs to know that before acting on them.

With all five in place, the app answered 10 of 10 test questions correctly against live data.

## Metadata cannot fix wrong data

The bug that taught me the most had nothing to do with the AI. Take VWO, for example. Vanguard's emerging-markets ETF holds thousands of companies across China, India, Taiwan, Brazil and elsewhere. Once fixed, the app shows about 30% of VWO's money in its ten largest holdings, spread across more than 6,000 positions. Before the fix it said 99.7%. Cortex Analyst understood the question, the semantic model pointed it at the right view, and the SQL was exactly right: add up the weights per security and show the top 10. The answer was still wrong.

Every security has an ID. In the US the standard one is the CUSIP, a 9-character code (Apple's is `037833100`). The app uses it to recognise the same company across funds and to total a fund's weight in each company. The rule was simple: use the CUSIP, fall back to the international ID (ISIN) if it is empty, and to the company name if that is empty too.

Many foreign companies have no CUSIP, and on 30,955 holding lines the fund's SEC filing had the text `N/A` in that field. `N/A` is not empty, so the code took it as a real ID. That left 10,363 different companies sharing one ID, and the top-10 query added them up as a single huge "security".

Picture a class register where every student without a roll number is entered as "N/A". Ask for the ten biggest students and "N/A" comes first every time, because it is three hundred children counted as one.

Better metadata could not have caught this. The AI only sees the description of the data, and no synonym, unit or instruction would have told it that `N/A` was a placeholder. It would have given the same wrong answer just as confidently.

The fix was one rule in the SQL view that builds the security ID: treat placeholders (`N/A`, `000000000`, blank) as missing. Those holdings now fall back to the ISIN or the name, and each company has its own identity again. A test checks that no single "security" swallows a fund, so the bug cannot quietly come back.

So the work splits in two. Metadata tells the AI where to look, and well-built views make sure what it finds there is true. I keep the hard logic (identifiers, de-duplication, formulas) in tested SQL views and leave the AI the easy part: picking the right view and filtering it.

## What I would do again

- Shape data around questions. One clear view per question is easier for the AI than one wide table it has to join.
- Write metadata the way you would brief a new analyst, with units, synonyms, rules and examples.
- Treat verified queries as test cases. They teach the AI and catch regressions.
- Show how old the data is in every answer. Public filings are always weeks behind.
- Check answers against facts you already know. SQL that runs can still be wrong.

## Try it yourself

The full project is open source: Terraform, SQL migrations, loaders, the semantic model, the Streamlit app and tests.

- GitHub repo: [github.com/ramanathanapa/snowflake-ai-ready-data](https://github.com/ramanathanapa/snowflake-ai-ready-data)
- Knowledge base, covering the problem, data sources, design, 13 architecture decisions, lineage and app flow: [docs/KNOWLEDGE_BASE.md](https://github.com/ramanathanapa/snowflake-ai-ready-data/blob/main/docs/KNOWLEDGE_BASE.md)

**I started out thinking I was building an AI app. I ended up writing a very careful description of fund data, and that description is what made the AI worth trusting.**

*Analysis of public regulatory filings, not investment advice.*
