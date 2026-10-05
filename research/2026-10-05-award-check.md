# Award data check — 2026-10-05

Checked the riskiest assumption in `plan.md`: is there enough CanadaBuys award data to reach ~20 prospects/week, and can we tell which awards are CPCSC-relevant?

**Source:** https://canadabuys.canada.ca/opendata/pub/2026-2027-awardNotice-avisAttribution.csv (current fiscal year, refreshed daily; 4,314 awards from 2026-04-01 to 2026-10-05).

## Numbers (last 60 days, new awards only, Canadian suppliers, DND / defence as buyer or end user)
- 643 defence awards
- 382 of these are **$1 placeholder entries for the Defence Drone Initiative (DDI) marketplace**, not real contracts (published 2026-08-29 to 2026-09-11)
- 261 real contracts. 155 look like engineering-type work; the rest are groceries, cleaning, grass cutting, tailoring, etc.
- 121 unique suppliers behind those 155 (~14/week)
- In a hand-checked sample of 30, only about 1 in 3 looked like a real Rendatum fit (engineering / manufacturing / R&D firms). The rest were parts resellers, truck dealers and similar
- **Estimate: ~4–5 good-fit companies/week before the size check and Clay lookup, so ~2–4/week reach a draft. Well short of 20.**

## CPCSC relevance
- Award notices do **not** say whether CPCSC applies. Only 27 of 261 mention security at all, mostly boilerplate ("There are no security requirements…" or "There are security requirements, see Part 1").
- So relevance has to be judged from the **type of work** (title, category, description), not from a security field.

## Other data quirks
- Many awards show a **$0 contract value** (standing offers and supply arrangements), so emails can't rely on quoting the value.
- The supplier country is written inconsistently ("CA", "Canada", "canada") and the same company appears under several spellings (e.g. "GCPROC Ltd", "GC PROC LTD."), so names need cleaning before the "already contacted" check.
- The award file has **no company size**. Size has to come from Clay.

## Bigger opportunity found
- **385 Canadian companies were accepted into DND's Defence Drone Initiative marketplace** (Aug 29 to Sep 11, 2026). These are drone and defence-tech firms that will handle defence Specified Information, which makes them a strong ICP fit with a timely, specific hook.
- Over the last 6 months, 820 unique Canadian companies won defence awards. That's a one-time backlog, separate from the weekly flow.

## Recommended change to the plan
Mix two sources each week: (1) new engineering-type awards (~3–5/week) and (2) a one-time backlog (the DDI marketplace companies plus fitting award winners from the last 6 months), used to top the list up to 20. At roughly 15/week from the backlog, it lasts several months.
