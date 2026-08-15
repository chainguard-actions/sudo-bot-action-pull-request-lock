<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-lock/v1.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-lock/v1.0.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files use mutable tag-based action references instead of pinned full SHA commit hashes, making them vulnerable to supply-chain attacks if the referenced tags are moved or compromised.

build.yml:
- `uses: actions/checkout@v1` (line 8)
- `uses: actions/setup-node@v1` (line 9)
- `uses: actions/cache@v1.0.3` (line 13)

lock.yml:
- `uses: sudo-bot/action-pull-request-lock@v1.0.5` (line 11)

All references should be pinned to a full 40-character commit SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v1`).

Locations:

- `.github/workflows/build.yml:8`
- `.github/workflows/build.yml:9`
- `.github/workflows/build.yml:13`
- `.github/workflows/lock.yml:11`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` key, and no job within either file declares job-level permissions. This means both workflows run with GitHub's default permissions (which include write access to repository contents and other scopes), violating the principle of least privilege. A `permissions:` block with minimal required scopes should be added to each workflow.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/lock.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all 4 action references to full 40-character commit SHAs with original tags preserved in comments. (2) Added minimal top-level permissions blocks — build.yml gets 'contents: read' for checkout/cache/npm operations, lock.yml gets 'pull-requests: write' for the pull request locking action.

