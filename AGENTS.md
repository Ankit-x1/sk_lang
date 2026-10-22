## Project context

Math 3315 modeling project: Dallas Stars 2026-27 NHL season forecast
(Poisson goals for/against, Monte Carlo 82-game seasons, sensitivity and roster scenarios,
backtest on 2024-25 and 2025-26, Central Division rank translation).
Sources of truth: docs/source/proposal.md and docs/source/results-requirements.md.
Never edit docs/source/. Every numeric claim in results must come from a reproducible,
seeded, tested run. Python with uv and pytest unless an ADR says otherwise.
Domain terms live in CONTEXT.md; decisions live in docs/adr/.

## Agent skills

### Issue tracker

Issues live as markdown files under `.scratch/<feature>/`. See `docs/agents/issue-tracker.md`.

### Triage labels

Use the default labels: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix`. See `docs/agents/triage-labels.md`.

### Domain docs

Use the single-context layout. See `docs/agents/domain.md`.
