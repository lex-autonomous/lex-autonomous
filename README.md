# Lex Autonomous — Agent & Skills Repository

This is the canonical Git repository for the Lex Autonomous agent system.

It contains two things:
1. **Agent instruction files** — the CLAUDE.md that powers each agent's Claude Project
2. **Skill files** — reusable operating procedures mounted across agents

## How This Works

Every Claude Project connects to this repo. The Instructions field in each project contains a short pointer — not the full system prompt. The full system prompt lives in the agent's CLAUDE.md file here.

### Instructions Field Template (paste into each agent's Claude Project)
```
Your full instructions are in this project's knowledge base.
Read the file at /mnt/project/agents/[agent-folder-name]/CLAUDE.md before doing anything else.
That file is your source of truth. Do not proceed until you have read it.
```

## Folder Structure

```
lex-autonomous/
├── README.md                          ← This file
├── CLAUDE.md                          ← Axiom / Agents Lab instructions
├── agents/
│   ├── axiom-mercer/
│   │   └── CLAUDE.md                  ← Axiom's full system prompt (same as root CLAUDE.md)
│   ├── sloane-rhys/
│   │   └── CLAUDE.md                  ← Sloane's full system prompt
│   ├── cassandra-voss/
│   │   └── CLAUDE.md                  ← Cassandra's full system prompt
│   └── [agent-name]/
│       └── CLAUDE.md                  ← Each agent gets their own folder
└── skills/
    └── user/
        ├── agent-persona-creator/
        │   └── SKILL.md
        ├── answer-accuracy-standard/
        │   └── SKILL.md
        ├── course-architect/
        │   └── SKILL.md
        ├── dr-copywriter/
        │   └── SKILL.md
        ├── offer-intelligence/
        │   └── SKILL.md
        ├── social-content-planner/
        │   └── SKILL.md
        ├── session-handoff/
        │   └── SKILL.md
        ├── misalignment-detection/
        │   └── SKILL.md
        └── ubiquitous-language/
            └── SKILL.md
```

## Adding a New Agent

1. Create a folder under `agents/` using the agent's name in lowercase with hyphens
2. Add a `CLAUDE.md` file with their full system prompt
3. Commit and push
4. In the agent's Claude Project, set the Instructions field to the pointer template above
5. Connect the Claude Project to this repo

## Updating an Agent

1. Edit their `CLAUDE.md` file in GitHub
2. Commit with a message: `[Agent Name] — upgrade to v[X.X] — [date]`
3. Changes take effect on the next conversation automatically

## Adding a New Skill

1. Create a folder under `skills/user/` using the skill name in lowercase with hyphens
2. Add a `SKILL.md` file
3. Reference it in the relevant agent's CLAUDE.md under `[MOUNTED SKILLS]`

## Unbound Labs (Client Repo)

Sloane Rhys operates in a separate client-owned repo.
That repo lives at: [to be set up — separate from this one]
Sloane's skill files are copied there, not referenced from here.
