# Data, Explained by Appa

---
title: "Data, Explained by Appa"
date: 2026-08-16
type: "posts"
tags:
	- data engineering
	- glossary
summary: "A playful primer explaining core data concepts through a conversation between Appa and Anya."
---

**Anya:** Appa, what is data?

**Appa:** Data is like rain, kutty. Every time something happens — you tap the phone, you buy something, a sensor reads the temperature — a drop of information falls. That drop is "data."

**Anya:** Just one drop? That's it?

**Appa:** One drop alone doesn't do much. But millions of drops together can fill a lake, water a whole farm, or even predict a storm. That's the power of data — not in one drop, but in all of them together.

**Anya:** Okay so where does all that "rain" go?

**Appa:** It flows down through rivers and pipes into a big reservoir. We call that a **database** — an organized place to store the water so it doesn't get lost. If the reservoir is really, really big and holds water for a whole city, we call it a **data warehouse**.

**Anya:** Is a warehouse different from a lake?

**Appa:** Good question! A **data lake** is like a big natural lake that collects water in *any* form — rain, river water, melted snow, even muddy water, all mixed together, not yet sorted. A **data warehouse** is more like a treated reservoir — the water's already been filtered and organized into clean sections, ready to drink.

**Anya:** What's "muddy" data called?

**Appa:** We call that **unstructured data** — messy, not organized into neat rows, like a photo, a voice note, or a video. **Structured data** is the opposite — like a clean table, with clear columns: name, amount, date. Much easier to work with, like water that's already filtered into bottles.

**Anya:** How does the water even get to the reservoir?

**Appa:** Through rivers and pipes — that whole moving system is called a **data pipeline**. It's the path that carries the water from where it fell all the way to where we store it, running every single day without stopping.

**Anya:** Who builds the rivers and pipes?

**Appa:** That's my job, actually — I'm a **data engineer**, or rather, I lead a team of them. We design the dams, lay the pipes, build the treatment plants — so water reaches the reservoir reliably, clean, and on time, whatever the weather.

**Anya:** Does the water need cleaning?

**Appa:** Always. Rainwater picks up dust and leaves on the way down. We clean it in one of two ways:
- **ETL** — filter the water *before* it enters the reservoir. Only clean water goes in.
- **ELT** — let all the water in first, messy or not, and filter it *later*, only when we're about to use it.

**Anya:** Which one do you use?

**Appa:** Mostly ELT these days — with tools like Snowflake, storage is cheap, so we store everything first and clean it only when needed. More flexible that way.

**Anya:** But how do you know which water is clean or dirty?

**Appa:** That's called **data quality** — checking if the water (data) is accurate, complete, and not duplicated. Bad data quality is like water with leaves and dirt still floating in it — looks fine from far away, but you don't want to drink it.

**Anya:** And what's on the bottle label — like when it says "purified, from this river, tested on this date"?

**Appa:** That's called **metadata** — data *about* the data. It doesn't tell you what's inside, it tells you where it came from, when it was collected, and how trustworthy it is. Like a label on a water bottle.

**Anya:** Who decides who's allowed to drink from the reservoir?

**Appa:** That's **data governance** — the rules about who can access which water, how it's tested, and who's responsible if something goes wrong. Very important in a bank, since some of that "water" is people's account details — very private.

**Anya:** Is there a map of where all the reservoirs and pipes are?

**Appa:** Yes! We call that a **data catalog** — like a village map showing every reservoir, pipe, and treatment plant, so people can find where a particular kind of water lives without wandering around lost.

**Anya:** What about the shape of the reservoir — like how it's divided into sections?

**Appa:** That's the **data model** or **schema** — the blueprint of how the storage is organized. Like deciding a reservoir has one section for drinking water, one for irrigation, one for industrial use, each labeled clearly.

**Anya:** Does the water flow all the time, or only sometimes?

