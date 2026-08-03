# Deployment choices

Use this reference only after the user accepts the local workbench and asks to deploy. Re-check official pricing and limits immediately before making a recommendation; free tiers change.

## Selection

| Project | Prefer | Why | Do not use it for |
| --- | --- | --- | --- |
| Static site with browser-local data | GitHub Pages or Cloudflare Pages | Simple HTTPS hosting; no server to maintain | Centralized/private server data or API secrets |
| Small full-stack workbench with SQLite-style data | Cloudflare Pages/Workers + D1 | Pages Functions/Workers plus managed D1 SQL database | Long CPU-heavy jobs, unrestricted server filesystem, or guaranteed zero cost at any scale |
| Existing container-based application | A provider with a current free offering only after checking its official terms | May fit an existing runtime | Promising permanent free persistence without verifying it |

## Current official facts to verify

- Cloudflare Pages supports static sites and Pages Functions; its Free plan documents 500 builds per month and 100 projects per account. <https://developers.cloudflare.com/pages/> <https://developers.cloudflare.com/pages/platform/limits/>
- Workers Free has a 100,000 request/day limit and 10 ms CPU time per invocation. <https://developers.cloudflare.com/workers/platform/limits/>
- D1 is managed serverless SQL with SQLite semantics and is available on Workers Free; current Free quotas include 5 million rows read/day, 100,000 rows written/day, and 5 GB stored data. <https://developers.cloudflare.com/d1/> <https://developers.cloudflare.com/workers/platform/pricing/>
- GitHub Pages is available for public repositories on GitHub Free. <https://docs.github.com/en/pages/getting-started-with-github-pages>

## Safe deployment procedure

1. Confirm the site passed acceptance and decide whether data stays in the browser or moves to a managed database.
2. Ask the user to choose the host and authenticate themselves. Never request passwords in chat.
3. Create a deployment configuration that contains no secrets. Store runtime secrets in the provider’s secret store.
4. For Cloudflare, provision D1/schema before deploying the Worker/Pages project; retain migration files and document export/restore.
5. Build locally, deploy, open the exact production URL, and exercise the main create/read/update/delete flow on both desktop and phone widths.
6. Give the user the URL, rollback command/dashboard path, and backup instructions.

## Guardrails

- Do not deploy a local SQLite file to a stateless/serverless filesystem and describe it as durable.
- Do not create paid resources or enable paid plans without a separate, explicit user approval.
- Do not expose service tokens, database credentials, or user data in repositories, screenshots, logs, or chat.
