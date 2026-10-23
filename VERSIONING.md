# Release Versioning Convention

## Semantic version rules

Use `MAJOR.MINOR.PATCH` according to Semantic Versioning:

- **MAJOR** increments for an incompatible public API or behavior change. Example: `v1.4.2 -> v2.0.0` for a breaking API change.
- **MINOR** increments for backward-compatible functionality. Reset PATCH to zero. Example: `v1.4.2 -> v1.5.0` for a new optional checkout capability.
- **PATCH** increments for backward-compatible fixes. Example: `v1.4.2 -> v1.4.3` for a timeout fix that does not change the public interface.

Released version numbers are immutable: never move or reuse a published release tag.

## Tag naming

Use exactly `vMAJOR.MINOR.PATCH`, with a lowercase `v` prefix and non-negative integer components without leading zeroes. Example: `v1.5.0`.

## Release tags: annotated, not lightweight

Every release uses an **annotated** tag so the tag object records a release message and tagger metadata alongside its target commit. Create one with:

```sh
git tag -a v1.5.0 -m "Release 1.5.0: add optional checkout validation"
```

Push release tags with `git push origin --tags`. Do not use lightweight tags for releases.

## Pre-releases

Mark candidates with a hyphenated pre-release identifier, for example `v1.5.0-rc.1` or `v1.5.0-beta.1`. Increment the suffix for each candidate (`rc.1`, `rc.2`). Under SemVer, a pre-release sorts before the corresponding final release: `v1.5.0-rc.2` is earlier than `v1.5.0`. Publish the final `v1.5.0` only after the candidate is accepted; do not treat pre-release tags as production releases.
