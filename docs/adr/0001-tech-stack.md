# ADR 0001: Tech stack – Next.js, Supabase, Vercel and Cloudflare R2

- **Status:** Accepted
- **Date:** 2026-10-16

## Context

Studio Manager starts with one user (the author) but must grow to several artists and, later, shared rooms where an artist and a gallery work on the same data. The data is relational: works have process images, inventory history and sales; sales link to clients; receipts need sequential numbering. Bookkeeping data and client data require strict access control and EU storage (GDPR). The author is a beginner developer, and the project should run on free tiers as long as possible. The image archive is estimated at 50–100 GB over time.

## Decision

| Layer | Choice |
|---|---|
| Application | **Next.js** with **TypeScript**, delivered as an installable web app (PWA) |
| Hosting | **Vercel** |
| Database, authentication, file storage | **Supabase** – PostgreSQL in an EU region, with Row Level Security |
| Image archive (when needed) | **Cloudflare R2** with EU jurisdiction |
| Code, documentation, automation | **GitHub** |

## Alternatives considered

**Supabase + SvelteKit.** Same backend, simpler front-end syntax. Rejected because the ecosystem, documentation and examples are smaller, which matters for a beginner.

**Firebase (Google).** Good documentation, but a document database fits relational bookkeeping and artwork data poorly, its security rules are easier to get wrong, and file storage now requires a paid plan.

## Consequences

**Positive**
- **Row Level Security** lets the database itself enforce who can see each row – the key requirement for multiple users and shared rooms. *(Confidentiality)*
- PostgreSQL is an open standard and Supabase is open source, so data and schema can be moved to another host. *(Availability – exit strategy)*
- Sign-in is handled by a maintained service rather than custom code. *(Confidentiality, integrity)*
- TypeScript catches many errors before the code runs. *(Integrity)*
- Image storage scales almost linearly in cost; most of the archive stays free or close to it.

**Negative / risks**
- Several services and accounts to manage – each must use two-factor authentication.
- Supabase free tier: 500 MB database, 1 GB file storage, no automatic backups, and projects pause after a week of inactivity. Own backups must be built early. *(Availability)*
- Vercel's free tier is for non-commercial use. A paid plan or another host is needed if the project becomes a paid service.
- Supabase, Vercel and Cloudflare are US companies, even when data is stored in the EU. Data processing agreements and transfer mechanisms must be documented. *(GDPR)*
- Next.js has a learning curve, especially the split between server and client code.

## Review

Revisit when the free tiers are exceeded, before onboarding test users (v1.0), and before any commercial launch.