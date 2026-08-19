# Build log — Coastline Retail Group Internship

Every change, with the reason and the requirement it traces to. This is the
artefact that survives the project and the one an auditor or a successor reads.

| Date | Component | Type | Change | Why / requirement |
|---|---|---|---|---|
| 19/08/2026 | Org: `coastline` | Provisioning | Developer Edition created, org named Coastline Retail Group (`00DgL00000b5uvVUAQ`), authenticated to the CLI as alias `coastline` | Dedicated org for the Data Cloud track. The four existing orgs are each allocated to a certification track; ingesting into any of them would pollute graded work |
| 19/08/2026 | Org: `coastline` | Audit | Data Cloud entitlements confirmed present (`Data Cloud` PSL Active, 200,000) but **not provisioned** — `DataspaceScope` does not resolve | Establishes the starting position. Provisioning is a prerequisite, not part of the build |
| 19/08/2026 | Org: `coastline` | Finding | Org provisioned with US locale (`Country: United States`, `LanguageLocaleKey: en_US`) against an Australian scenario | Must be corrected before ingestion — currency and date formats propagate into the data model. Instance `CAN98` is unrelated and not changeable |
