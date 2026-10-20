# BacMR

**AI tutor for Mauritania's national baccalaureate.** A student asks a question in Arabic, French or English and gets a grounded, Socratic answer with citations into the official curriculum. Built by Lebjawi Tech.

## How the platform is organised (since 2026-10-20)

One repo per deployable. Every client talks only to the gateway.

| Repo | Role |
|---|---|
| [`api-gateway`](https://github.com/BacMR/api-gateway) | **The only public API** (`api.bacmr.com`): auth with Zitadel, wallets and billing, admin operations, rate limits. Calls tutor and knowledge on the VPS network. |
| [`tutor`](https://github.com/BacMR/tutor) | Turns a question into a streamed answer: understanding, evidence from knowledge, prompt assembly, sufficiency check. Owns the `tutor` schema. |
| [`knowledge`](https://github.com/BacMR/knowledge) | Curriculum ingestion (parse, figures, chunk, enrich, embed, QA gate) and retrieval (hybrid lanes, fusion, rerank). Owns the `content` schema. |
| [`scraper-worker`](https://github.com/BacMR/scraper-worker) | Pulls curriculum PDFs from the government site into the ingestion queue. |
| [`bridge`](https://github.com/BacMR/bridge) | Optional Claude-subscription shim for LiteLLM. Off by default, never on the student path. |
| [`py-common`](https://github.com/BacMR/py-common) | Shared Python library (settings, DB, LiteLLM client, events), versioned by git tag. |
| [`infra`](https://github.com/BacMR/infra) | LiteLLM, Zitadel, RabbitMQ, backups, nginx vhost templates, Postgres provisioning. |
| [`db-migrations`](https://github.com/BacMR/db-migrations) | The single Flyway home for every schema lineage. |
| [`evals`](https://github.com/BacMR/evals) | ragloop (adversarial tutor evals), promptfoo gates, the retrieval bench and golden set. |
| [`web-platform`](https://github.com/BacMR/web-platform) | Admin dashboard (`admin.bacmr.com`). |
| [`landing-site`](https://github.com/BacMR/landing-site) | `bacmr.com` and its `/chat`. |
| [`mobile-app`](https://github.com/BacMR/mobile-app) | The Flutter app, the primary student interface. |
| [`docs`](https://github.com/BacMR/docs) | Architecture, ADRs, runbooks, studies, the `docs.bacmr.com` site, and cross-cutting roadmap issues. |
| [`github-security-workflows`](https://github.com/BacMR/github-security-workflows) | The reusable PR Security Gate and the daily org scan. |
| `.github` (this repo) | Org profile, workflow templates, security policy. |

Archived, read-only, never edited: `archive-backend` (the 2026 monolith the services were extracted from) and `archive-rag-engine` (the first RAG engine).

## How work happens

- **Roadmap:** the [Production Road Map](https://github.com/orgs/BacMR/projects/1) project board. Every finished step is logged on its item with the PR link and the decision taken.
- **Decisions:** Architecture Decision Records in [`docs/adr`](https://github.com/BacMR/docs).
- **Branches:** `dev` is the default and the deploy trigger in every service and app repo; feature branches branch off `dev` and merge back by PR. `main` is reserved for production. Org-meta repos (`.github`, `github-security-workflows`) use `main` because they are not deployed.
- **Every PR** passes the `security / Security Gate` check (Gitleaks, Trivy, Semgrep; new findings block). The org ruleset enforces PRs and the gate on `dev` and `main` in all repos.
- **Secrets** live only in Infisical; nothing secret is stored in GitHub.

## Security

Report a vulnerability privately as described in [SECURITY.md](../SECURITY.md). Please do not open a public issue for security problems.
