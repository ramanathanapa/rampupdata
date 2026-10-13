---
title: "From Vibe Checks to Verified AI: Product Thinking, Evals, Skills and AI-Ready Data in One Snowflake Story"
date: 2026-10-13
type: "posts"
tags: ["ai", "data engineering", "snowflake"]
summary: "A practical guide to combining product thinking, evals, AI-ready data, and team skills to ship trustworthy AI on Snowflake."
draft: false
---

*A 5-minute read.*

## The demo always works. Production doesn't.

Most AI projects don't fail because the model is weak. They fail because nobody defined "good", nobody measured it, and the data gave the AI no clues.

The fix is a handful of ideas that sound like jargon but are really common sense. Here they are in 60 seconds, then one Snowflake story that ties them together.

## The jargon in 60 seconds

| Term | What it means | Think of it as |
| --- | --- | --- |
| Product-first thinking | Start from the user and the decision they need to make, not the tool | A tailor measuring you before cutting cloth |
| PRD (Product Requirements Document) | One page on who it's for, why, scope, definitions and rules | The architect's drawing before the build |
| TDD (test-driven development) | Write the test first, then the code that passes it | Writing the answer key before teaching the chapter |
| Evals | Realistic questions with known good answers, used to score an AI | Grading an essay exam |
| Skills | Packaged instructions and examples that teach an AI your way of working | The runbook you hand a new joiner |
| AI-ready metadata | Labels on data: meaning, owner, freshness, sensitivity | Labels on pantry jars |
| Semantic layer | A dictionary from business words to tables and formulas | A translator between business and SQL |

The one difference worth remembering: TDD suits predictable code, where 2 + 2 is always 4. AI answers vary from run to run, so evals give a score, like 46 out of 50, instead of pass or fail.

**Evals aren't new, by the way.** Machine learning has used them for decades: hold back a test set the model never saw in training, then measure accuracy, precision and recall before shipping. Public benchmarks such as ImageNet did the same for whole research fields. What changed with LLMs is that answers are open-ended text, so teams now score them with rubrics, LLM-as-judge and human review. And the people writing evals are now product and data teams, not only ML researchers.

## How they connect

It's one loop, with evals as the referee in the middle.

![The AI product loop: product-first thinking and the PRD feed evals; a low score sends you to improve metadata and skills, a cleared bar ships, and real questions feed back](/images/ai-product-loop.png)

- **PRD feeds evals.** The PRD says what "correct" means; the eval set is 50 concrete examples of it.
- **Score too low? Pull one of two levers.** Metadata fixes *what the data means*. Skills fix *how your team does the job*.
- **TDD and evals are partners.** TDD tests the predictable code; evals test the AI's answers.

## "Aren't evals the new PRD?"

Half true. Old PRDs described behaviour in vague sentences like "answers should be accurate and helpful", which nobody can test. A set of golden questions is a much sharper spec, and it becomes the real definition of done.

But evals can't tell you who the user is, which questions are in scope, that "net flows exclude switches", or that 90% is good enough. People have to make and own those decisions *before* anyone can write a golden answer.

**The modern answer:** a one-page PRD for why, who, scope and rules, with the eval set attached as its executable acceptance criteria. Skip the PRD and you precisely measure the wrong questions. Skip the evals and you get a nice document and an untestable product.

## The story: Snowy and the €40 million question

*Fictional team, real Snowflake features.*

Team Fundstream runs an asset manager's Snowflake platform: **Priya** builds pipelines, **Arjun** owns dashboards, **Meera** is the product owner. Their new AI assistant, **Snowy**, answers questions in plain English using Snowflake Cortex.

**Monday: the dazzling demo.** Priya asks for last month's net inflows. Snowy writes the SQL and returns a number with a chart. Applause. "Roll it out next week."

**Three weeks later: the €40 million gap.** Snowy says equity inflows were €212 million. The official report says €172 million. Snowy had summed `TXN_AMT`, which includes switches between funds and two test funds. It wasn't stupid, just uninformed.

**Product first, then a PRD.** Meera talks to three fund managers. About 40 kinds of question cover their needs: daily flows, assets under management by fund, top redeeming distributors. Her one-page PRD sets the definitions (net flows exclude switches), the must-nevers (no investor names or tax IDs, no stale data without a warning) and a launch bar of 90% correct.

**The exam before the class.** Priya, a TDD fan, turns the PRD into 50 real questions with golden answers from the official report, stored in a Snowflake table. Five are traps Snowy must refuse. A small script scores every run. Baseline: **21 out of 50**.

**Labelling the pantry.** The team adds column descriptions from the Collibra glossary, defines "net flows" once in a semantic view for Cortex Analyst, tags name and tax ID columns as PII with a masking policy, and tracks freshness with Data Metric Functions. Same model, same prompt: **38 out of 50**.

**Teaching the house rules.** The remaining misses are habits: the fiscal year starts in April, "last month" means the last closed month, always state the as-of date. Arjun writes a skill with the rules, three examples and a pre-answer checklist. **46 out of 50**, every trap refused. Launch.

**The night the load failed.** The pipeline breaks at 2 a.m. At 9, Snowy checks freshness, says yesterday's data isn't loaded yet, and gives the last complete figure instead. Later, a model upgrade scores 44 in the eval suite; one skill tweak lifts it to 47 before it ships. Nobody vibe-checked anything.

The model never decided the outcome. The loop did.

## Start on Monday

1. **Pick one narrow job** for one group of users.
2. **Write a one-page PRD:** who, why, scope, definitions, must-nevers, launch bar.
3. **Turn it into 30 to 50 golden questions,** including a few the AI must refuse.
4. **Score a baseline,** then add metadata (meaning, PII tags, freshness), then skills. Rerun after each step.
5. **Gate every change** to model, prompt or schema on the eval score.

TDD writes the test before the code. Evals write the exam before the prompt. The PRD decides which exam is worth setting, and metadata and skills help the AI pass it.

## The whole idea on one page

Each pillar answers one question; take any one away and trust falls.

![Four pillars and one foundation: Product + PRD, Evals, AI-ready data and Skills hold up trustworthy AI answers, standing on TDD](/images/four-pillars.png)
