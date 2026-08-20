<!-- markdownlint-disable -->

# Hardening Report: imranismail--setup-kustomize/v1.7.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **imranismail--setup-kustomize/v1.7.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v2` (a mutable tag reference) in two steps. These should be pinned to a full 40-character commit SHA to prevent supply-chain attacks. Failing references: `uses: actions/checkout@v2` (lines 14 and 21).

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:21`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and neither the `build` job nor the `test` job defines a job-level `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned both `actions/checkout@v2` references (lines 14 and 21) to the full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with `# v2` comments for readability. 2. Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

