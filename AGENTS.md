# AGENTS.md

This repository is **agent-agnostic first** and **Claude-compatible second**.

Use it as a portable workflow pack for coding agents that can read Markdown
instructions. Claude Code can additionally package the split docs as native
slash-command skills, but that is an adapter layer — not the core of the repo.

## Primary docs

- `GSTACK_LITE.md` — main planning / review / ship / retro workflow
- `gstack-lite-rubric.md` — evaluation rubric for testing repos, agents, and runs
- `gstack-lite-storybook.md` — Storybook / Chromatic policy for React repos
- `PLANNING.md` — split planning docs
- `REVIEW.md` — split review docs
- `SHIP-RETRO.md` — split ship + retro docs
- `RUBRIC.md` — split scorecard skill

## How any coding agent should use this repo

1. Read `GSTACK_LITE.md` before non-trivial work.
2. If the project is a React app with reusable UI components, also read
   `gstack-lite-storybook.md`.
3. If you are evaluating the workflow or comparing agents, also read
   `gstack-lite-rubric.md`.
4. Treat the slash-command names in `GSTACK_LITE.md` as **mode labels**, not as
   a requirement for a specific tool.
5. If your agent does not support slash commands, invoke the modes with plain
   English prompts.

## Mode map

- `plan-ceo-review` → founder/product reframing mode
- `plan-eng-review` → engineering planning and architecture mode
- `review` → paranoid pre-ship review mode
- `ship` → release execution mode
- `retro` → retrospective / metrics mode
- `scorecard` → structured evaluation / comparison mode

## Plain-language invocation examples

- "Use founder mode from `GSTACK_LITE.md` to reframe this feature request."
- "Use eng review mode from `GSTACK_LITE.md` and produce architecture, failure
  modes, and a test matrix."
- "Use review mode from `GSTACK_LITE.md` on this diff."
- "Use `gstack-lite-rubric.md` to score this repo test run."

## Claude Code adapter

If you want native Claude-style slash-command packaging in a consuming repo:

- copy `PLANNING.md`, `REVIEW.md`, `SHIP-RETRO.md`, and `RUBRIC.md` into `.claude/skills/`
- paste or adapt relevant sections from `GSTACK_LITE.md` into `CLAUDE.md`
- for React repos, also paste or reference `gstack-lite-storybook.md`
- if you want structured evaluations, also paste or reference `gstack-lite-rubric.md`

## Philosophy

The workflow rules are the product. Agent-specific packaging is just a delivery
mechanism.

<!-- nx configuration start-->
<!-- Leave the start & end comments to automatically receive updates. -->

# General Guidelines for working with Nx

- When running tasks (for example build, lint, test, e2e, etc.), always prefer running the task through `nx` (i.e. `nx run`, `nx run-many`, `nx affected`) instead of using the underlying tooling directly
- You have access to the Nx MCP server and its tools, use them to help the user
- When answering questions about the repository, use the `nx_workspace` tool first to gain an understanding of the workspace architecture where applicable.
- When working in individual projects, use the `nx_project_details` mcp tool to analyze and understand the specific project structure and dependencies
- For questions around nx configuration, best practices or if you're unsure, use the `nx_docs` tool to get relevant, up-to-date docs. Always use this instead of assuming things about nx configuration
- If the user needs help with an Nx configuration or project graph error, use the `nx_workspace` tool to get any errors

<!-- nx configuration end-->

