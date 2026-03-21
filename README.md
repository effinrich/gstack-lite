# gstack-lite

A condensed, binary-free port of [Garry Tan's gstack](https://github.com/garrytan/gstack), repackaged as portable Markdown workflow docs for AI coding agents. Six workflow modes, no Bun, no compiled binary, no dependencies.

The workflow itself is **agent-agnostic**. Claude Code is one good adapter for
it, but the repo is designed so any agent can use the Markdown docs directly.

> **New:** `gstack-lite` is now **agent-agnostic first, Claude-compatible
> second**. The workflow docs are the primary product; Claude packaging is an
> optional adapter layer.

## How `gstack-lite` differs from `gstack`

| `gstack` | `gstack-lite` |
|---|---|
| Broader packaged toolchain | Lightweight, docs-first workflow pack |
| Includes browser-oriented workflows and tooling | No Bun, no compiled binary, no dependency-heavy setup |
| More tied to its native tool environment | Agent-agnostic by design |
| Primary product is the packaged tool experience | Primary product is portable Markdown workflow docs |
| UI/browser extras live in the main toolchain | Ships `gstack-lite-storybook.md` and `gstack-lite-rubric.md` as public companion docs |

## Agent support

- **Any coding agent**: start with `AGENTS.md`, then use `GSTACK_LITE.md`
- **Claude Code**: can additionally package the split docs into `.claude/skills/`
- **React repos**: use `gstack-lite-storybook.md` for Storybook/Chromatic policy
- **Evaluation / benchmarking**: use `gstack-lite-rubric.md` or `/scorecard`

## Quick start

1. Read `AGENTS.md`
2. Use `GSTACK_LITE.md` as the main workflow reference
3. If your project is a React app with reusable components, also use
   `gstack-lite-storybook.md`
4. If you are testing or benchmarking the workflow, also use
   `gstack-lite-rubric.md`

If you're using Claude Code, you can optionally package the split docs into
`.claude/skills/` for native slash-command ergonomics.

File naming convention in this repo:
- repo-branded public docs use `gstack-lite-*`
- adapter-friendly workflow docs keep short stable names like `PLANNING.md`
  and `REVIEW.md` for easy reuse in agent-specific folders

## Core modes

| Mode | Claude alias | What it does |
|---|---|---|
| Founder mode | `/plan-ceo-review` | Challenges the literal request, finds the 10-star product |
| Eng manager mode | `/plan-eng-review` | Architecture, diagrams, failure modes, test matrix |
| Review mode | `/review` | Structural audit for bugs that survive CI |
| Ship mode | `/ship` | Sync, test, lint, push, open PR |
| Retro mode | `/retro` | Git-based retrospective with per-contributor breakdown |
| Scorecard mode | `/scorecard` | Structured rubric for testing repos, agents, or workflow runs |

Companion docs shipped in this repo:
- `AGENTS.md` — agent-neutral entry point
- `GSTACK_LITE.md` — single-file workflow reference
- `gstack-lite-rubric.md` — public evaluation rubric / scorecard
- `gstack-lite-storybook.md` — public Storybook/Chromatic policy for React repos

> **Need browser automation?** Workflows like `/browse`, `/qa`, and `/setup-browser-cookies` require tooling outside this repo. Install the full [gstack](https://github.com/garrytan/gstack) if you need those.

## Setup

**Requirements:** a coding agent that can read Markdown instructions, plus Git.

### 1. Agent-neutral setup

Use these docs directly in your project or agent context:

- `AGENTS.md`
- `GSTACK_LITE.md`
- `gstack-lite-rubric.md` (for testing / benchmarking)
- `gstack-lite-storybook.md` (for React repos)

If your agent supports repository instruction files, `AGENTS.md` is the best
entry point.

### 2. Optional Claude Code adapter

If you're using [Claude Code](https://docs.anthropic.com/en/docs/claude-code),
you can additionally package the split docs as native skills:

```bash
mkdir -p .claude/skills
cp PLANNING.md REVIEW.md SHIP-RETRO.md RUBRIC.md .claude/skills/
```

Optionally also copy the public companion docs into your repo root or docs folder:
- `AGENTS.md`
- `GSTACK_LITE.md`
- `gstack-lite-rubric.md`
- `gstack-lite-storybook.md`

### 3. Add the workflow guidance to your agent instructions

For any agent, reference or paste the shipped docs into your repo-level
instruction file.

For Claude Code, that file is `CLAUDE.md`.

This repo does **not** ship a generated `CLAUDE-gstack-section.md` file.
Instead, reference the shipped docs directly or paste the sections you want to
enforce into your project's instruction file:

- `GSTACK_LITE.md` for the main planning/review/ship/retro workflow
- `gstack-lite-rubric.md` for structured evaluation and benchmarking
- `gstack-lite-storybook.md` for React Storybook/Chromatic defaults

If you're using Claude Code and don't have a `CLAUDE.md` yet, create one and add
the relevant guidance.

```bash
touch CLAUDE.md
```

### 4. Commit

For Claude Code, that usually looks like:

```bash
git add .claude/skills/ CLAUDE.md
git commit -m "chore: add gstack-lite workflow skills"
```

If you're using a different agent setup, commit the equivalent instruction files
you added to your repo.

Teammates get the committed workflow docs and instruction files automatically on
`git clone` — no extra setup needed.

## Usage

With any coding agent, ask it to use the mode definitions from `AGENTS.md` /
`GSTACK_LITE.md`.

Plain-language example prompts:

- "Use founder mode from `GSTACK_LITE.md` for this feature request."
- "Use eng review mode from `GSTACK_LITE.md` and give me architecture, failure modes, and a test matrix."
- "Use review mode from `GSTACK_LITE.md` on this diff."
- "Use `gstack-lite-rubric.md` to score this repo test run."

If you're using Claude Code with the optional adapter, you can use the slash
commands directly:

```
/plan-ceo-review   ← start here for any non-trivial feature
/plan-eng-review   ← lock in architecture after product direction is set
/review            ← structural audit before shipping
/ship              ← sync, test, push, PR — non-interactive
/retro             ← end-of-week retrospective from git history
/scorecard         ← structured evaluation for testing repos, agents, or runs
```

### Recommended workflow

```
/plan-ceo-review  →  /plan-eng-review  →  [implement]  →  /review  →  /ship
```

Always run CEO review before Eng review. `/ship` is for a ready branch — not for deciding what to build.
Use `/scorecard` when you want to benchmark the workflow itself or compare test runs.

## Opinionated frontend default

For any React app repo with reusable components, Storybook is required.
Treat it as UI documentation plus an automated QA surface: shared components
should have stories for key states, and CI should run as much Storybook
automation as the project supports (static build, interaction tests,
accessibility checks, and visual regression where available).

### Repo-specific Storybook doc for React repos

This repo now includes `gstack-lite-storybook.md`, a repo-specific public
Storybook/Chromatic policy doc. You can reference it directly or paste relevant
sections into your repo's instruction file for projects that enforce Storybook
by default.

### React + Storybook scaffold / convention

For React app repos with reusable components, standardize on these script names:

```json
{
  "scripts": {
    "storybook": "storybook dev -p 6006",
    "build-storybook": "storybook build",
    "test-storybook": "<your storybook test command>",
    "chromatic": "chromatic"
  }
}
```

Conventions:
- `build-storybook` is required for CI on UI changes.
- `test-storybook` should run story interaction tests and accessibility checks
  when the repo supports them.
- `chromatic` is the preferred visual regression check; Chromatic uses the
  `build-storybook` script by default.
- If the repo includes a design system, component library, or roughly `10+`
  reusable components, `chromatic` becomes required and its UI test check should
  block merges.
- In those larger UI repos, use the strongest practical coverage: visual,
  interaction, accessibility, themes, responsive states, and other key variants.
- Minimum story coverage: every shared/public component, every meaningful
  variant, and explicit empty/loading/error states when applicable.
- Bug fixes should add or update a story that captures the broken state.

## Repository contents

```
AGENTS.md                 # agent-neutral entry point
GSTACK_LITE.md            # single-file workflow reference
GSTACK_LITE_WORKFLOW.pdf  # exported workflow reference / shareable artifact
PLANNING.md               # split planning skills
REVIEW.md                 # split review skill
SHIP-RETRO.md             # split ship + retro skills
RUBRIC.md                 # split scorecard skill
gstack-lite-rubric.md     # public evaluation rubric / scorecard
gstack-lite-storybook.md  # Storybook / Chromatic companion policy
gstack-graph.mindnode     # mind map source artifact
README.md                 # setup + usage
```

## Credit

Skills adapted from [garrytan/gstack](https://github.com/garrytan/gstack) (MIT).
