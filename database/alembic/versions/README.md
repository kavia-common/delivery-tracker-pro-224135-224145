# Alembic Versions Directory

This directory will contain Alembic migration scripts (revision files) if you choose to centralize and run migrations from this repository.

Notes:
- Compatible with Alembic >= 1.10 and current releases.
- Ensure `alembic.ini` points `script_location` to `alembic` and this directory is discovered as `alembic/versions`.
- Do not commit secrets. Database connections should be provided via the `DATABASE_URL` environment variable.
- If your models live in the backend, create `alembic/env.py` to import the backend model metadata for autogenerate.
