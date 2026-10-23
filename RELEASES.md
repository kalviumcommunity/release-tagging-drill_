# Release Notes

These entries describe the source snapshots identified by the new annotated tags. Dates are Git commit dates, not verified deployment dates. None of these versions can be confirmed as currently running in production from the supplied records.

## v1.0.0 — 2026-06-06

**Summary:** Initial tagged checkout-service placeholder snapshot.

### Added

- Minimal checkout-service placeholder and repository release-tagging exercise scaffold.

**Rollback target:** None recorded. This is the earliest release in this map; no prior known-good version is established.

## v1.0.1 — 2026-06-06

**Summary:** Historical deployment-history documentation snapshot.

### Changed

- Updated the deployment-history records.

**Rollback target:** `v1.0.0`, the previous tagged source snapshot. The available records do not prove that it was deployed or known-good in production; verify before redeploying.

## v1.1.0 — 2026-06-06

**Summary:** Refined the placeholder startup output to identify the service and its placeholder version.

### Changed

- Replaced the generic checkout placeholder labels with explicit `checkout-service` and `0.0.0-placeholder` output.
- Kept the application as an exercise placeholder; this is not a production checkout implementation.

**Rollback target:** `v1.0.1`, the previous tagged source snapshot. The available records do not prove that it was deployed or known-good in production; verify before redeploying.
