<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-lock/v1.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-lock/v1.0.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference actions using mutable tags instead of pinned 40-character SHA commit digests, making the action vulnerable to supply-chain attacks if the tag is moved.

build.yml failing references:
- uses: actions/checkout@v1
- uses: actions/setup-node@v1
- uses: actions/cache@v1.0.3

lock.yml failing references:
- uses: sudo-bot/action-pull-request-lock@v1.0.4

Locations:

- `.github/workflows/build.yml:8`
- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:12`
- `.github/workflows/lock.yml:11`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` block, and no job in either file has a job-level `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/lock.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

build.yml:
- Added top-level `permissions: {}` block
- Pinned actions/checkout@v1 → @50fbc622fc4ef5163becd7fab6573eac35f8462e # v1
- Pinned actions/setup-node@v1 → @f1f314fca9dfce2769ece7d933488f076716723e # v1
- Pinned actions/cache@v1.0.3 → @cffae9552bb9f84b9812c1ee9ea2e3c0a70a797e # v1.0.3

lock.yml:
- Added top-level `permissions: {}` block
- Added job-level `permissions: { issues: write, pull-requests: write }` for the lock job (minimum needed to lock a PR)
- Pinned sudo-bot/action-pull-request-lock@v1.0.4 → @dfbd97e4189a02e99efc42786c64c8efab8ac0c5 # v1.0.4

