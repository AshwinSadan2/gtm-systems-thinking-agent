# Decisions

## 2026-10-01: Install `jq` so the status line script can run as written
- Why: the script relies on `jq` to read session info. Installing it with Homebrew is one command and keeps the script identical to the course version.
- What we didn't pick: rewriting the script to use Python instead. That would drift from the shared course version and be harder to update.

## 2026-10-01: Turn the status line on for every project (user-level settings)
- Why: seeing how much of Claude's memory is in use matters in every project, not just this one.
- What we didn't pick: project-only settings, which would have to be set up again in each folder.

## 2026-10-01: Keep general rules in a user-level `~/.claude/CLAUDE.md`
- Why: lessons like "Notion links need a browser download" apply to every project.
- What we didn't pick: putting them in this project's CLAUDE.md. That file is the interview framework and is already over 200 lines.

## 2026-10-05: Trigger outreach from public federal contract awards (CanadaBuys open data)
- Why: a fresh defence award is a concrete "why now" reason to reach out, and the data is free, public and refreshed daily.
- What we didn't pick: ICP fit alone with no trigger (weaker reason to email), and a paid tender-tracking service (not needed for v1).

## 2026-10-05: Contact direct award winners first; subcontractor discovery is Phase 2 (option C)
- Why: award notices name the contract holder, not the subcontractors, so v1 sticks to reliable public data.
- What we didn't pick: (A) only ever contacting winners, which misses much of the core subcontractor ICP long-term; (B) guessing primes' subcontractors from day one, which is too much guesswork for v1.

## 2026-10-05: Awards from the last 60 days, no open tenders in v1, don't pad below 20
- Why: keeps emails timely while giving a big enough pool; quality over hitting the number.
- What we didn't pick: a 2-week window (too few prospects some weeks), a 1-year window (weak timing), and open tenders (bidders aren't public, so it would be guesswork).

## 2026-10-05: Review in Slack, one-click save to Ashwin's Gmail drafts, never auto-send
- Why: cold emails can't be unsent, and the audience is small and security-minded, so a human checks every one.
- What we didn't pick: drafts straight to Gmail with no review step, and automatic sending.

## 2026-10-05: General-inbox fallback only for companies under 50 people
- Why: at small firms a general inbox usually reaches someone senior; at bigger firms it gets lost.
- What we didn't pick: skipping every company with no named contact, or using the general inbox for all sizes.

## 2026-10-05: Success = 2–4 replies/week, tracked manually in a tracking sheet for v1
- Why: replies are the result that matters. Manual marking takes 2 minutes a week and avoids building Gmail reply detection up front.
- What we didn't pick: measuring draft quality or time saved as the main signal; automatic reply detection (Phase 2).
