# Security Policy

## Supported versions

Until the framework reaches `1.0.0`, only the latest minor release of each project receives security fixes. After `1.0.0`, the two most recent minor releases will be supported.

## Reporting a vulnerability

**Do not open a public issue.** Report vulnerabilities privately via one of:

1. **GitHub Security Advisories** — preferred. Open a draft advisory in the affected repository:
   `https://github.com/phronesis-framework/<repo>/security/advisories/new`
2. **Email** — `security@phronesis-framework.dev` (or `edumarreroglezz@gmail.com` until the mailbox is provisioned). PGP key on request.

When reporting, please include:

- A description of the vulnerability and its potential impact.
- Steps to reproduce, or a minimal proof-of-concept.
- The affected versions and any known mitigations.
- Your name and how you would like to be credited (or anonymous).

## What to expect

- **Acknowledgement** within 72 hours of report.
- **Initial triage** within one week, including a CVSS estimate.
- **Fix and coordinated disclosure** on a timeline proportional to severity:
  - Critical/High: targeted same-week patch release.
  - Medium: next regular minor release.
  - Low: next regular minor or as part of normal hardening.

We do not currently run a paid bug-bounty program, but we credit reporters in release notes unless anonymity is requested.

## Scope

In scope:

- Any code in repositories under the `phronesis-framework` organization.
- Workflows and actions in `phronesis-framework/.github` that downstream repos consume.

Out of scope:

- Third-party dependencies (report upstream; we will track and patch).
- Documentation typos that have no security implication.
- Social-engineering or physical-security findings.
