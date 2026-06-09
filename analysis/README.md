# PolyBazar Analysis

## Summary
PolyBazar is a multi-service marketplace platform with three main runtime components:
- Frontend: Next.js app in `frontend`
- Backend: Spring Boot API in `backend`
- ML Service: FastAPI service in `ml-service`

The project has good foundations (Dockerfiles, Compose, service separation), but core documentation was inconsistent with the actual repository state.

## What Was Improved
- Added this analysis folder to capture project-level documentation health and architecture findings.
- Identified README inconsistencies and replaced them with verified instructions.

## Key Findings
1. Documentation drift existed.
- Root README referenced paths and files not present in repository (`docs/`, `render.yaml`, `database/`, `ml-services/`).

2. Run instructions were incomplete for day-to-day development.
- No clear dedicated section for running frontend alone.
- No clear dedicated section for running backend alone.

3. Deployment guidance was too high-level.
- Render deployment was not actionable for manual setup.

## Current Architecture (Verified)
- `frontend` calls backend API via `NEXT_PUBLIC_API_URL`.
- `backend` exposes API on port 8080 and depends on PostgreSQL, MongoDB, Redis, and optional ML service URL.
- `ml-service` exposes FastAPI on port 8000.
- Local orchestration is available through `docker-compose.yml`.

## Recommendations
1. Keep root README synchronized with actual directory names whenever folders are renamed.
2. Add service-specific READMEs under `frontend/`, `backend/`, and `ml-service/` for deeper setup details.
3. Add a checked-in Render blueprint file only if maintained alongside code changes.
4. Add a CI doc check that validates links to local files to prevent README drift.

## Known Follow-Up Opportunity
- `docker-compose.yml` references `./ml-services` while the repository folder is `ml-service`.
  This likely breaks local compose startup for ML service and should be corrected in a follow-up change.