**Appa:** Both happen. **Batch processing** is like a truck delivering water once a day, in one big load. **Real-time (or streaming) data** is different — a pipe that never stops, water flowing continuously, second by second. Banks often need real-time — the second you swipe your card, we need to know instantly if it's fraud.

**Anya:** How do different apps talk to each other and share water?

**Appa:** One way is an **API** — think of it as a tap. You turn their tap and ask for exactly the water you need, instead of digging into their reservoir yourself. But someone has to build and maintain that tap, and each time, you're asking, waiting, and carrying the water back yourself.

**Anya:** Is there a faster way to share water than the tap?

**Appa:** Yes — it's called **direct share**. Two reservoirs are simply connected by a channel. The moment new water arrives in mine, it shows up in yours too — instantly. No bottling, no trucks, no separate copy for you to keep. Snowflake — one of those big reservoirs companies use — actually offers exactly this, they call it Direct Share.

**Anya:** So nobody copies the water at all?

**Appa:** Exactly. Before, everyone kept their own tank and had to keep refilling it. With direct share, we just open a channel between reservoirs — one true copy, always fresh, no two tanks ever showing different amounts.

**Anya:** What if I don't want to just look at the water — I want to actually do something clever with it?

**Appa:** Then you build what we call **analytical capability** right on top of the reservoir — instead of moving water out at all, you set up your farm right at the water's edge. Dashboards, AI models, reports — all built to run exactly where the water already sits, instead of trucking it miles away first.

**Anya:** So the choice is: turn a tap and ask for water (API), share a channel between reservoirs (direct share), or farm right beside the reservoir (build analytics on top)?

**Appa:** Exactly right, kutty. Different jobs need different approaches — but the direction data is moving in is clear: less carrying water around, more building smart things right where it already lives.

**Anya:** And the reservoir — is it in our house or somewhere else?

**Appa:** These days, mostly somewhere else — in giant, shared reservoirs run by companies like Amazon, Google, or Microsoft. We call that the **cloud**. Instead of everyone building their own small tank, we all rent space in a massive, well-maintained reservoir far away.

**Anya:** And the forecaster you mentioned before — AI?

**Appa:** Right — **AI** is like a weather forecaster watching all this water flow. It studies patterns — rainfall, river levels, past floods — and predicts what's coming: which customers might leave the bank, which transaction looks suspicious, or it can just answer a question in plain words, like "how much water did we collect last month?" without anyone writing complicated code.

**Anya:** So you're basically... a river and reservoir engineer, but for information?

**Appa:** (laughs) Exactly, kutty. That's precisely what I do.

---

### Quick glossary — the words we used

| Word | What it means (in water terms) |
|---|---|
| Data | A single drop — one piece of information |
| Database | The reservoir where data is stored |
| Data Warehouse | A big, treated, organized reservoir |
| Data Lake | A natural lake holding raw, mixed, unfiltered water |
| Structured / Unstructured | Bottled clean water vs. muddy, mixed water |
| Data Pipeline | The rivers and pipes moving the water |
| Data Engineering | Building and maintaining the pipes, dams, treatment plants |
| ETL / ELT | Filtering before storing vs. filtering after storing |
| Data Quality | How clean and trustworthy the water is |
| Metadata | The label on the bottle — details about the water |
| Data Governance | Rules on who can access and use the water |
| Data Catalog | The map of all reservoirs and pipes |
| Data Model / Schema | The blueprint of how the reservoir is divided |
| Batch vs Real-time | A truck delivery once a day vs. a pipe flowing nonstop |
| API | A tap that lets others request water in a controlled way |
| Data Sharing (e.g. Snowflake Direct Share) | An underground channel connecting two reservoirs — no copying, always up to date |
| Analytical Capability (built on the data) | Building the mill, farm, or forecaster right next to the reservoir instead of trucking water away |
| Cloud | A giant shared reservoir run by someone else, rented by many |
| AI | The forecaster predicting floods, droughts, and patterns |
