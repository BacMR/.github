# BacMR/.github

The organization's meta repository. It holds:

- `profile/README.md` — the org profile shown at https://github.com/BacMR (what the platform is, the repo map, how work happens).
- `workflow-templates/` — workflow starters offered in the Actions "New workflow" page for every BacMR repo. Today: **BacMR PR Security Gate** (`pr-security.yml`), which calls `BacMR/github-security-workflows/.github/workflows/security-scan.yml@main` on every pull request.
- `SECURITY.md` — the org-wide vulnerability reporting policy (GitHub surfaces it in every repo that has none of its own).

Conventions: default branch `main` (this repo is not deployed); changes by PR; the org ruleset applies. Keep the repo map in the profile in step with the actual org — when a repo is created, renamed or archived, update it in the same session.
