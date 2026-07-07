# Shifti — System Overview (for Claude)

This repository (`Shifti-il/General`) holds the **product specification** for Shifti. The
canonical document is [`README.md`](./README.md) — a full PRD written in **Hebrew**. This
`CLAUDE.md` is an English orientation so an AI agent can understand the system without
re-reading the whole Hebrew PRD.

> **Language:** The product (UI, copy, and — for now — this spec) is delivered **in Hebrew
> only**. RTL layout is a first-class requirement. English (LTR) is a later phase, not v1.
> When generating product-facing text, write it in Hebrew.

## What Shifti is

Shifti is a workforce-management app for small-to-medium businesses (5–100 staff on
shifts: restaurants, cafés, retail, call centers, security, etc.). Its core is a **smart
shift scheduler**: staff submit availability and constraints, the manager defines the
week's staffing needs, and the system builds a roster that satisfies every rule — skills,
skill tiers, labor rules, and personal constraints. Around scheduling it adds GPS-based
time-clock, tracking/statistics, in-org messaging, and staff-to-staff shift swaps.

## Key concepts (glossary)

- **Shift (משמרת)** — a time span the employer must staff with required roles.
- **Fixed shift (משמרת קבועה)** — fixed daily times (e.g. morning 08:00–14:00).
- **Sliding window (חלון הזזה)** — flexible demand: staff N people in given roles across a
  window; the system picks actual in/out times so the window is covered.
- **Role (תפקיד)** — a job function (bartender, waiter, cook, shift-lead). A worker may be
  qualified for several.
- **Tier / competency (דרג)** — skill level of a worker in a role. Drives staffing
  requirements ("this shift needs tier ≥ 2") and swaps ("only someone at my tier or above").
- **Constraint (אילוץ)** — personal, interpersonal ("A can't work with B"), or legal (rest
  between shifts).
- **Submission (הגשה)** — a worker's availability/shift request for a given week.
- **Preset (פריסט)** — a saved template of a shift, a week, or a worker's standing submission.

## Personas

- **Manager (מנהל)** — business owner / ops manager. **Also a worker** in the org: gets
  scheduled and submits like anyone else.
- **Worker (עובד)** — joins by manager invite. May belong to more than one workspace; the
  app supports **switching between workspaces**.

## Scheduler — hard rules (must always hold)

1. A worker is scheduled only into shifts they submitted / declared available for.
2. Only into a role they're qualified for, at a tier meeting the shift's requirement.
3. No exceeding max hours/day and no violating minimum rest between shifts.
4. Respect personal and interpersonal constraints.
5. No double-booking the same slot in the same shift.
6. Sliding windows: fully cover the window at the required count and tier.
7. Manual manager edits always win — but the system flags any rule violation.

## Manager environment

Week setup (which shifts, hours, headcount per role, required tier; fixed + sliding);
staff management (invite, set tiers, standing constraints); org management (roles, tier
meanings, presets); staffing rules; automatic roster build + manual edit + publish;
attendance override; tracking/alerts/anomalies; messaging + swap approval. Screens: Today,
My Staff, My Org, Tracking, Current Week, Next Week, Swaps popup.

## Worker environment

Submit availability/shifts (with draft + standing-order preset); 1:1 swaps subject to tier
and manager approval; GPS time-clock; personal tracking (hours, estimated pay, history);
messaging (contact manager, staff list → phone/WhatsApp/chat). Screens: Home/Today,
Schedule, Submit, Messages, Staff, Tracking.

## Open questions (from the PRD, still undecided)

Free chat vs. WhatsApp/phone hand-off · pricing model · sliding-window auto-timing vs.
manager approval · swap auto-approval at equal tier · source of hourly rate for pay calc ·
exact anomaly definitions.

## Not in v1 (proposed)

Full payroll reports / payroll-software integration · built-in chat (phase 1 = hand off to
phone/WhatsApp) · multi-language (English is phase 2 — **v1 is Hebrew only**).

## Related

A working code sketch of this system lives in a sibling `Shifti/` project (React + Vite
frontend, Node + Express + Prisma backend, PostgreSQL, Claude-based scheduler with a greedy
fallback). This repo is spec-only; keep the PRD (`README.md`) as the source of truth for
product decisions.
