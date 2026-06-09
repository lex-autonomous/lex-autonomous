Precision lead prospecting operating system for Hunter Cross. Use this skill whenever Hunter needs to define or refine an ICP, build a prospect list, score or qualify leads, pull cross-reference intelligence from LinkedIn, websites, or social media, identify decision-maker and owner profiles, surface trigger events, or prepare a handoff-ready prospect record for the outreach agent. Triggers include: "build a prospect list," "find decision makers," "pull ICP," "score these leads," "cross-reference this contact," "research this company," "find the owner," "who should we reach out to," or any request to identify, qualify, or enrich a prospect before outreach begins. Always use this skill before building any list, running any enrichment, or handing off a record to an outreach agent.Lead Prospector Skill
Hunter Cross — Lex Autonomous
A precision prospecting operating system. Not a lead generation tool — an
intelligence-first targeting framework that produces handoff-ready prospect
records for the outreach agent.
Applies to: Hunter Cross. Every list build, ICP definition, contact research
task, and pre-handoff enrichment run goes through this skill.

How This Skill Works
Every prospecting task follows the same four-phase sequence:

Define — Lock the ICP before touching any data source
Discover — Find companies and contacts that match
Cross-Reference — Validate and enrich using LinkedIn, website, and social
Package — Structure the output as a handoff-ready prospect record

Do not skip phases. Volume means nothing without validation. A list that hasn't
been cross-referenced is an unverified guess — not a qualified prospect.

Phase 1 — ICP Definition (Run Before Every List Build)
Before any research begins, the ICP must be locked. No exceptions.
Required ICP Fields
FieldNotesIndustry / VerticalBe specific — "marketing agencies" not "services"Company sizeRevenue range or headcount range — pick one or bothGeographyCountry, region, state, or cityGrowth stageStartup / SMB / Mid-market / EnterpriseTech stack signalsTools they use that indicate fit (e.g., using GHL, HubSpot, Shopify)Decision-maker title(s)The person who owns the problem — not just the buyer titleOwner / Founder flagIs this a founder-led business? Owner-operated? Flag it.Pain signalWhat problem do they have that makes them a fit right now?Anti-ICP markersWho is explicitly NOT a fit — save everyone's time
ICP Validation Check
Before building any list, run this:

 Is the vertical specific enough to filter meaningfully?
 Is the company size range tight enough to produce qualified names?
 Is the decision-maker title mapped to actual buying authority in this company type?
 Is there at least one observable pain or fit signal beyond demographics?
 Is the anti-ICP list defined?

If any field is missing, ask the single most important clarifying question to
resolve the biggest gap. One question. Not five.

Phase 2 — Discovery (Finding Companies and Contacts)
Primary Data Tools
Vibe Prospecting (Explorium) — Primary Tool
Use for company search, contact discovery, and enrichment at scale.
Workflow inside Claude Projects (MCP connector):

Connect via: https://vibeprospecting.explorium.ai/mcp
Authenticate via browser OAuth on first use
Always run a sample preview (5–10 results) before full export
Confirm record count and credit cost before pulling full dataset

Core actions available:

Company search by industry, size, location, tech stack, growth stage, funding
Contact discovery by title, seniority, function
Record matching from raw/messy name+company inputs
Trigger event lookup (funding rounds, leadership changes, hiring surges, tech changes)
Enrichment: email, LinkedIn URL, phone, title verification
Export to CSV for CRM or handoff

Workflow inside Claude Code:

Plugin path: agentsource-plugin from explorium-ai/agentsource-plugin
SKILL.md reference: skills/vibe-prospecting/SKILL.md in that repo
Supports multi-step chained workflows: company search → contact find → enrich → export

Manual / Supplementary Sources
When Vibe Prospecting doesn't have a record, or for high-priority accounts
requiring deeper intelligence, use these in order:

LinkedIn (primary for contact verification and role confirmation)
Company website (ownership, team page, about page)
Facebook / Instagram (owner identity, business personality, audience signals)
Google / news search (recent activity, press, funding, partnerships)

Signal-First Discovery Protocol
Every prospect must have at least one observable signal before being added
to a list. Signals by category:
Company-level signals:

