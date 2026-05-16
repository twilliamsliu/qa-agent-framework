# Security Policy

## Scope of this repository

This repository (the **L1 layer** in the framework's terminology) contains documentation only. It is intentionally scrubbed of any organization-specific configuration, credentials, or operational data. There are no secrets to leak from this repo itself.

If you adopt this framework, please follow the **Layer E** separation:

- **L1 (this repo)** — Shareable framework documentation. Safe to fork, share, or publish.
- **L2** — Organization-private configuration. Keep in a private repo.
- **L3** — Local-only secrets (credentials, tokens, OAuth). Never commit. `.gitignore` + pre-commit hooks as dual protection.

Mechanical separation is the only reliable protection. Prompt-level discipline alone will fail eventually.

## Reporting a vulnerability

If you discover a security issue in:

- This documentation (e.g., an example pattern that would leak data if followed literally), or
- A linked artifact (blog post, example snippet) under the same author,

please report it privately rather than opening a public issue.

**Contact:** [twilliamsliu@gmail.com](mailto:twilliamsliu@gmail.com)

Please include:

1. A description of the issue and its potential impact.
2. Steps to reproduce, if applicable.
3. Whether you would like to be credited in any subsequent fix or disclosure.

I will acknowledge receipt within a few business days and work with you on a coordinated disclosure timeline.

## Out of scope

- Vulnerabilities in third-party tools mentioned in this documentation (Jira, MeterSphere, Slack, Google Drive, etc.) — please report those to the respective vendors.
- General questions about the framework — please open a GitHub Discussion or Issue instead.

## Acknowledgement

This security policy exists because the framework explicitly addresses secret handling (Layer E). It would be incongruent to publish a framework about secret discipline without offering a clear channel for security feedback.
