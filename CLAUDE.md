# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working in this project.

## What this is

Engagement workspace for the **Coastline Retail Group internship** — a ten-week
**Data Cloud Consultant** simulation. Hemayet plays the incoming data specialist at a
fictional 62-store NSW and Victorian homewares retailer whose customers exist three
times over — once in the point of sale, once in e-commerce, once in the loyalty app —
and where nobody can answer how many customers the business actually has.

Coastline Retail Group Pty Ltd is fictional; no real customer data is in here.

**Current state: scaffold.** `force-app/`, `seed/` and `evidence/` hold only
`.gitkeep`. Nothing has been built yet.

## The org

Target org alias **`coastline`** — a Developer Edition org.

```bash
sf org display --target-org coastline
```

**Two provisioning steps block all work and must happen first** (see `README.md`):

1. **Data Cloud is not turned on.** The entitlements ship with the org (`Data Cloud`
   permission set licence, Active, 200,000) but provisioning has not run. The tell is
   `SELECT Id FROM DataspaceScope` failing with "sObject type not supported". Setup →
   Data Cloud Setup → Get Started.
2. **The org locale is US.** It provisioned as `Country: United States`,
   `LanguageLocaleKey: en_US`, unlike every other org in this program. Set Locale to
   English (Australia), Currency to AUD, Time Zone to Australia/Sydney **before
   ingesting anything** — currency and date formats propagate into the data model and
   are painful to unpick afterwards.

Do not seed, ingest or model anything until both are done. Check, don't assume.

## Known repo gap

There is **no `sfdx-project.json`** in this repo, so `sf project deploy` and
`sf project retrieve` will not work against `force-app/` until one is added. The other
Salesforce repos in this program use `packageDirectories: [{path: "force-app", default:
true}]` with `sourceApiVersion: "67.0"`. Add it before the first metadata retrieve.

## The division of labour on this engagement

**Hemayet builds all Setup configuration by hand** — data streams, data lake and data
model objects, identity resolution rulesets, calculated insights, segments, activations,
consent settings. The certification tests Setup navigation and so does the job. Do not
build config via the Metadata API on his behalf unless he asks explicitly.

**Claude does:** seed data (Apex anonymous and source files in `seed/`), including the
deliberate defects the engagement depends on; verification queries; evidence extraction;
code review; deployment mechanics; ERD and documentation drafting; and playing
stakeholders in character for discovery exercises.

## The distinction that shapes this engagement

Identity resolution is the whole point. The seeded data must contain **realistic,
deliberate duplication across three sources** — the same human as a POS record, a
web account and a loyalty member, with the mismatches that make matching hard: nicknames,
transposed address lines, a changed surname, a shared household email. Data that
resolves cleanly proves nothing.

Match rules and reconciliation rules are separate decisions and get documented
separately: matching decides *which records are the same person*, reconciliation decides
*which value wins*. Conflating them is the classic error.

## Documentation standards

`deliverables/` is the substance and the interview evidence. The configuration proves
the clicks happened; the documents prove the thinking did.

- **Every change goes in `deliverables/build-log.md`** with its date, the component, the
  change, and the requirement it traces to. Corrections are appended as new rows, never
  edited over.
- **Claim only what was verified** — a query or a screenshot backs every "verified".
- **Accepted risks are recorded, not hidden.** Where a training-org shortcut is taken,
  say what production would have required instead.
- **Dates are Australian** — `dd/mm/yyyy`.
- `evidence/` holds before/after extracts and screenshots per phase.

## Never commit

Auth files and sfdx auth URLs — an auth URL is a full credential. `.gitignore` covers
`**/*authFile*.json`, `**/*sfdxAuthUrl*`, `.env*`, `.sf/` and `.sfdx/`. A credential
that reaches git history has to be *rotated*, not deleted.

## Agent workflow

Superpowers is expected to be installed as a **user-level plugin**
(`/plugin install superpowers@claude-plugins-official`), not vendored into this repo.
There is no test runner here and most work is Setup configuration, so the red/green TDD
skills have little to bite on; the planning, verification and code-review skills apply
to the seed scripts and the written deliverables.
