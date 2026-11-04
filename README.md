# Firecrawl web data platform

A web scraping and crawling API that converts web pages into structured data for downstream applications and agents.

## Architecture and stack

`apps/api` contains the TypeScript API, workers and job harness; Playwright handles browser rendering; Redis, RabbitMQ and NuQ PostgreSQL support processing; `apps/*-sdk` contain client SDKs. FoundationDB is an optional queue backend.

## Requirements

Docker and Docker Compose for self-hosting. Direct API development also needs Node and pnpm plus the external services used by the harness.

