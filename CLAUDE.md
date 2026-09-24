# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working in this project.

## What this is

Engagement workspace for **Coastline Retail Group** — a ten-week Data Cloud
Consultant simulation at a fictional 62-store NSW and Victorian homewares
retailer whose customers exist three times over: once in the point of sale, once
in the e-commerce platform, once in the loyalty app. Nobody can answer how many
customers the business actually has.

Week scope: source ingestion, data modelling, identity resolution, calculated
insights, segmentation, activation, consent and privacy, governance handover.

## Read this before proposing any build

**Data Cloud is not provisioned in this org.** The entitlements ship with it — the
`Data Cloud` permission set licence is Active at 200,000 — but provisioning has
never run. The tell is `SELECT Id FROM DataspaceScope` failing with "sObject type
not supported".

Provisioning is a **prerequisite, not part of the build**: Setup → Data Cloud
Setup → Get Started. Until it has run, none of the ten weeks can start, and any
plan that assumes a working dataspace is premature.

## The locale trap — fix before ingesting anything

The org provisioned as `Country: United States`, `LanguageLocaleKey: en_US`,
against an Australian scenario. Unlike the other program orgs, **this one has not
been corrected yet.**

Set Locale to English (Australia), Currency to AUD, Time Zone to Australia/Sydney
**before ingesting anything.** Currency and date formats propagate into the data
model itself, and unpicking them after ingestion is far worse than a settings
change. This is the single highest-cost mistake available in this repository.

(Instance `CAN98` is unrelated to the locale problem and is not changeable. Do not
chase it.)

## The org

Target org alias **`coastline`**, org ID `00DgL00000b5uvVUAQ`. A dedicated
Developer Edition org — the other program orgs are each allocated to a
certification track, and ingesting into any of them would pollute graded work.

```bash
sf org display --target-org coastline
sf data query --target-org coastline --query "SELECT Id FROM DataspaceScope"  # fails until provisioned
```

## The division of labour

**Hemayet builds all Setup configuration by hand** — data streams, data model
objects, mappings, identity resolution rulesets, calculated insights, segments,
activation targets. The certification tests Setup navigation and so does the job.
Do not build config via the Metadata API on his behalf unless he asks explicitly.

**Claude does:** source data generation (including its deliberate defects),
verification queries, data model and ERD drafting, documentation, build-log
entries, code review, and playing stakeholders in character for discovery
exercises.

## The distinction that shapes this engagement

The premise is that the **same customer appears three times across three systems**.
That means the interesting work is identity resolution, and the interesting
failure is resolving too aggressively — merging two real customers who share a
household or a phone number.

Source data in `seed/` should therefore contain both kinds of case: genuine
duplicates that must match, and near-duplicates that must not. A ruleset that
scores well only because the test data has no hard cases has not been tested.

## Repository conventions

| Folder | Contents |
|---|---|
| `force-app/` | Metadata **retrieved from** the org, not authored here |
| `seed/` | Scripts that build the starting data, including its deliberate defects |
| `deliverables/` | Design docs, SOPs, analyses, runbooks — the substance |
| `evidence/` | Before/after screenshots and test results, per phase |

`deliverables/build-log.md` carries three entries covering provisioning and the
opening audit. Every subsequent change gets a row: date, component, type, change,
and the requirement it traces to.

## Rules worth enforcing in review

- Deliberate defects in source data are the exercise. Do not quietly fix them.
- Consent and privacy is week 7, but consent flags belong in the data model from
  week 2. Retrofitting them is the mistake this track is designed to teach.
- No `sfdx-project.json` exists here yet — this repo cannot be deployed from or
  retrieved into until one is added.
- Never commit an sfdx auth URL. It is a full credential. See `.gitignore`.
