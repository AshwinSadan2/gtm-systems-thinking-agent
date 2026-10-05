# Rendatum Award-Triggered Outbound

> This spec is designed to be used as context for a new Claude Code session. Drop it in a project folder and begin building from here.

## Outcome
Every week, the system finds up to 20 Canadian defence suppliers (20–200 people) that have recently won a defence-related federal contract, identifies their VP of Engineering or Engineering Manager, and drafts a short, personal cold email offering a **free Rendatum pilot** on that specific contract in exchange for product feedback. Drafts are reviewed in Slack by Ashwin or the founder, and approved drafts are saved to Ashwin's Gmail with one click, ready to send manually. "Done" means a Monday-morning Slack channel full of accurate, award-specific drafts that need little or no rewriting, with nothing ever sent automatically.

## Success Signal
- **Primary:** 2–4 replies per week from the ~20 weekly prospects (a 10–20% reply rate).
- Measured through the tracking sheet: Ashwin marks replies at the end of each week.
- Secondary signal to watch: how many drafts are saved to Gmail without heavy editing, and the reasons given for skips.

## Target (ICP)
- **Person:** VP of Engineering or Engineering Manager.
- **Company:** Canadian defence suppliers with roughly 20–200 people that handle drawings, specs, DXF files and revision tables as Specified Information. Each segment gets its own email angle:
  1. **Engineering-heavy Tier 1 / Tier 2 subcontractors** heading toward CPCSC Level 2 in 2027 (core ICP). Angle: they want AI help on RFPs and specs, but control 03.01.20 makes most AI tools hard to approve.
  2. **Controlled Goods Program registrants**, often also handling ITAR data. Angle: a US-parented cloud tool is a hard sell to their security officer, so architectural sovereignty is a differentiator.
  3. **Dual-market suppliers already under CMMC / ITAR.** Angle: they already understand compliance, have budget for it, and feel the "where does the data go" question most acutely.
  4. **Engineering consultancies, design bureaus, CAD/drafting shops** in the defence chain. Angle: education. CPCSC reaches them even though they often assume it doesn't.
  5. **Bid-intensive firms with small (2–3 person) bid teams.** Angle: RFP cross-referencing pain.

## Inputs
- **Contract awards:** who won, buyer department, description, value, date, link. From the Government of Canada's public CanadaBuys award notices dataset (free, open data, refreshed every morning). Freshness: awards from the **last 60 days**; newest first.
- **Company details:** size, location, what they do. From **Clay**. Freshness: looked up at run time.
- **Contact (VP Eng / Eng Manager) and email:** from **Clay**. Fallback for companies under 50 people: the company's general inbox (info@, contact@). Freshness: looked up at run time.
- **Rendatum messaging:** the core pitch plus the angle for each of the 5 segments. Currently in the pitch deck; **to be extracted into a short written messaging doc** that the system reads from. Freshness: updated manually when positioning changes.
- **Tracking sheet ("already contacted" list):** created by this system, since none exists today. Freshness: always current; checked before every draft.
- **Do-not-contact list:** existing customers, pilots and active conversations. Maintained manually.

### When data is missing or wrong
- **No VP Eng / Eng Manager found, company under 50 people:** draft to the general inbox, tagged 📮, with slightly different wording ("Could you pass this to whoever leads engineering?").
- **No contact found, company 50+ people:** skip the company and list it in the Slack run summary under "found the company, couldn't find the person."
- **Company size or details unclear:** include it, but flag it ⚠️ "unverified size."
- **Can't tell whether the award is defence-relevant:** leave it out. Version one only includes awards it is confident about.

## Logic
- **Trigger:** runs automatically every **Monday at 8:00am**. A manual "run now" option exists for testing.
- **Decision points (in order):**
  1. Is the award defence-related (e.g. DND as the buyer, security requirements, controlled goods)? No → skip.
  2. Is the winner in the 20–200 person range? No → skip.
  3. Which of the 5 segments does it fit? → picks the email angle.
  4. Has this company been contacted before, or is it on the do-not-contact list? Yes → skip.
  5. Can a VP Eng / Eng Manager email be found? No → general inbox if under 50 people, otherwise the "couldn't find person" list.
  6. Rank the remaining companies by award recency and keep the top 20. If there are fewer than 20 good matches, send fewer. Never pad the list.
- **Rules:**
  - **One company, one email.** Never re-contact a company in the tracking sheet, even if it wins another award. A company can be manually re-opened.
  - **Never contact** existing customers, pilots, or active conversations (do-not-contact list).
  - **Every email must name the specific award.** No award means no draft, so no generic emails are ever created.
  - **Facts only from the award notice and the messaging doc.** No invented statistics, customer names, or claims about the prospect's compliance status.
  - If one company has multiple recent awards, combine them into **one** email.
  - **Nothing is sent automatically.** The system only creates drafts.
- **Human-in-the-loop:** every draft is reviewed in Slack by Ashwin or the founder. Only an explicit "✅ Save to Gmail" click creates a Gmail draft, and Ashwin sends manually from Gmail.

## Output
- **Produces:**
  - **One Slack message per prospect** in a dedicated channel (e.g. `#outbound-drafts`), containing:
    - Company, size, segment, and a status tag (🟢 verified / ⚠️ unverified size / 📮 general inbox)
    - Contact name, title, and email
    - The award: description, value, date, and a link to the notice
    - The draft email (subject + body)
    - Buttons: **✅ Save to Gmail** · **⏭️ Skip** (asks for a one-word reason) · **✏️ Edit** (tweak the text in Slack before saving)
  - **One summary message per run**, e.g. "Checked 340 awards → 22 matched → 20 drafts → 3 couldn't find a person (listed below)."
  - **Gmail drafts** in Ashwin's inbox (only for approved prospects).
