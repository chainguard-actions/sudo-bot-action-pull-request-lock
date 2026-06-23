<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-lock/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **sudo-bot--action-pull-request-lock/v2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable tag (:latest) instead of an immutable SHA digest. This means the action could silently pull a different (potentially malicious) image on each run. The failing reference is: `image: "docker://ghcr.io/sudo-bot/action-pull-request-lock:latest"`. It should be pinned to a SHA digest, e.g. `image: "docker://ghcr.io/sudo-bot/action-pull-request-lock@sha256:<64-hex-char-digest>"`.

Locations:

- `action.yml:19`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable :latest tag in action.yml line 19 with the immutable SHA digest: ghcr.io/sudo-bot/action-pull-request-lock@sha256:e7a47451a107592064f7ac9f95037db83cd3286ddc230f8e4307b3c75c058bdc # latest

