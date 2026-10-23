# Release Map

The tags below are annotated markers on historical source commits, added to establish a consistent release sequence for this exercise. The commit dates are Git commit dates, not deployment dates. The supplied deployment history does not establish that any of these snapshots reached production; current production is therefore **unverified**.

| Version (tag) | Commit (short hash) | Date | What Shipped |
|---|---|---|---|
| `v1.0.0` | `ff1fb9a` | 2026-06-06 | Initial checkout-service placeholder and repository exercise scaffold. Historical source snapshot; no production deployment record verified. |
| `v1.0.1` | `28bd110` | 2026-06-06 | Updated deployment-history documentation. Documentation-only snapshot; no production deployment record verified. |
| `v1.1.0` | `82535d9` | 2026-06-06 | Checkout placeholder refactor with explicit service name and placeholder version in startup output. Historical source snapshot; no production deployment record verified. |

The 2026-06-06 dates above are the dates recorded in Git for these commits. They must not be interpreted as dates of production deployment. Confirm the running deployment and health status through the deployment system before treating any tag as known-good.

## Traceable rollback

```sh
git tag --sort=-v:refname
git describe --tags --abbrev=0
git checkout v1.0.1
# Redeploy the checked-out commit using the team's deployment process.
```

If `v1.1.0` is the release being rolled back, `v1.0.1` is its immediately preceding tagged snapshot in this map; verify it is healthy and was deployed before using it as the rollback target. The consistent, immutable SemVer tags resolve directly to commit hashes, making the source snapshot reproducible and auditable. In contrast, the original history used inconsistent names that are not Git refs and left production deployments undocumented, so rollback targets could not be resolved reliably.
