# AGENTS.md — BacMR/.github (org meta repo)

This file is the single agent guide for the repo. See `README.md` for the summary.

## What this repo holds

- `profile/README.md` — the org profile shown at https://github.com/BacMR (platform
  summary, repo map, how work happens).
- `workflow-templates/` — starters offered on the Actions "New workflow" page of every
  BacMR repo (`<name>.yml` + `<name>.properties.json`).
- `SECURITY.md` — org-wide vulnerability reporting policy (default for repos without one).
- `.github/workflows/pr-security.yml` — this repo's own security gate;
  `.github/dependabot.yml` — monthly grouped github-actions updates.

## Ground rules

- **Default branch `main`** (not deployed). Feature branches (`feat/…`, `fix/…`,
  `docs/…`, `chore/…`) off `main`; PR into `main`; never push directly (org ruleset).
  Conventional Commits; commits end with the `Co-Authored-By` trailer.
- The PR must pass `security / Security Gate`. No secrets in this repo.
- Project secrets (where a repo has any) live in Infisical `bacmr-<repo>`; this repo has none.

## Keep the repo map current

The profile's repo map must match the real org. When a repo is created, renamed,
archived or changes role, update `profile/README.md` (and the project map in the
workspace `CLAUDE.md`/docs) in the same session. Verify against the org:
`gh repo list BacMR --limit 100 --json name,isArchived,defaultBranchRef`.

## Adding a workflow template

1. Add `workflow-templates/<name>.yml` and `workflow-templates/<name>.properties.json`
   (`name`, `description`, `categories`; optional `iconName`, `filePatterns`).
2. Templates call reusable workflows at `@main` of the provider repo (as
   `pr-security.yml` does for `BacMR/github-security-workflows`); never inline logic.
3. Pin any third-party action in a template to a full commit SHA with a version comment.
4. Mention the template in `README.md`, open a PR and let the gate pass. Templates are
   offered org-wide on merge; existing repos are not changed automatically.
