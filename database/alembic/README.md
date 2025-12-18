# Alembic Directory

This directory holds Alembic migration scripts for the database if you choose to centralize migrations in this repository.

- Place generated migration revisions inside `versions/`.
- Ensure `alembic.ini` is configured correctly and `DATABASE_URL` is set via environment variables (see `.env.example` in the database root).
- If the backend owns models, ensure Alembic's env.py knows how to import the model metadata for autogeneration.
- This scaffold is compatible with Alembic >= 1.10 and current releases.

Note: This repo provides a minimal scaffold. If your organization standardizes Alembic in the backend service, prefer keeping Alembic there and treat this directory as a template.
