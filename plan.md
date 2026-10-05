# Rendatum Award-Triggered Outbound

> This spec is designed to be used as context for a new Claude Code session. Drop it in a project folder and begin building from here.

## Outcome
Every week, the system finds up to 20 Canadian defence suppliers (20–200 people) that have either recently won a defence-related federal contract or **qualified for DND's Defence Drone Initiative (DDI) Marketplace**, identifies their VP of Engineering or Engineering Manager, and drafts a short, personal cold email offering a **free Rendatum pilot** in exchange for product feedback. Contract winners get an email about their specific contract; DDI companies get an email about preparing for their first DDI contracts. Drafts are reviewed in Slack by Ashwin or the founder, and approved drafts are saved to Ashwin's Gmail with one click, ready to send manually. "Done" means a Monday-morning Slack channel full of accurate drafts, each tied to a specific award or DDI qualification, that need little or no rewriting, with nothing ever sent automatically.

## Success Signal
- **Primary:** 2–4 replies per week from the ~20 weekly prospects (a 10–20% reply rate).
- Measured in the Attio "Rendatum Outbound" list. Replies show up automatically on the company's record (the sending Gmail is connected to Attio); Ashwin moves the list stage to "Replied" when a reply comes in.
- Secondary signal to watch: how many drafts are saved to Gmail without heavy editing, and the reasons given for skips.

## Target (ICP)
- **Person:** VP of Engineering or Engineering Manager.
- **Company:** Canadian defence suppliers with roughly 20–200 people that handle drawings, specs, DXF files and revision tables as Specified Information. Each segment gets its own email angle:
  1. **Engineering-heavy Tier 1 / Tier 2 subcontractors** heading toward CPCSC Level 2 in 2027 (core ICP). Angle: they want AI help on RFPs and specs, but control 03.01.20 makes most AI tools hard to approve.
  2. **Controlled Goods Program registrants**, often also handling ITAR data. Angle: a US-parented cloud tool is a hard sell to their security officer, so architectural sovereignty is a differentiator.
  3. **Dual-market suppliers already under CMMC / ITAR.** Angle: they already understand compliance, have budget for it, and feel the "where does the data go" question most acutely.
  4. **Engineering consultancies, design bureaus, CAD/drafting shops** in the defence chain. Angle: education. CPCSC reaches them even though they often assume it doesn't.
  5. **Bid-intensive firms with small (2–3 person) bid teams.** Angle: RFP cross-referencing pain.

## Two prospect sources
Each Monday's list mixes two sources:
1. **Contract winners (first priority):** companies that won a real defence contract in the last 60 days. Expect only **~2–4 per week** to reach a draft (see `research/2026-10-05-award-check.md`).
2. **DDI Marketplace companies (fills the rest, up to 20):** 385 Canadian companies that DND pre-approved as suppliers for drones, counter-drone, communications, engineering and testing work (qualified Aug 29 – Sep 11, 2026; the arrangement runs to July 2031). They have no contract yet, so their email is about **getting ready for their first DDI contracts**, not about a specific award. At ~15 a week, this list lasts several months.

## Inputs
- **Contract awards:** who won, buyer department, description, value, date, link. From the Government of Canada's public CanadaBuys award notices dataset (free, open data, refreshed every morning). Freshness: awards from the **last 60 days**; newest first. Many awards show a $0 value (standing offers), so emails must not depend on quoting a value.
- **DDI Marketplace list:** from the same CanadaBuys file. These entries are recognisable by the title "Defence Drone Initiative (DDI) Marketplace" and a $1 value. **Saved once as a separate list**, because they will drop out of the 60-day window in November. New DDI qualifiers that appear later are added to the list.
- **Company details:** size, location, what they do. From **Clay**. Freshness: looked up at run time.
- **Contact (VP Eng / Eng Manager) and email:** from **Clay**. Fallback for companies under 50 people: the company's general inbox (info@, contact@). Freshness: looked up at run time.
- **Rendatum messaging:** the core pitch, the angle for each of the 5 segments, and a separate **DDI opening** (see "Email wording" under Output). Currently in the pitch deck; **to be extracted into a short written messaging doc** that the system reads from. Freshness: updated manually when positioning changes.
- **Attio "Rendatum Outbound" list (the "already contacted" list):** a new list in the **Northern Loop** Attio workspace (free plan), created for this system. Freshness: always current; checked before every draft.
- **Existing CRM records:** before drafting, the system checks whether the company (or the contact) already exists anywhere in the Northern Loop Attio workspace, e.g. on the Sales or Fundraising lists, or from past emails synced from Gmail. It **still drafts the email**, but flags it in Slack so the reviewer can decide. There is no separate do-not-contact list today (no current customers, pilots or active conversations).

