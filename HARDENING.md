<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-lock/v1.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-lock/v1.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in workflow files are pinned to mutable tags rather than full 40-character commit SHA digests, making the action vulnerable to supply-chain attacks if the referenced tags are moved or overwritten.

build.yml failing references:
- `actions/checkout@v3`
- `actions/setup-node@v3`
- `actions/cache@v3`

lock.yml failing references:
- `sudo-bot/action-pull-request-lock@v1.1.0`

Locations:

- `.github/workflows/build.yml:8`
- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:12`
- `.github/workflows/lock.yml:11`

### missing-permissions (severity: medium)

Neither workflow file declares a `permissions:` block at the top level or at the job level. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. Both `build.yml` and `lock.yml` are affected.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/lock.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

build.yml:
- Pinned actions/checkout@v3 → @a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3
- Pinned actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 # v3
- Pinned actions/cache@v3 → @6f8efc29b200d32929f49075959781ed54ec270c # v3
- Added top-level `permissions: {}` (build/lint job needs no special permissions)

lock.yml:
- Pinned sudo-bot/action-pull-request-lock@v1.1.0 → @8d1ae2b00cc4bf943144f4706048d7e75f038c3c # v1.1.0
- Added top-level `permissions: {}` with job-level `issues: write` and `pull-requests: write` (needed for the lock action to lock pull requests)

