# Database Container

This container holds the database-related assets for the Delivery Tracker application (PostgreSQL).

Current status:
- No schema or migrations are defined in this repository yet.
- Backend container (`delivery-tracker-pro-224135-224147`) is expected to own SQLAlchemy models and generate Alembic migrations if Python/FastAPI is used.

Migration ownership:
- Alembic is intended to be driven from the backend where the SQLAlchemy models live.
- This database container provides a minimal Alembic scaffold (alembic.ini, alembic/versions/) for reference and ops alignment.
- If your team decides to centralize migrations here, you must add an alembic/env.py that imports the backend model metadata.

Recommended approach:
- Use Alembic for migrations driven from the backend repository where SQLAlchemy models live.
- Keep this `database` container for ops-ready artifacts such as Alembic config templates, migration metadata, and DB documentation.

What is included:
- `alembic.ini` (template): Minimal Alembic configuration pre-populated for PostgreSQL and compatible with recent Alembic releases.
- `alembic/` directory with `versions/` and a placeholder README.
- `.env.example`: Example environment variables required by DB-aware tooling.
- `DB_DEPENDENCY_UPDATES.md`: Notes on compatibility, pinned versions, and how to apply migrations.

Important notes:
- Do not hardcode secrets. Use environment variables.
- This repo does not apply migrations automatically. Migration execution should be orchestrated by CI/CD or backend tooling.
- Ensure DATABASE_URL is set when running Alembic (see `.env.example`).
- If the backend is not Python/SQLAlchemy-based, you can swap Alembic for your stack's native migration tool; update this folder accordingly.

Next steps (for teams using Alembic with SQLAlchemy models in backend):
1) In the backend repo, install Alembic and SQLAlchemy pinned to project standards.
2) Configure `alembic.ini` in the backend to point to the same database URL.
3) Generate an initial migration from your models:
   alembic revision --autogenerate -m "initial schema"
4) Apply migrations:
   alembic upgrade head

If you prefer to centralize migrations here, place your Alembic env.py and script location here and ensure the backend's models are importable by the Alembic env (e.g., via a shared package or codegen step).

