<!-- markdownlint-disable -->

# Hardening Report: sudo-bot--action-pull-request-lock/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sudo-bot--action-pull-request-lock/v2** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml uses a Docker image with a mutable tag (`latest`) instead of a SHA digest. This means the action can silently pull a different (potentially malicious) image on each run. The image reference `docker://ghcr.io/sudo-bot/action-pull-request-lock:latest` should be pinned to a SHA256 digest.

Locations:

- `action.yml:18`

### unpinned-uses (severity: high)

Multiple `uses:` references in build.yml are pinned to mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks: `actions/checkout@v6` (line 13, 28), `dtolnay/rust-toolchain@stable` (line 15), `Swatinem/rust-cache@v2` (line 18), `docker/setup-qemu-action@v3` (line 29), `docker/setup-buildx-action@v4` (line 30).

Locations:

- `.github/workflows/build.yml:13`
- `.github/workflows/build.yml:15`
- `.github/workflows/build.yml:18`
- `.github/workflows/build.yml:28`
- `.github/workflows/build.yml:29`
- `.github/workflows/build.yml:30`

### unpinned-uses (severity: high)

`uses:` reference in lock.yml is pinned to a mutable version tag instead of a full 40-character commit SHA: `sudo-bot/action-pull-request-lock@v2` (line 12).

Locations:

- `.github/workflows/lock.yml:12`

### unpinned-uses (severity: high)

Multiple `uses:` references in release.yml are pinned to mutable version tags instead of full 40-character commit SHAs: `actions/checkout@v6` (line 20), `docker/setup-qemu-action@v3` (line 23), `docker/setup-buildx-action@v3` (line 26), `docker/login-action@v3` (line 28).

Locations:

- `.github/workflows/release.yml:20`
- `.github/workflows/release.yml:23`
- `.github/workflows/release.yml:26`
- `.github/workflows/release.yml:28`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Fixed all unpinned-uses findings across 4 files:
1. action.yml: Pinned `docker://ghcr.io/sudo-bot/action-pull-request-lock:latest` to SHA256 digest `sha256:e7a47451a107592064f7ac9f95037db83cd3286ddc230f8e4307b3c75c058bdc`, preserving the `docker://` scheme and `:latest` tag inline.
2. build.yml: Pinned `actions/checkout@v6` → `@d23441a48e516b6c34aea4fa41551a30e30af803`, `dtolnay/rust-toolchain@stable` → `@4cda84d5c5c54efe2404f9d843567869ab1699d4`, `Swatinem/rust-cache@v2` → `@e18b497796c12c097a38f9edb9d0641fb99eee32`, `docker/setup-qemu-action@v3` → `@c7c53464625b32c7a7e944ae62b3e17d2b600130`, `docker/setup-buildx-action@v4` → `@bb05f3f5519dd87d3ba754cc423b652a5edd6d2c` (both occurrences).
3. lock.yml: Pinned `sudo-bot/action-pull-request-lock@v2` → `@e20c54d0f068b0b2cf3b345e0585c10ac5d5415a`.
4. release.yml: Pinned `actions/checkout@v6` → `@d23441a48e516b6c34aea4fa41551a30e30af803`, `docker/setup-qemu-action@v3` → `@c7c53464625b32c7a7e944ae62b3e17d2b600130`, `docker/setup-buildx-action@v3` → `@8d2750c68a42422c14e847fe6c8ac0403b4cbd6f`, `docker/login-action@v3` → `@c94ce9fb468520275223c153574b00df6fe4bcc9`. All original tags preserved as inline comments.

