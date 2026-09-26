# Codex contributor credit

Date: 26 September 2026 (Australia/Sydney)
Target: hossainconsulting/coastline-retail-group
Request: Credit Codex across the owner's repositories.
Starting commit: eff5bea919974dcde723e29fb519c668fa82891f

## Changes

Added an AI-contributor credit to the root README. Existing README bytes were
preserved as a prefix where a README existed. No historical author attribution,
licence, application code, access permission or repository visibility was changed.

## Actual validation

- Clean temporary checkout confirmed with git status --porcelain before editing.
- Existing instruction and evidence files inspected before preparing the change.
- Existing README preservation checked by a byte-prefix assertion.
- git diff --check exited 0 after the README edit.
- New credit and evidence contain no credentials or private contact details.
- Staged scope is limited to README.md and this dated evidence file.

## Limits

Documentation-only update: no application tests, deployments or org operations
were requested or run. This is AI-tool attribution, not a GitHub user invitation
or a claim that every planned feature has been implemented by Codex.
