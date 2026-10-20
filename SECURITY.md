# Security policy

## Reporting a vulnerability

Please report security issues **privately**, not in a public issue or pull request.

- Preferred: GitHub private vulnerability reporting on the affected repository ("Report a vulnerability" under the Security tab), or on this repository if unsure which one applies.
- Alternative: email the maintainer listed on the organization profile.

We acknowledge reports within 3 working days and keep you informed until the issue is resolved. Please include steps to reproduce and the affected component (API, admin dashboard, website, mobile app, ingestion).

## Scope

- Production hosts: `api.bacmr.com`, `admin.bacmr.com`, `bacmr.com`, `zitadel.bacmr.com`, the mobile app.
- In scope: authentication and authorisation, data exposure (student data, curriculum content), injection, secrets exposure, dependency vulnerabilities with a demonstrable impact.
- Out of scope: denial of service, reports from automated scanners without a demonstrated impact, social engineering, physical attacks.

## What we do on our side

- Every pull request in every repository runs the org **Security Gate** (Gitleaks for secrets, Trivy for dependencies and OS packages, Semgrep for static analysis); new findings block the merge.
- A daily scan of every non-archived repository runs on our own runner and keeps a history of findings.
- Secrets are never stored in the repositories or in GitHub Actions; they live in a self-hosted secrets manager and are rendered on the server at deploy time.
- Dependabot is enabled on every repository.

Thank you for helping keep BacMR's students safe.
