<!-- markdownlint-disable -->

# Hardening Report: imranismail--setup-kustomize/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **imranismail--setup-kustomize/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v2` (a mutable tag reference) in two steps. These should be pinned to a full 40-character commit SHA (e.g., `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`) to prevent supply-chain attacks via tag mutation.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:20`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and neither of its jobs (`build`, `test`) defines job-level permissions. Without explicit permissions, the default GITHUB_TOKEN permissions (which can include write access) are granted to all jobs. A minimal `permissions:` block (e.g., `contents: read`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned both `actions/checkout@v2` references to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e # v2`. (2) Added top-level `permissions: contents: read` block to restrict GITHUB_TOKEN to the minimum required access.