Recent funding round (Series A/B indicates budget and growth intent)
New leadership hire (new VP/Director = mandate to change something)
Job postings (hiring for SDR, marketing, ops = growth motion is active)
Tech stack change (new CRM, new marketing tool = someone just made a decision)
Public complaint about a competitor (they're shopping)
Revenue milestone or press mention (visibility = credibility check)

Owner / Founder signals (for SMB and founder-led targets):

Active on social media posting about business problems
Recent LinkedIn activity indicating growth focus
Visible on website as named founder (not just "our team")
Speaking, podcast, or event appearance in the past 90 days
Direct connection to a known network or referral source

Contact-level signals:

Title matches buyer map (not just demographic fit)
LinkedIn shows recent activity (not dormant)
Has been promoted in the last 6–12 months (new authority, new mandate)
Listed as a contributor or decision-maker in visible company content


Phase 3 — Cross-Reference Intelligence
For every high-priority prospect, run the three-source cross-reference
before adding them to the handoff list. This is what separates a name
from a real, contactable person.
Source 1: LinkedIn
What to pull:

Full current title and company (verify against Vibe data — titles drift)
Tenure at current role (under 6 months = still finding their footing; over 3 years = established authority)
Recent activity (posts, likes, comments in the last 30 days = they're active and reachable)
Connections to Lex or known network (warm path exists)
Summary/About section (tells you their frame — how they see their own role)
Education and career path (are they a founder? Operator? Recently promoted?)

Owner / Decision-Maker Verification:

Is this person listed as Founder, Owner, CEO, or Principal? → Owner-operated flag ON
If not the owner, do they have budget authority for this type of decision?
Are there multiple decision-makers at this company (committee buy)? Flag it.

LinkedIn Enrichment Checklist:

 Title verified and current
 Tenure confirmed
 Activity level noted (active / dormant / inactive)
 Network overlap checked
 Owner / DM flag set

Source 2: Company Website
What to pull:

About / Team page: Who runs this business? Is the owner named and visible?
Services or product page: What do they actually sell? Does it match ICP fit logic?
Testimonials or case studies: What outcomes do they claim? (reveals sophistication level)
Blog or content: Are they producing content? (signals marketing maturity)
Contact page: Is there a direct email, phone, or form? (contact hygiene)
Footer: Look for founding year, legal entity name, location — cross-check against Vibe data

Red Flags to Log:

Site is under construction or clearly outdated
No team page (can't confirm owner identity)
Generic or templated copy (may be a shell or low-engagement business)
No contact method other than form (low responsiveness likely)

Website Intelligence Output:

Owner confirmed: Yes / No / Unclear
Business stage signal: Early / Growing / Established / Stagnant
Content activity: Active / Minimal / None
Contact accessibility: High / Medium / Low

Source 3: Social Media (Facebook and Instagram Primary)
What to pull for founder-led / SMB targets:

Facebook Business Page: Is it active? Follower count? Last post date?
Facebook Personal Profile (if public): Owner's tone, interests, business mentions
Instagram Business Account: Visual brand, posting frequency, engagement signals
Content themes: Are they posting about their business? About problems we solve?
Comments and engagement: Are customers interacting? Does the owner respond?

What to look for:

Owner's personality and communication style (feeds outreach tone for handoff)
Recent posts mentioning pain points, goals, or growth milestones
Audience quality signals (are their followers real customers or just followers?)
Response behavior (do they reply to DMs and comments? High response rate = reachable)

Social Intelligence Output:

Platform presence: Active / Minimal / None (per platform)
Owner communication style: Formal / Casual / Visual / Educational / Sales-heavy
Relevant recent content: Noted if applicable
Reachability signal: High / Medium / Low


Phase 4 — Prospect Record Packaging (Handoff Standard)
Every prospect delivered to the outreach agent is a complete record.
No half-built entries. No placeholders. If a field can't be verified,
mark it as unverified — do not omit it.
Handoff Record Format
PROSPECT RECORD
---
Name:
Title:
Company:
Industry:
Company Size (employees):
Revenue Range (if known):
Location:
Website:
LinkedIn URL:
Email (verified / unverified):
Phone (verified / unverified):
---
FIT SCORE: [1–10]
FIT RATIONALE: [1–2 sentences — why are they on this list]
---
TRIGGER SIGNAL: [What event or signal makes now the right time]
---
OWNER / DECISION-MAKER STATUS:
  - Owner-operated: Yes / No / Unclear
  - Decision-maker confirmed: Yes / No / Unclear
  - Committee buy risk: Yes / No
  - Notes:
---
CROSS-REFERENCE SUMMARY:
  - LinkedIn: [title verified, tenure, activity level, network overlap]
  - Website: [owner confirmed, stage signal, contact accessibility]
  - Social: [platform, activity level, communication style, reachability]
---
OUTREACH NOTES FOR HANDOFF AGENT:
  [2–4 sentences: tone recommendation, angle to lead with, anything to
  avoid, any warm connection or shared context to reference]
---
RECORD STATUS: Ready for Outreach / Needs Verification / Do Not Contact
Fit Scoring Guide
ScoreMeaning9–10Perfect ICP fit + active signal + verified decision-maker + warm path7–8Strong fit + at least one signal + DM confirmed5–6Decent fit, signal present, DM unconfirmed or role unclear3–4Demographic fit only, no signal, weak contact accessibility1–2Marginal fit — include only if volume is explicitly requested
Default standard: do not hand off records below a 5. Flag anything
below 7 for Lex's review before outreach agent receives it.

List Output Format
When delivering a full prospect list (not individual records):
| # | Name | Title | Company | Signal | Fit Score | LinkedIn | Email | Status |
|---|------|-------|---------|--------|-----------|----------|-------|--------|
Each row links to the full Prospect Record in the session notes or
Notion handoff page if detailed intelligence was gathered.

Trigger Event Monitoring
Hunter tracks trigger events as ongoing intelligence — not just at list
build time. Events to monitor for active target accounts:
Event TypeWhy It MattersFunding round announcedBudget unlocked, growth mandate activeNew C-suite / VP hireNew leader = new priorities = new buying windowHeadcount surge (hiring 5+ roles)Company is scaling — needs infrastructureTech stack changeJust made a decision — vendor switching is in motionCompetitor complaint (public)They're frustrated and shoppingFounder posts about a problem we solveSelf-identified painCompany anniversary (5, 10 yr)Reflection mode — often open to change conversationsRecent press / awardCredibility moment — good time to reach out with congratulations

Quality Control — Pre-Handoff Checklist
Run this before any list leaves Hunter's hands:

 Every record has a fit score with rationale
 Every record has at least one observable trigger signal
 LinkedIn, website, and social cross-reference completed on all records scoring 7+
 Owner / DM status confirmed or flagged as unclear
 No record below a 5 included without Lex approval
 Outreach notes written for every record — not placeholder text
 Record status field set on every entry
 List labeled with version, date, and ICP it was built against


Handoff Protocol to Outreach Agent
When a list is ready for the outreach agent:

Export the full list in the standard format (CSV or structured Notion page)
Include the ICP brief that drove the list (so outreach agent knows who they're targeting)
Flag any records that need special handling (committee buy, sensitive contact, warm intro available)
Tag record status clearly: Ready for Outreach / Needs Verification / Do Not Contact
Log the handoff in Notion with: list name, record count, date, outreach agent assigned

Never hand off a list verbally or through chat only. Every list gets a
saved record so the outreach agent can execute independently without having
to ask Hunter for context.

Common Mistakes to Avoid

Building a list before the ICP is locked — volume without definition is wasted time
Trusting Vibe Prospecting data without cross-referencing — enrichment tools have stale records
Marking a title as "Decision Maker" without verifying buying authority for this specific decision type
Skipping the social cross-reference on founder-led targets — social is often the richest signal source for SMB
Handing off records with missing outreach notes — the outreach agent needs context, not just a name
Logging a trigger event without dating it — a 6-month-old trigger is not a current signal
Assuming LinkedIn activity = reachability — check their response behavior, not just post frequency


Save Protocol Integration
After every list build or research session, save:

The ICP brief to the relevant Notion project page
The full prospect list (CSV or table) with version and date
Any trigger events identified for future monitoring
A session note: records built, signals found, handoff status

Precision over volume. Every time.
