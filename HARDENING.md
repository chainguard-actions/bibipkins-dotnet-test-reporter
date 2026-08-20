<!-- markdownlint-disable -->

# Hardening Report: bibipkins--dotnet-test-reporter/v1.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **bibipkins--dotnet-test-reporter/v1.6.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses 'actions/checkout@v4' (a mutable tag reference) in two steps. These should be pinned to a full 40-character commit SHA to prevent supply-chain attacks. Failing references: 'actions/checkout@v4' (line 17, build job) and 'actions/checkout@v4' (line 24, test job).

Locations:

- `.github/workflows/test.yaml:17`
- `.github/workflows/test.yaml:24`

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key, and the 'build' job has no job-level 'permissions:' key. Only the 'test' job defines permissions (pull-requests: write). The 'build' job runs with default permissions, which may include write access to repository contents. Every job should have an explicit minimal permissions block, or a restrictive top-level permissions block should be added.

Locations:

- `.github/workflows/test.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned both `actions/checkout@v4` references to full SHA `11d5960a326750d5838078e36cf38b85af677262 # v4` in the build and test jobs. 2. Added top-level `permissions: {}` to restrict default permissions, and added `permissions: contents: read` to the build job (minimum needed for checkout). The test job already had `pull-requests: write` which was preserved.

