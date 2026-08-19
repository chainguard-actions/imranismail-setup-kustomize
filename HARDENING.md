<!-- markdownlint-disable -->

# Hardening Report: imranismail--setup-kustomize/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **imranismail--setup-kustomize/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses actions/checkout@v2 (a mutable tag reference) instead of a full 40-character SHA commit hash. This means the action could be silently updated or replaced by a supply-chain attacker. Both steps in the 'build' and 'test' jobs reference the same unpinned tag. These should be pinned to a specific commit SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:20`

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key, and neither the 'build' job nor the 'test' job defines its own 'permissions:' block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, packages, etc.). A minimal permissions block such as 'permissions: read-all' or specific scopes should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned both `actions/checkout@v2` references (lines 14 and 20) to the full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with a `# v2` comment. 2. Added a top-level `permissions: read-all` block to restrict the workflow's default token permissions.

### Iteration 2

**Fixes applied:** broad-permissions

**Notes:**

Replaced `permissions: read-all` with specific minimal permissions `contents: read` in `.github/workflows/test.yml`. The workflow only performs repository checkouts and runs local npm/kustomize commands, so `contents: read` is the only permission required.

