# Tag Audit

## Commands and observed repository state

The following commands were run against the checked-out repository:

```text
git tag
(no output)

git log --oneline --decorate --all
5056222 Agent host session 5e5f3796-ff40-4a0c-b2ec-25c3f65e29c9 - baseline checkpoint
82535d9 (HEAD -> feature/release-tagging, origin/main, origin/HEAD, main) feat: add dummy checkout service
c17d4c4 feat: add dummy checkout service
86989b6 docs: add old release notes and changelog
9426db9 docs: add inconsistent old release notes and changelog
28bd110 docs: add broken deployment history and incident log
da6b2ed docs: add broken deployment history and incident log
ff1fb9a docs: scaffold assignment repository
4febcc6 first commit

git tag --sort=-v:refname
(no output)
```

There are no actual tag refs in the repository at audit time. The names below occur in legacy documents; they are claims or references, not verifiable Git tags. This means none of those names can currently be used to resolve a release commit with Git.

## Specific problems and operational risks

| Evidence | Problem | Team impact and rollback/traceability risk |
|---|---|---|
| `latest-good` in `CHANGELOG.md`, `docs/deployment-history.md`, and `docs/release-notes-old.md` | The name is mutable-sounding and does not identify a version; it is also absent from `git tag`. | Operators cannot establish which commit was deployed or check it out. If the name were later reused, the same rollback command could resolve to a different snapshot, undermining incident reproduction and audit evidence. |
| `release_2` in `CHANGELOG.md` and `docs/release-notes-old.md`; `docs/incident-log.md` calls it a lightweight tag | The underscore name conveys no semantic version, and the repository contains no such ref to inspect. | The incident log says this was an older unsupported commit, but without the ref there is no hash to verify. A rollback cannot be reproduced, and the claim that it was lightweight cannot be independently checked against Git objects. |
| `v1.4.2` in `CHANGELOG.md` and `docs/release-notes-old.md` | The changelog says production was only “assumed” to be this version; the tag is not present in Git. | Deployment identity is uncertain, so responders cannot compare production with a known source commit or select a trustworthy prior deployment for rollback. |
| `stable-build` in `docs/deployment-history.md` and `docs/release-notes-old.md` | The deployment history explicitly says its deployment record is missing, and no Git ref exists. | “Stable” is an unsupported assertion, not evidence of a healthy release. The team cannot know what was supposedly stable or whether it is a safe rollback target. |
| `1.5.0` in `docs/release-notes-old.md` | It omits the required `v` prefix and is not an actual Git tag. | Naming inconsistency makes scripts, documentation, and operator searches unreliable; a command using the expected `v1.5.0` spelling cannot find this purported release. |
| `v2-final-FINAL` in `docs/release-notes-old.md` | The repeated “final” suffix is not a version and the note itself questions production readiness; there is no matching ref. | The team cannot tell whether this is newer than another candidate or safe to deploy. Choosing it for rollback would be guesswork rather than selecting an identified commit. |
| `patch-new` in `docs/release-notes-old.md` | The name gives neither a version nor the scope of the patch, and is absent from Git refs. | Auditors cannot determine what changed or distinguish it from any later “new” patch. No repeatable commit-level rollback target can be established. |

The historical dates in the old deployment documents do not map reliably to Git commits. They are not used as deployment dates in the new release map.
