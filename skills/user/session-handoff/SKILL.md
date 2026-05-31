---
name: session-handoff
description: >
  Compacts the current conversation into a structured handoff document that can be
  dropped into a new conversation, a different agent, or a future session — preserving
  full context without re-explaining from scratch. Use this skill at the end of any long
  working session, before switching to a different agent or Claude Project, or when a
  task needs to continue in a future conversation.
---

# Session Handoff

Adapted from Matt Pocock's handoff skill for Lex Autonomous agent operations.

## Core Principle

**A good handoff eliminates the re-explanation tax entirely.**

## Handoff Document Structure

### 1. PROJECT / SESSION IDENTITY
### 2. CURRENT STATE — ONE PARAGRAPH
### 3. DECISIONS MADE — LOCKED
### 4. OPEN ITEMS — IN PRIORITY ORDER
### 5. NEXT SESSION — FIRST ACTION
### 6. REFERENCE LINKS / IDs

## Output Format

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SESSION HANDOFF — [Project Name]
[Date] | [Session Type]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CURRENT STATE
[One paragraph, plain English]

DECISIONS MADE — LOCKED
• [Decision]: [What was decided]

OPEN ITEMS
• [Item]: [What needs to happen] | [Responsible] | [Blocker]

NEXT SESSION — START HERE
[Exact first action for the next session]

REFERENCE
• [Name]: [Link or ID]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Compact Mode

```
HANDOFF — [Project] — [Date]
Done: [What was completed]
Open: [What remains]
Next: [First action]
Ref: [Key links/IDs]
```
