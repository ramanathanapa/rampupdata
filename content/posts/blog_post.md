---
title: "Feedback, Structured - A Vibe-Coded Fix for a Mess"
date: 2026-08-30
type: "posts"
tags:
  - productivity
  - software
  - workflow
summary: "A personal note on fixing a small but repeated hiring feedback problem with a lightweight internal tool."
---

# Feedback, Structured - A Vibe-Coded Fix for a Mess

Every hiring loop I've been part of has the same quiet friction point: feedback lives
everywhere except one place. One interviewer's notes are in an email. The coding challenge
result is a PDF sitting in a different tool. The recruiter's third-party assessment is a
separate attachment. By the time it reaches the next-round interviewer, they're stitching
together four sources before they've even met the candidate.

None of that is a hard problem. It's not a data science problem, or a platform problem, or
a "let's evaluate three SaaS vendors" problem. It's a small, specific, annoying gap — the
kind that's easy to live with because working around it only costs a few minutes each time.
Except those minutes add up, and they add up for everyone in the loop, not just you.

So instead of living with it, I spent a bit of time building a small internal tool to close
the gap:

- Every candidate gets their own configurable set of interview levels — Screening, Technical
  L1, Technical L2, Managerial, whatever the role actually needs.
- Feedback gets logged against the right level, by the right interviewer, with a rating and a
  recommendation — not buried in a chat thread.
- Any supporting PDF — candidate profile, coding challenge export, third-party feedback — gets
  attached directly to the candidate record.
- One button compiles everything — our feedback plus every attachment — into a single
  bookmarked PDF, so the next interviewer opens one file and can jump straight to the section
  they need.

That's it. No server, no login, no subscription. Python for the interface, a local database
file for storage, a couple of small libraries for PDF handling. It runs entirely on one
machine, and it took less time to build than it would have taken to evaluate a "real" tool
for the same job.

The point isn't the interview-feedback problem specifically — yours is probably something
else. A shared spreadsheet six people quietly maintain their own copy of. A report someone
assembles by hand every Friday. A handoff between two systems that don't talk to each other,
so a person plays translator. These are everywhere, and they're almost always small enough
to fix directly, without waiting for budget, a vendor evaluation, or a bigger initiative to
get around to it.

The barrier usually isn't difficulty — it's that the problem feels too small to justify
"real" software, so it just... persists. But small, boring problems are exactly the ones a
simple, purpose-built app handles well. It doesn't need to be elegant or general-purpose.
It just needs to close the specific gap you actually have.

If there's a version of this friction in your own day-to-day — feedback in fifty places, a
copy-paste ritual, a handoff that always drops something — it's probably closer to a weekend
project than you think.

