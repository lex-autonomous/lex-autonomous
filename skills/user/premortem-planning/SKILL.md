---
name: premortem-planning
description: >
  Run a structured failure analysis on any plan, launch, offer, agent build, client
  deliverable, or strategic decision before execution. Use when Lex wants to stress test
  something before committing to it. Triggers on: "premortem this," "what could kill this,"
  "stress test this plan," "find the blind spots," "poke holes in this," "what am I missing,"
  "where will this break," or "devil's advocate this." Do not trigger for simple questions,
  editing requests, vague ideas with no concrete plan, or decisions already made and irreversible.
---

# Premortem Planning

Adapted for Lex Autonomous operations. Original structure by premortem planning framework.

## Core Principle

**The plan looks solid right now. That is exactly when to stress test it.**

Run this skill before money, reputation, client trust, or strategic focus is on the line.
The goal is not to kill the idea. The goal is to make it harder to kill.

---

## Mandatory Triggers

Run this skill immediately when Lex says any of the following:

- premortem this
- premortem my [plan / launch / offer / agent / department]
- what could kill this
- stress test this plan
- future-proof this
- what am I missing here
- find the blind spots
- run a premortem

---

## Strong Triggers

Strongly consider running this skill when Lex says:

- what could go wrong
- am I missing anything
- poke holes in this
- where will this break
- devil's advocate this

---

## Do Not Trigger When

- Lex asks a factual question with a clear answer
- The request is for writing feedback or copy edits
- There is no concrete plan yet — only a vague idea
- The decision is already made and irreversible
- Lex explicitly wants perspectives, not failure analysis (use a different framework)

---

## Minimum Context Threshold

Before running the premortem, confirm three things are clear:

1. **What is being stress tested?** — the specific plan, offer, agent, launch, or decision
2. **Who does it affect?** — the audience, client, or stakeholder
3. **What does success look like?** — the target outcome

First, scan the current conversation for context already provided. If all three are clear, proceed immediately. If one is missing, ask only the single most important missing question. Do not make Lex fill out a form.

---

## Required Frame

Open every premortem with this premise — stated plainly, not dramatically:

> It is six months from now. This plan did not work. We are looking back to understand what went wrong before it happens.

That frame matters. It moves the conversation out of optimism and into useful discovery.

---

## Workflow

### Step 1 — Set the Frame

Restate the plan in one sentence. Name the audience or stakeholder. Define the success target.

### Step 2 — Generate Real Failure Reasons

List every genuine reason this plan could fail. Each failure reason must be:

- Specific to this actual plan — not generic
- Grounded in the details Lex provided
- Significant enough to change the approach if true
- Honest, not diplomatic

Do not pad the list. Four real risks are worth more than twelve obvious ones.

### Step 3 — Analyze Each Failure Mode

For each failure reason, dig one level deeper:

- **How it plays out** — 2-3 sentences showing the failure in motion
- **The assumption underneath** — the single belief that made this failure possible
- **The early warning sign** — one observable signal Lex can monitor before it's too late

### Step 4 — Deliver the Report

Structure the final output as follows:

1. **Most Likely Failure** — the failure mode with the highest probability
2. **Most Dangerous Failure** — the failure mode with the highest cost if it hits
3. **Hidden Assumption** — the largest unchallenged belief underneath the plan
4. **Revised Plan** — concrete changes that make the plan more resilient
5. **Pre-Launch Checklist** — 3 to 5 specific checks, tests, or safeguards before execution

---

## Output Format

**In chat (default):** Lead with the Most Likely Failure, the Hidden Assumption, and the single most important revision. Follow with the full report below if the detail is needed.

**Optional files when the plan is high-stakes:**
- `premortem-report-[date].html` — scannable summary with one card per failure mode
- `premortem-transcript-[date].md` — full context, raw failure reasons, analysis, and revised plan

Only produce files if Lex asks or if the stakes clearly warrant it.

---

## Tone Standard

Calm. Direct. Useful. This is not a critique session and it is not encouragement. It is a clear-eyed look at what could go wrong so Lex can fix it before it does.

Do not soften findings to be polite. Do not be harsh for sport. Deliver the truth in plain language with a path forward.

Lex Autonomous brand voice applies: calm confidence, practical insight, no hype, no drama.

---

## Lex Autonomous Use Cases

This skill belongs in any conversation where a meaningful plan is at stake. High-value triggers include:

- **New offers** — before Soren finalizes an offer structure
- **Agent department builds** — before Axiom begins a multi-agent architecture
- **Course launches** — before Reid signs off on a curriculum
- **Funnel deployments** — before Nadia pushes a client funnel live
- **Client deliverables** — before any consulting handoff where reputation is on the line
- **Consulting pitches** — before Lex presents a roadmap or proposal to a new client

---

## Portable Use Note

Any Lex Autonomous agent that receives this skill file should follow the context threshold, trigger rules, workflow, and report structure above. If the environment does not support file creation, produce the full report in chat. Transparency over performance — do not claim capabilities the environment does not support.
