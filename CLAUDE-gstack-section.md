## gstack Skills

Lightweight planning, review, and release workflow skills.
Skill files live in `.claude/skills/`.

### Available Skills

| Command | File | Mode |
|---|---|---|
| `/plan-ceo-review` | `.claude/skills/PLANNING.md` | Founder — rethink the problem, find the 10-star product |
| `/plan-eng-review` | `.claude/skills/PLANNING.md` | Eng manager — architecture, diagrams, failure modes |
| `/review` | `.claude/skills/REVIEW.md` | Paranoid staff engineer — structural audit, not style |
| `/ship` | `.claude/skills/SHIP-RETRO.md` | Release engineer — sync, test, push, PR |
| `/retro` | `.claude/skills/SHIP-RETRO.md` | Eng manager — git-based team retrospective |

### Workflow Order

```
/plan-ceo-review  →  /plan-eng-review  →  [implement]  →  /review  →  /ship
```

Always run CEO review before Eng review. Never jump straight to architecture.
`/ship` is for a ready branch only — not for deciding what to build.

### Rules

- `/plan-ceo-review` must challenge the literal request before scoping work
- `/plan-eng-review` must produce at minimum an architecture diagram + data flow diagram
- `/review` findings must be classified: CRITICAL / HIGH / MEDIUM / LOW
- `/ship` runs non-interactively: sync → test → lint → tsc → push → PR
- CRITICAL review findings block `/ship`
- Tests run with `npm test -- --runInBand` unless CLAUDE.md specifies otherwise
