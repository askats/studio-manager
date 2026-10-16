# Studio Manager

**A studio management platform for visual artists – built with security and privacy by design.**

> 🚧 **Status:** Early development (phase 0 – foundation). Not yet in use.

Studio Manager gathers the administration of an artist's studio in one place: the image archive, inventory and consignments, the production process, sales, and bookkeeping records for the accountant. The **artwork is the central object** – images, process, location, sales and documents all connect to it.

It is built by a working painter, for daily use in the studio, and is developed in the open as a learning and portfolio project in software development and cybersecurity.

---

## The problem

- **Bookkeeping** – receipts are scanned, emailed and typed into a spreadsheet by hand before going to the accountant.
- **Scattered material** – images, process documentation and the whereabouts of works are spread across devices and folders, which makes grant applications and exhibition requests slow.
- **Existing tools** are either expensive and gallery-centred, US-focused, or treat the artist as a guest in the gallery's system. None of them combine process data, Swedish bookkeeping rules, automatic image variants and an equal artist–gallery workspace.

## Modules

| Module | Purpose | Status |
|---|---|---|
| **Works registry** | Single source of truth for every work: title, year, dimensions, medium, work number | Planned |
| **Process** | Timeline from first sketch to finished work; time per work, production rate | Planned |
| **Receipts & records** | Photo of receipt → structured record → monthly overview → export to accountant (SIE / Excel) | Planned |
| **Inventory** | Status (studio, consignment, sold, on loan), location, history, consignment reminders | Planned |
| **Archive** | One master image per work → automatic variants (print, web, application ≤ 2 MB) | Planned |
| **Sales** | Clients, invoices and a transparent breakdown: price → gallery share → VAT → artist's share | Planned |
| **Gallery rooms** | Shared, offline-capable workspace for planning exhibitions with galleries | Future |

## Roadmap

Small, usable releases – each one is used in the studio before the next is built.

| Version | Goal |
|---|---|
| **0 – Foundation** | Repository, documentation, threat model, app skeleton, sign-in, deployment |
| **0.1 – Works & process** | Register works; add process photos from the phone in the studio |
| **0.2 – Receipts** | Photograph and register receipts, automatic numbering, monthly overview, Excel export |
| **0.3 – Inventory** | Status, location history, consignment reminders |
| **0.4 – Archive** | Master images with automatic variants; scalable image storage |
| **0.5 – Sales** | Clients, invoices, sales breakdown |
| **0.6 – Smart receipts** | AI-assisted receipt reading, account suggestions, SIE export |
| **0.7 – Statistics** | Time per work and format, production-rate forecasts |
| **1.0 – Testers** | Accounts for fellow artists, GDPR data export and deletion |
| **Later** | Gallery rooms, offline sync, Swedish/English UI expansion |

## Principles

- **The artwork is the single source of truth.** Everything links to a work.
- **Security by design.** Decisions are evaluated against confidentiality, integrity and availability (CIA). See [SECURITY.md](SECURITY.md).
- **Privacy by design (GDPR).** Data minimisation, data stored in the EU, and the right to export and delete.
- **The accountant stays.** The platform produces complete, rule-compliant records – it is not a full accounting system.
- **Bilingual from the start.** Swedish and English, chosen by the user.
- **Free tiers first.** Paid services only when actual usage requires it.

## Tech stack

| Layer | Choice |
|---|---|
| App | [Next.js](https://nextjs.org/) with TypeScript, installable on the phone as a PWA |
| Hosting | [Vercel](https://vercel.com/) |
| Database, auth, files | [Supabase](https://supabase.com/) (PostgreSQL with Row Level Security, EU region) |
| Image archive | [Cloudflare R2](https://www.cloudflare.com/developer-platform/r2/) (when needed) |

The reasoning behind each choice is documented as Architecture Decision Records in [`docs/adr/`](docs/adr/).

## Documentation

- [SECURITY.md](SECURITY.md) – security policy and how to report a vulnerability
- [`docs/adr/`](docs/adr/) – architecture decisions
- [`docs/threat-model.md`](docs/threat-model.md) – threat model

*(Documents are added step by step as the project grows.)*

---

## På svenska

Studio Manager är en plattform för bildkonstnärers ateljéadministration: bildarkiv, inventarie, processdokumentation, försäljning och bokföringsunderlag till revisorn – med verket som det centrala objektet. Projektet byggs öppet av en verksam målare, med säkerhet och GDPR inbyggt från start, och fungerar som portfolio inom utveckling och cybersäkerhet. Gränssnittet blir valbart på svenska och engelska.

---

## Author

**Alexander Skats** – visual artist and developer, Malmö, Sweden · [github.com/askats](https://github.com/askats)

## License

© Alexander Skats. All rights reserved.
The source code is public for transparency and portfolio purposes. No licence is granted to copy, modify or distribute it. See [ADR 0002](docs/adr/0002-no-open-source-license-yet.md).