### When data is missing or wrong
- **No VP Eng / Eng Manager found, company under 50 people:** draft to the general inbox, tagged 📮, with slightly different wording ("Could you pass this to whoever leads engineering?").
- **No contact found, company 50+ people:** skip the company and list it in the Slack run summary under "found the company, couldn't find the person."
- **Company size or details unclear:** include it, but flag it ⚠️ "unverified size."
- **Can't tell whether the award is defence-relevant:** leave it out. Version one only includes awards it is confident about.
- **The award doesn't say whether CPCSC applies:** this is normal, because notices almost never say it. Judge fit from the type of work (engineering, manufacturing, R&D, electronics) instead. Skip parts resellers, vehicle dealers, food, cleaning, grounds and building services.
- **The same company appears under different spellings** (e.g. "GCPROC Ltd" vs "GC PROC LTD."): Attio matches companies by website, so look up each company's website first and check Attio by website, not by name.

## Logic
- **Trigger:** runs automatically every **Monday at 8:00am**. A manual "run now" option exists for testing.
- **Decision points (in order):**
  1. Which source is this: a real contract, or a DDI Marketplace qualification? → picks the email type.
  2. *(Contracts only)* Is the award defence-related and engineering-type work? No → skip.
  3. Is the company in the 20–200 person range? No → skip. (This applies to DDI companies too; the list includes large firms like CAE.)
  4. Which of the 5 segments does it fit? → picks the email angle.
  5. Is this company already in the "Rendatum Outbound" list, or ticked "Do not contact"? Yes → skip.
  6. Does the company or contact already exist elsewhere in Attio? Yes → draft anyway, but add the 👀 **Already in CRM** flag in Slack.
  7. Can a VP Eng / Eng Manager email be found? No → general inbox if under 50 people, otherwise the "couldn't find person" list.
  8. Build the weekly list: **contract winners first** (newest award first), then **fill up to 20 with DDI companies**. If there are fewer than 20 good matches, send fewer. Never pad the list.
- **Rules:**
  - **One company, one email.** Never re-contact a company that is already in the Attio "Rendatum Outbound" list, even if it wins another award. This includes a DDI company that later wins a real contract. A company can be manually re-opened.
  - **Never contact** a company ticked "Do not contact (Rendatum)" in Attio.
  - **Always flag** companies that already exist elsewhere in Attio, so a human sees the history before approving.
  - **Emails are written in English.** Companies based in Quebec are tagged ⚜️ in Slack so the reviewer can decide case by case.
  - **Company size:** 20–200 people, revisited once real Clay sizes are in (possibly lowered to 10 for DDI startups).
  - **Every email must name a specific trigger:** either the specific award, or the company's DDI Marketplace qualification. No trigger means no draft, so no generic emails are ever created.
  - **DDI emails never imply the company has won a contract.** They are pre-approved suppliers, not contract winners.
  - If a company is on the DDI list **and** has won a real contract, use the contract email.
  - **Facts only from the award notice and the messaging doc.** No invented statistics, customer names, or claims about the prospect's compliance status.
  - If one company has multiple recent awards, combine them into **one** email.
  - **Nothing is sent automatically.** The system only creates drafts.
- **Human-in-the-loop:** every draft is reviewed in Slack by Ashwin or the founder. Only an explicit "✅ Save to Gmail" click creates a Gmail draft, and Ashwin sends manually from Gmail.