- **Consumer:** Ashwin and the founder (review); Ashwin (sends from Gmail); the VP Eng / Eng Manager (receives the email).
- **The email's ask:** "Would you be interested in exploring Rendatum as a free pilot on this [bid/awarded contract], and giving us feedback?"
- **Storage:** a simple **tracking sheet**, one row per prospect: company, contact, segment, award, date drafted, status (*drafted → saved to Gmail → sent → replied / skipped + reason*). It also serves as the "already contacted" list and the place to measure success.

## Version Control
- **Repo:** GitHub (private by default)
- **`.gitignore` must exclude:** `.env`, API keys (Clay, Slack, Gmail), `logs/`, local data files (downloaded award spreadsheets, exports of the tracking sheet), any secrets
- **Commit cadence:** at least one commit per working milestone; push regularly
- **Why:** one rollback-able safety net is worth more than any other guardrail in early builds

## Logging (Phase 1 Guardrail)
- **Log location:** `logs/run.log` at the project root
- **What gets logged:** run start and end times; how many awards were checked; for every company, whether it was kept or skipped and **why**; every Clay lookup (what was asked, what came back, success or failure); every draft created; every Slack post and Gmail draft save (with status); every Skip click and its reason; every error with full context
- **Format:** plain-English lines with timestamps, e.g. `2026-10-12 08:01 — Skipped "Acme Aerospace": 1,400 employees (over 200)`
- **Why:** in version one, this is the single best tool for debugging. When you ask "why didn't Company X show up?", the answer is in the log.

## High-Stakes Actions & Approval Gates
- **Action:** sending a cold email to a prospect
  - **Why it's high-stakes:** it can't be unsent; a wrong fact or a wrong recipient costs credibility with a small, security-minded audience
  - **Approval gate:** the system never sends. A draft only reaches Gmail after a human clicks "✅ Save to Gmail" in Slack, and Ashwin presses Send manually in Gmail.
- **Action:** creating Gmail drafts
  - **Why it's high-stakes:** low risk (drafts can be deleted), but it touches a real inbox
  - **Approval gate:** only created one at a time, on an explicit button click per prospect. No bulk creation.
- **Action:** writing to the tracking sheet
  - **Why it's high-stakes:** it is the "already contacted" list. A wrong or lost row could cause a company to be emailed twice.
  - **Approval gate:** the system only adds rows or updates status; it never deletes rows. The sheet is backed up / version-tracked.

## System Edges
- **Edge 1: Drafts pile up unreviewed.** → If the previous week's drafts haven't been reviewed, Monday's run does **not** create new ones. It posts "⏸️ 18 drafts still waiting, skipping this week's run" instead.
- **Edge 2: The system misjudges a company** (e.g. a large prime that looked small, or a non-defence firm). → Caught at human review. The ⏭️ Skip button asks for a one-word reason ("too big", "not defence"), which is logged and used to tighten the rules.
- **Edge 3: The AI writes something wrong** (wrong award details, invented claims, implying non-compliance). → The email may only use facts from the award notice and the messaging doc, and the award link sits next to every draft so it can be checked in seconds.
- **Edge 4: Award data or Clay is down or returns nothing.** → Retry 2 more times over the next hour. If it still fails, post "❌ Run failed: couldn't reach [source]" in Slack. A run with **zero** results is also flagged, since that usually means something broke.
- **Edge 5: The same company gets drafted twice** (multiple awards, or the system runs twice by accident). → Check the tracking sheet before every draft, and combine multiple awards for one company into a single email.

## System Diagram
See `diagram.html` for the visual flow.

## Suggested Tech Stack (High-Level)
- **A scheduler** to run the job every Monday at 8am
- **A downloader / reader** for the public CanadaBuys award notices spreadsheet
- **Clay** for company details and contact lookup
- **An AI model** to classify segments and write the drafts, grounded in a messaging doc
- **Slack** (a bot posting into a dedicated channel, with interactive buttons)
- **Gmail** (creating drafts in Ashwin's inbox)
- **A simple spreadsheet** for the tracking sheet / "already contacted" list
- **A plain-text log file**

## Phase 2 (Not in Version One)
- **Subcontractor discovery:** when a large prime wins a defence award, work out which smaller firms in your ICP are likely in its supply chain, and contact them. This reaches more of the core Tier 1/Tier 2 subcontractor ICP.
- **Open tenders:** contact companies that *match* open defence tenders (bidders are not public).
- **Automatic reply detection** from Gmail, updating the tracking sheet without manual marking.

## Open Questions
- **How do we tell whether an award is CPCSC-relevant?** Check a sample of recent DND award notices to see whether CPCSC or security requirements are stated, or whether this must be inferred (buyer, keywords, controlled goods). This is the riskiest assumption, so validate it first.
- **How many defence awards per week go to firms with 20–200 people?** Confirm the pool is big enough to reach ~20 prospects/week, and adjust the 60-day window or size range if not.
- **Clay's hit rate for VP Eng / Eng Manager emails at small Canadian defence firms.** If it's poor, test an alternative contact-finding tool.
- **Messaging doc:** pull the core pitch and the 5 segment angles out of the pitch deck into a short written doc before building the drafting step.
- **Reply-rate target:** 10–20% is well above typical cold email (1–5%). Revisit after 4 weeks of real data.
- **Which tool holds the tracking sheet** (Google Sheets, Airtable, Attio, HubSpot, etc.). Decide at build time.
- **Do-not-contact list:** compile the current customers, pilots and active conversations before the first run.
