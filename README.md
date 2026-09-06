# Coastline Retail Group Internship

> **This is a simulation, not client work.** Coastline Retail Group Pty Ltd is a fictional company.
> This repository documents a self-directed Salesforce project built to develop
> and evidence implementation skills. No real customer data appears anywhere in it.

**Certification track:** Data Cloud Consultant
**Salesforce org:** Developer Edition (CLI alias `coastline`)
**Scope:** 10 weeks | source ingestion, data modelling, identity resolution, calculated insights, segmentation, activation, consent and privacy, governance handover

## The brief

Ten weeks as the incoming data specialist at a 62-store NSW and Victorian
homewares retailer whose customers exist three times over — once in the point of
sale, once in the e-commerce platform, once in the loyalty app — and where nobody
can answer how many customers the business actually has.

## What's in here

| Folder | Contents |
|---|---|
| `force-app/` | Salesforce metadata retrieved from the org — the configuration itself |
| `seed/` | Apex scripts that build the starting data, including its deliberate defects |
| `deliverables/` | The written work: design docs, SOPs, analyses, runbooks |
| `evidence/` | Before/after screenshots and test results per phase |

`deliverables/` is the substance. The configuration proves the clicks happened;
the documents prove the thinking did.

## Progress

Build log lives in `deliverables/build-log.md` — every change with its date,
reason, and the requirement it traces to.

## Org prerequisites

Unlike the other tracks, this one needs provisioning before any build can start:

- [ ] **Turn Data Cloud on.** Setup → `Data Cloud Setup` → **Get Started**. The
      entitlements ship with the org (`Data Cloud` permission set licence, Active,
      200,000) but provisioning has not run. `SELECT Id FROM DataspaceScope`
      failing with "sObject type not supported" is the tell.
- [ ] **Fix the org locale.** The org provisioned as `Country: United States`,
      `LanguageLocaleKey: en_US`. Every other org in this program is Australian.
      Set Locale to English (Australia), Currency to AUD, Time Zone to
      Australia/Sydney — **before** ingesting anything, because currency and date
      formats propagate into the data model and are painful to unpick afterwards.

## For recruiters and agencies

**What this repository evidences:** Data Cloud Consultant discipline — identity resolution
designed against deliberately messy triplicated customers, with match rules and
reconciliation rules documented as separate decisions.

**State as at 06/09/2026:** Scoped; org provisioned. Data Cloud provisioning and the
locale correction are outstanding and block all ingestion. Nothing has been ingested or
modelled yet, and this README will say so until it has.

**Read these first:**

1. [`deliverables/build-log.md`](deliverables/build-log.md) — the record so far, including the provisioning audit
2. [`CLAUDE.md`](CLAUDE.md) — the engagement rules and the matching-versus-reconciliation distinction

**How to verify:** every change is in the build log with its date and the requirement it
traces to; corrections are appended, never edited over. The
[skill-to-evidence map](https://portfolio.hossainconsulting.com/#evidence) on the portfolio shows where each certification is
applied, and the [hiring page](https://portfolio.hossainconsulting.com/#hire) says what I am open to.

---

Built by [Hemayet Hossain](https://github.com/hossainconsulting) · Sydney, Australia
Portfolio: [portfolio.hossainconsulting.com](https://portfolio.hossainconsulting.com)

---

## Connect

Built by **Hemayet Hossain**, Salesforce administrator and implementation
consultant, Sydney, Australia. This is one of eight projects
published in full; the complete record and the certification track are on the
portfolio.

[Portfolio](https://portfolio.hossainconsulting.com/?utm_source=github&utm_medium=readme&utm_campaign=coastline-retail-group) ·
[All links](https://portfolio.hossainconsulting.com/links) ·
[GitHub](https://github.com/hossainconsulting) ·
[LinkedIn](https://www.linkedin.com/company/hossain-consulting) ·
[Instagram](https://www.instagram.com/hossainconsulting/)
