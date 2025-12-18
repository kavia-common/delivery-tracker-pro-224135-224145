# DB Dependency Updates

Purpose: Track database tooling and dependency decisions for the Delivery Tracker project.

Current stack:
- Database: PostgreSQL (external service or containerized)
- Migration tooling: Alembic (recommended when using Python/FastAPI backend with SQLAlchemy models)

Status:
- No schema defined in this repository yet.
- Minimal Alembic scaffolding has been added to this `database/` container for future use if you centralize migrations here.
- If your backend (`delivery-tracker_backend`) manages SQLAlchemy models, it is recommended to keep Alembic migrations in the backend repository.

Environment variables:
- DATABASE_URL: Required when running Alembic or other DB tooling from this repository (see `.env.example`).

Pinned versions (tooling recommendations):
- Alembic: 1.13.2
- SQLAlchemy: 2.0.36
- psycopg (psycopg3): 3.2.3  (recommended)
- OR psycopg2-binary: 2.9.10 (only if psycopg3 is not feasible)
Notes:
- Alembic 1.13+ works seamlessly with SQLAlchemy 2.x.
- For psycopg3, use URL scheme postgresql+psycopg://...; for psycopg2, use postgresql+psycopg2://...

Compatibility and notes:
- PostgreSQL 12+ recommended. Ensure psycopg2/psycopg (as required by the backend) are pinned according to backend's `requirements.txt`.
- This repository does not perform migrations automatically.
- When generating migrations with Alembic using autogenerate, ensure the model metadata is importable from the Alembic environment (`env.py`), typically residing in the backend codebase.
- `alembic.ini` here is compatible with Alembic >= 1.10 and current releases; `version_path_separator = os` is supported and sets OS-specific paths.

Backend coordination:
- Alembic is intended to be driven from the backend repository where models live.
- Ensure backend DEPENDENCY_UPDATES.md references these DB tooling versions and notes.
- If centralizing migrations here, create `database/alembic/env.py` that imports backend metadata and respects `DATABASE_URL`.

Next steps for teams:
- Decide whether migrations are centralized here or in the backend.
- If centralized here, add an `env.py` under `database/alembic` that imports the backend models' metadata, and add the backend path to `sys.path` in `env.py` if needed.
- Keep this document updated when versions or tooling choices change.
