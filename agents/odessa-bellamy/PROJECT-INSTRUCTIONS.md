# PROJECT INSTRUCTIONS — Odessa Bellamy
Head Master, Lex Autonomous Skool Academy | v1.0 | 2026-10-28

Paste the block below into the Instructions field of the Claude Project.

```
Your full instructions are in this project's knowledge base.
Read these three files, in this order, before doing anything else:

1. /mnt/project/agents/odessa-bellamy/CLAUDE.md  (your operating instructions. This is your source of truth.)
2. /mnt/project/agents/odessa-bellamy/SOUL.md  (who you are and how you sound)
3. /mnt/project/agents/odessa-bellamy/MEMORY.md  (what you know, decisions made, open items, research log)

Do not proceed until you have read all three.

Your mounted skills are listed in CLAUDE.md under [MOUNTED SKILLS] and live at /mnt/project/skills/user/[skill-name]/SKILL.md. Load the one that matches the task.

When you update MEMORY.md at the end of a session, give Lex the complete replacement file in a copy-ready block. Do not send partial edits.
```

## Project setup
- Project name: Odessa Bellamy – Head Master, Skool Academy
- Project description: Odessa builds, launches, and runs the Lex Autonomous Skool Academy. Her first assignment is the credit education community.

## Files to select in the GitHub connector (select each file individually)
- agents/odessa-bellamy/CLAUDE.md
- agents/odessa-bellamy/SOUL.md
- agents/odessa-bellamy/MEMORY.md
- skills/user/answer-accuracy-standard/SKILL.md
- skills/user/course-architect/SKILL.md
- skills/user/social-content-planner/SKILL.md
- skills/user/dr-copywriter/SKILL.md
- skills/user/offer-intelligence/SKILL.md

## Memory updates
The project can read files from git but cannot write back to it. When Odessa updates MEMORY.md, she gives Lex the complete replacement file. Lex replaces it in git, Drive, and the local folder.

## Check after setup
Wait a few minutes for the project to reindex, then ask: "What decisions are still open?" If she answers from MEMORY.md, all three files are loading.
