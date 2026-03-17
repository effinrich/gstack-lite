# gstack-lite

A condensed, binary-free port of [Garry Tan's gstack](https://github.com/garrytan/gstack) — five workflow skills for Claude Code as plain Markdown files. No Bun, no compiled binary, no dependencies.

## What's included

| Command | What it does |
|---|---|
| `/plan-ceo-review` | Founder mode — challenges the literal request, finds the 10-star product |
| `/plan-eng-review` | Eng manager mode — architecture, diagrams, failure modes, test matrix |
| `/review` | Paranoid staff engineer — structural audit for bugs that survive CI |
| `/ship` | Release engineer — sync, test, lint, push, open PR |
| `/retro` | Eng manager — git-based retrospective with per-contributor breakdown |

> **What's not included:** `/browse`, `/qa`, and `/setup-browser-cookies` require a compiled Chromium binary. Install the full [gstack](https://github.com/garrytan/gstack) if you need those.

## Setup

**Requirements:** [Claude Code](https://docs.anthropic.com/en/docs/claude-code), Git.

### 1. Copy skill files into your project

```bash
mkdir -p .claude/skills
cp PLANNING.md REVIEW.md SHIP-RETRO.md .claude/skills/
```

### 2. Add the gstack section to your CLAUDE.md

```bash
cat CLAUDE-gstack-section.md >> CLAUDE.md
```

If you don't have a `CLAUDE.md` yet:

```bash
cp CLAUDE-gstack-section.md CLAUDE.md
```

### 3. Commit

```bash
git add .claude/skills/ CLAUDE.md
git commit -m "chore: add gstack-lite workflow skills"
```

Teammates get the skills automatically on `git clone` — no extra setup needed.

## Usage

Open Claude Code in your project and use the slash commands:

```
/plan-ceo-review   ← start here for any non-trivial feature
/plan-eng-review   ← lock in architecture after product direction is set
/review            ← structural audit before shipping
/ship              ← sync, test, push, PR — non-interactive
/retro             ← end-of-week retrospective from git history
```

### Recommended workflow

```
/plan-ceo-review  →  /plan-eng-review  →  [implement]  →  /review  →  /ship
```

Always run CEO review before Eng review. `/ship` is for a ready branch — not for deciding what to build.

## File structure

```
.claude/
└── skills/
    ├── PLANNING.md       # /plan-ceo-review + /plan-eng-review
    ├── REVIEW.md         # /review
    └── SHIP-RETRO.md     # /ship + /retro
CLAUDE.md                 # registers skills + enforces workflow rules
```

## Credit

Skills adapted from [garrytan/gstack](https://github.com/garrytan/gstack) (MIT).