## Output
- **Produces:**
  - **One Slack message per prospect** in a dedicated channel (e.g. `#outbound-drafts`), containing:
    - Company, size, segment, source (📄 contract / 🛩️ DDI Marketplace), and status tags (🟢 verified / ⚠️ unverified size / 📮 general inbox / ⚜️ Quebec)
    - 👀 **Already in CRM**, when it applies: which Attio list(s) it's on and its stage (e.g. "Sales — Discovery"), plus the date of the last email exchange if Attio has one
    - Contact name, title, and email
    - The trigger: for contracts, the description, value, date and a link to the notice; for DDI, the qualification date and a link to the notice
    - The draft email (subject + body)
    - Buttons: **✅ Save to Gmail** · **⏭️ Skip** (asks for a one-word reason) · **✏️ Edit** (tweak the text in Slack before saving)
  - **One summary message per run**, e.g. "Checked 340 awards → 4 contract winners + 16 DDI companies → 20 drafts → 3 couldn't find a person (listed below) · 290 DDI companies left on the list."
  - **Gmail drafts** in Ashwin's inbox (only for approved prospects).
- **Consumer:** Ashwin and the founder (review); Ashwin (sends from Gmail); the VP Eng / Eng Manager (receives the email).
- **Email wording:**
  - **Contract winners:** opens with the specific award. Ask: "Would you be interested in exploring Rendatum as a free pilot on this [awarded contract], and giving us feedback?"
  - **DDI Marketplace companies:** opens with their qualification. The angle: once DDI contracts start, they'll be handling DND specs, drawings and other Specified Information, and the CPCSC requirements come with that work. Example opening: *"Congratulations on qualifying for DND's Defence Drone Initiative Marketplace. When the first DDI contracts come through, your engineering team will be working with DND specs and drawings…"* Ask: "Would you be interested in trying Rendatum as a free pilot while you prepare for your first DDI contracts, and giving us feedback?" The exact wording is finalised in the messaging doc.
- **Storage:** **Attio, Northern Loop workspace (free plan)**.
  - The prospect's company and contact are saved as normal Attio Company and Person records (Attio prevents duplicates by matching on website / email).
  - A new list, **"Rendatum Outbound"**, holds one entry per prospect company, with stages *Drafted → Saved to Gmail → Sent → Replied / Skipped*, and fields for: source (contract / DDI), segment, trigger (award or DDI qualification) with link, date drafted, skip reason.
  - A **"Do not contact (Rendatum)"** checkbox on the Company record. Empty today; ticked manually if someone asks not to be contacted again.
  - This list is the "already contacted" list and the place to measure success.
  - Because Northern Loop's own Companies, People, Sales and Fundraising data live in the same workspace, the system **only ever touches the "Rendatum Outbound" list and the records it creates**. It never edits other lists or existing records' other fields.

## Version Control
- **Repo:** GitHub (private by default)
- **`.gitignore` must exclude:** `.env`, API keys (Clay, Slack, Gmail), `logs/`, local data files (downloaded award spreadsheets, exports of the Attio list), any secrets
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
- **Action:** writing to Attio (Northern Loop workspace)
  - **Why it's high-stakes:** it is the "already contacted" list. A wrong or lost row could cause a company to be emailed twice.
  - **Why it's also risky here:** the workspace holds Northern Loop's own CRM data, so a mistake could change unrelated records.
  - **Approval gate:** the system only adds records and list entries, or updates the stage; it never deletes anything and never edits records outside the "Rendatum Outbound" list. The list is exported to a file every week as a backup.

## System Edges
- **Edge 1: Drafts pile up unreviewed.** → If the previous week's drafts haven't been reviewed, Monday's run does **not** create new ones. It posts "⏸️ 18 drafts still waiting, skipping this week's run" instead.
- **Edge 2: The system misjudges a company** (e.g. a large prime that looked small, or a non-defence firm). → Caught at human review. The ⏭️ Skip button asks for a one-word reason ("too big", "not defence"), which is logged and used to tighten the rules.
- **Edge 3: The AI writes something wrong** (wrong award details, invented claims, implying non-compliance, or telling a DDI company it "won" a contract). → The email may only use facts from the award notice and the messaging doc, and the award link sits next to every draft so it can be checked in seconds.
- **Edge 4: Award data or Clay is down or returns nothing.** → Retry 2 more times over the next hour. If it still fails, post "❌ Run failed: couldn't reach [source]" in Slack. A run with **zero** results is also flagged, since that usually means something broke.
- **Edge 5: The same company gets drafted twice** (multiple awards, or the system runs twice by accident). → Check Attio (by company website) before every draft, and combine multiple awards for one company into a single email.

