# Alembic Directory

This directory holds Alembic migration scripts for the database if you choose to centralize migrations in this repository.

- Place generated migration revisions inside `versions/`.
- Ensure `alembic.ini` is configured correctly and `DATABASE_URL` is set via environment variables.
- If the backend owns models, ensure Alembic's env.py knows how to import the model metadata for autogeneration.

Note: This repo provides a minimal scaffold. If your organization standardizes Alembic in the backend service, prefer keeping Alembic there and treat this directory as a template.
