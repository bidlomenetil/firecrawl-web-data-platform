# Firecrawl web data platform

A web scraping and crawling API that converts web pages into structured data for downstream applications and agents.

## Architecture and stack

`apps/api` contains the TypeScript API, workers and job harness; Playwright handles browser rendering; Redis, RabbitMQ and NuQ PostgreSQL support processing; `apps/*-sdk` contain client SDKs. FoundationDB is an optional queue backend.

## Requirements

Docker and Docker Compose for self-hosting. Direct API development also needs Node and pnpm plus the external services used by the harness.

## Installation and local development

Start with the checked-in [self-hosting guide](SELF_HOST.md). The matching local stack is:

```sh
docker compose -f docker-compose.yaml config --quiet
docker compose -f docker-compose.yaml up --build
```

The API is published on port 3002 by the root Compose file.

## Configuration

Root `.env` only overrides variables referenced in `docker-compose.yaml`; `apps/api/.env.example` is a separate contract. Default API authentication is disabled. Configure authentication before exposure, and do not publish dependency ports. AI features require a separately configured provider.

## Testing

For source tests, work in `apps/api`, install dependencies from its lockfile, and use `pnpm harness pnpm exec vitest run <test-file>` as required by `AGENTS.md`. The harness provides services; running Vitest alone is insufficient for end-to-end tests.

## Deployment and integrations

`SELF_HOST.md` documents missing persistence and production decisions in the baseline Compose stack. Add backup/restore and access control before production. SDK packages show API integrations.

## Source provenance and license

This repository imports source from [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl). Original product functionality belongs to its upstream contributors. The local history begins with a November 2026 source snapshot; it does not retain upstream development history or prove the exact upstream revision. GitHub reports the upstream repository was created on 2024-04-15; that is repository-origin evidence, not the date of this contribution. Existing year folders are retained as local organization.

Preserve `LICENSE` and existing third-party notices when redistributing. Missing root license text was recovered from the upstream repository during this maintenance pass; existing license files were preserved.

## Validation status

Setup and test commands above were checked against this checkout’s manifests, scripts and entry points. Full dependency installation, application builds and integration tests were not performed in this maintenance pass. The API dependencies and browser/database/queue service stack were not provisioned. These instructions identify the supported workflow without claiming a successful product build.

See [source provenance](SOURCE_PROVENANCE.md) for pinned upstream license retrieval evidence and redistribution limitations.
