# Scorecard Skill

## `/scorecard` — Evaluation Mode

> *"Don't trust vibes. Score the run."*

### When to use

- after testing `gstack-lite` on a repo
- after a feature exercise or diff review
- when comparing two agents, repos, or workflow installs
- when deciding if the current setup is ready for broader adoption

### Behavior

1. **Read context.** Pull `gstack-lite-rubric.md` if present, plus `AGENTS.md`,
   `GSTACK_LITE.md`, `CLAUDE.md`, relevant diffs, and test results.
2. **Identify the target.** Are you scoring a repo install, a feature run, a
   diff, or a side-by-side agent comparison?
3. **Score each category** from **1–5** or **N/A**:
   - Setup & discoverability
   - Mode fidelity
   - Planning quality
   - Implementation discipline
   - Review sharpness
   - Ship readiness
   - Storybook / Chromatic fit (React repos only)
   - Friction & ergonomics
4. **Cite evidence for every score.** No evidence → do not score above **3**.
5. **Call out blockers separately.** Anything that would stop adoption today goes
   in a blockers section, not buried in prose.
6. **Give a clear verdict.** End with one of:
   - `Adopt now`
   - `Promising, iterate`
   - `Not ready`

### Output format

```
Overall: [X]/5 — [verdict]

Blockers:
- ...

| Category | Score | Evidence | Next action |
|---|---:|---|---|

Top 3 strengths
Top 3 gaps
Recommended next test
```

### Comparison mode

If comparing two agents or repos, produce a side-by-side score table and a short
winner summary by category.

### Rules

- Use **N/A** instead of guessing.
- Penalize friction honestly; repeated hand-holding is a real cost.
- For React design systems or component libraries, missing Storybook / Chromatic
  requirements should score poorly.
- Be specific. Evidence beats vibes.
