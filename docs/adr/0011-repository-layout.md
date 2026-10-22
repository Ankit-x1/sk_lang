# Repository Layout

Use a small `src/dallas_forecast/` package with uv configuration in `pyproject.toml`, pytest tests under `tests/`, cited source snapshots in `data/raw/`, derived datasets in `data/processed/`, and run manifests and generated results in `outputs/`. Keep domain terms in `CONTEXT.md` and decisions in `docs/adr/` so the project’s model, tests, data, and deliverables have explicit boundaries.