## System Diagram
See `diagram.html` for the visual flow.

## Suggested Tech Stack (High-Level)
- **A scheduler** to run the job every Monday at 8am
- **A downloader / reader** for the public CanadaBuys award notices spreadsheet
- **Clay** for company details and contact lookup
- **An AI model** to classify segments and write the drafts, grounded in a messaging doc
- **Slack** (a bot posting into a dedicated channel, with interactive buttons)
- **Gmail** (creating drafts in Ashwin's inbox)
- **Attio** (Northern Loop workspace, free plan) for the "already contacted" list, pipeline stages and do-not-contact flag
- **A plain-text log file**

## Phase 2 (Not in Version One)
- **Subcontractor discovery:** when a large prime wins a defence award, work out which smaller firms in your ICP are likely in its supply chain, and contact them. This reaches more of the core Tier 1/Tier 2 subcontractor ICP.
- **Open tenders:** contact companies that *match* open defence tenders (bidders are not public).
- **Automatic stage updates on reply**: Attio shows replies on the record once Gmail is connected; moving the list stage to "Replied" automatically can come later.

## Open Questions
- ~~How do we tell whether an award is CPCSC-relevant?~~ **Answered 2026-10-05:** notices don't say, so fit is judged from the type of work. See `research/2026-10-05-award-check.md`.
- ~~Is the award pool big enough for ~20/week?~~ **Answered 2026-10-05:** no, only ~2–4/week. Fixed by adding the DDI Marketplace list as a second source.
- **What happens when the DDI list runs out** (in roughly 4–6 months)? Options: add good-fit contract winners from the last 6 months (~820 companies won defence work), or accept a smaller weekly list.
- **Is DDI a segment of its own?** Decide with the founder whether drone and defence-tech companies get their own angle in the messaging doc, or keep the 5 segments with just a DDI opening line.
- **Clay's hit rate for VP Eng / Eng Manager emails at small Canadian defence firms.** If it's poor, test an alternative contact-finding tool.
- **Messaging doc:** pull the core pitch and the 5 segment angles out of the pitch deck into a short written doc before building the drafting step.
- **Reply-rate target:** 10–20% is well above typical cold email (1–5%). Revisit after 4 weeks of real data.
- ~~Which tool holds the tracking sheet?~~ **Decided 2026-10-05:** Attio, Northern Loop workspace (free plan).
- ~~Can an outside system write to Attio on the free plan?~~ **Confirmed 2026-10-05:** yes. API access is included on all Attio plans, including Free. Free allows up to 3 objects (we use the 2 standard ones, Companies and People) and the pricing page shows no limit on lists. Use a workspace API key limited to only the permissions the system needs.
- ~~Which Gmail sends Rendatum emails?~~ **Answered 2026-10-05:** the sending mailbox is already connected to the Northern Loop Attio workspace, so replies appear in Attio automatically.
- ~~Do-not-contact list~~ **Answered 2026-10-05:** nobody to exclude today. Existing CRM records are flagged in Slack instead of skipped.
- **No opt-out line (decided 2026-10-05).** Ashwin chose not to include an unsubscribe line in the emails. The tradeoff to know: Canada's anti-spam law (CASL) generally expects commercial emails to identify the sender and include a way to unsubscribe, even for one-to-one B2B outreach, and penalties can be significant. Revisit if volume grows or if anyone raises it.
- ~~Defaults~~ **Confirmed 2026-10-05:** 20–200 size range for now; English-only with Quebec tag; Slack channel `#outbound-drafts`; founder signs off on the messaging doc once; Ashwin checks the Clay plan allows outside lookups and that apps can be added to Slack.
