# Security Policy

Studio Manager will handle business records, client data and unpublished artwork. Security and privacy are treated as core requirements, not add-ons. Decisions are evaluated against **confidentiality, integrity and availability (CIA)**.

> **Project status:** Early development. No production deployment and no real user data yet.

## Reporting a vulnerability

**Please do not open a public issue for security problems.**

Report vulnerabilities privately through GitHub:
**Security** tab → **Report a vulnerability** (private vulnerability reporting is enabled).

Please include a description, steps to reproduce and the potential impact. This is a single-maintainer project: reports are acknowledged on a best-effort basis, normally within 7 days.

## Principles

- **Security by design** – controls are planned before features are built.
- **Least privilege** – every user, key and service gets only the access it needs.
- **Defence in depth** – no single control is trusted to stop an attack on its own.
- **Data minimisation (GDPR)** – collect only what is needed; store it in the EU.
- **Kerckhoffs's principle** – the system must stay secure even though the source code is public. Secrets protect the system, not obscurity.

## Controls in place

### Account & access
| Control | Protects |
|---|---|
| Two-factor authentication on the GitHub account | Confidentiality, integrity |
| SSH key authentication (Ed25519, passphrase-protected, one key per device) | Confidentiality, integrity |
| Recovery codes stored offline in a password manager | Availability |

### Repository
| Control | Protects |
|---|---|
| Commits use a GitHub no-reply address; pushes exposing a private email are blocked | Confidentiality (personal data) |
| Secret scanning and **push protection** enabled | Confidentiality |
| Dependabot alerts, security updates and malware alerts enabled | Integrity |
| Private vulnerability reporting enabled | Confidentiality |
| `.gitignore` blocks environment files, keys and business data (receipts, SIE/Excel exports) | Confidentiality |
| Global ignore of macOS `.DS_Store` metadata files | Confidentiality |

## Planned controls

These are commitments for upcoming phases and will move to *Controls in place* when implemented.

- **Row Level Security** on every database table – users can only read and write their own rows, enforced by the database itself.
- **Secrets only in environment variables** – local `.env` files (ignored by Git) and the hosting provider's encrypted settings. Admin keys never reach the browser.
- **EU data residency** – database and file storage in EU regions; data processing agreements with each provider documented.
- **Multi-factor authentication** for app sign-in.
- **Automated backups** independent of the database provider, with tested restore.
- **Tamper-evident bookkeeping records** – sequential numbering and no silent edits, in line with the Swedish Bookkeeping Act (*bokföringslagen*).
- **GDPR rights** – data export and deletion for every user.
- **CodeQL code scanning** once application code exists.
- **Threat model** – see `docs/threat-model.md`.

## If a secret is ever leaked

1. **Revoke or rotate the secret immediately** at the provider. This is the only step that actually removes the risk.
2. Then remove it from the code and history.
3. Review access logs for misuse and document the incident.

Deleting a commit is *not* enough – once a secret has been pushed to a public repository it must be considered compromised.