# gstack-lite — Evaluation Rubric

Use this doc to score a `gstack-lite` run on a sample repo, an existing repo,
or across multiple agents. It is intentionally **agent-agnostic**.

## When to use

- after a real feature exercise
- after installing slash-command adapters in Claude Code
- when comparing two agents on the same repo/task
- when deciding whether a repo is ready to adopt `gstack-lite`

## Scoring scale

- **5 — Excellent:** strong, low-friction, production-usable
- **4 — Strong:** good enough to adopt, minor gaps only
- **3 — Acceptable:** useful, but needs iteration
- **2 — Weak:** works inconsistently or misses important behaviors
- **1 — Broken:** not trustworthy yet
- **N/A:** not exercised in this test run

Use **N/A** instead of guessing. Exclude `N/A` categories from the average.

## Categories

### 1. Setup & discoverability
- Were the docs or skills easy to install?
- Could the agent find the right entry points quickly?
- If Claude slash commands were installed, were they actually available?

### 2. Mode fidelity
- Did the modes behave distinctly?
- Did planning feel different from review, ship, and scorecard?
- Did the agent follow the intended purpose of each mode?

### 3. Planning quality
- Did product framing improve after founder mode?
- Did eng review produce architecture, failure modes, and a test matrix?
- Were real constraints and trust boundaries surfaced?

### 4. Implementation discipline
- Did the agent stay within scope?
- Did it update tests, docs, or stories where appropriate?
- Did it avoid inventing unnecessary work?

### 5. Review sharpness
- Did review catch real bugs, regressions, or gaps?
- Did it go beyond style nits?
- Did it explain why issues mattered?

### 6. Ship readiness
- Did ship mode verify the right checks?
- Did it ask for the right release/PR evidence?
- Did it avoid making unsafe assumptions?

### 7. Storybook / Chromatic fit (React repos only)
- Did the agent correctly decide whether Storybook is required?
- Did it correctly decide whether Chromatic is required?
- Did it ask for the right story coverage and UI automation depth?

### 8. Friction & ergonomics
- How much hand-holding was required?
- Were prompts concise and reusable?
- Could a teammate repeat the workflow without heavy explanation?

## Output format

Use this table:

| Category | Score | Evidence | Next action |
|---|---:|---|---|
| Setup & discoverability | 1–5 / N/A | concrete repo evidence | fix / keep / retest |

Then summarize:

- **Average score:** `[X]/5`
- **Blockers:** what would stop adoption today?
- **Top 3 strengths**
- **Top 3 gaps**
- **Recommendation:** `Adopt now` / `Promising, iterate` / `Not ready`

## Recommendation bands

- **4.5–5.0:** Adopt now
- **3.5–4.4:** Promising, iterate on the weak spots
- **2.5–3.4:** Not ready for broad rollout
- **Below 2.5:** Rework the workflow before further testing

## Guardrails

- No evidence → do not score above **3**.
- Missing required Storybook/Chromatic behavior in a React design system should
  heavily penalize **Storybook / Chromatic fit**.
- If the test did not include implementation or shipping, mark those categories
  **N/A** instead of guessing.

## Plain-language prompts

- "Use `gstack-lite-rubric.md` to score this repo test run."
- "Compare Agent A vs Agent B using `gstack-lite-rubric.md`."
- "Score whether this repo is ready to adopt `gstack-lite` broadly."
