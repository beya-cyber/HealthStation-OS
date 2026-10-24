# HealthStation OS (H-OS)
**A Community Digital Health & Mental Wellness Platform for Ethiopia**

Built by Behailu Kelemework (Tazi Tech Solution). 

## Why this matters for young Ethiopians
Young Ethiopians—especially young women—avoid seeking care for sexual and reproductive health (SRHR), gender-based violence (GBV), and mental health because the current paper-based clinic system offers no privacy. A young person cannot risk being seen in a crowded public queue. 

HealthStation OS is a fully built, offline-first health management platform designed to solve this. It provides a **confidential digital gateway** for youth: USSD booking (`*801#`) on any feature phone, clinical triage, encrypted patient history, and a payment-locked pharmacy. Data stays on local servers (data sovereignty), ensuring absolute privacy.

## Core Features
- **Citizen Portal & USSD Booking:** Book a spot via web or `*801#` in Amharic without internet.
- **Clinical Triage:** Replaces manual queues with RED/YELLOW/GREEN urgency sorting.
- **Digital Patient Identity:** No paper card required. Patients are found by name, phone, or Fayda ID.
- **Tena Medihin (CBHI) Integration:** Handles 90/10 insurance splits automatically.
- **Audited Pharmacy:** Prescriptions are checked against 130 drug interactions and locked until payment is captured.
- **Strict Privacy:** Role-Based Access Control means registrars and pharmacists cannot read sensitive doctor's notes.

## Architecture & Security
Built as an enterprise-grade system:
- **Offline-First:** Designed to run on a local edge server inside the Woreda health office.
- **Tenant Isolation:** PostgreSQL Row Level Security (RLS) forced on every clinical table.
- **Field Encryption:** Clinical notes are AES-256-GCM encrypted with patient-bound AAD.
- **Identity:** Staff PINs and Fayda FINs are Argon2id-hashed.
- **Audit Trail:** Append-only clinical audit logs at the database privilege level.
- **Integrations:** Telebirr, M-Pesa, EthSwitch, MoR ETR fiscal invoicing, and DHIS2 aggregate reporting.

## Tech Stack
- **Frontend:** React, Tailwind, Vite (apps/web)
- **Backend:** Fastify, Node.js (apps/api)
- **Database:** PostgreSQL 16
- **Shared:** Zod schemas, Ethiopic/Gregorian calendar engine (packages/shared)

## Local Setup
Run the full stack with Docker:
```bash
node scripts/gen-env.mjs            # generates both .env files with random secrets
docker compose up --build
docker compose run --rm migrate pnpm --filter @hos/api seed:demo
