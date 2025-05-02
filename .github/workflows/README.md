# GitHub Actions Workflows

This directory contains GitHub Actions workflows for automating various aspects of our development process.

## PR Status Tracking

**File:** `pr-status-tracking.yml`

This workflow automatically tracks the status of issues referenced in pull requests and updates their labels accordingly.

### How It Works

1. **When a Draft PR is created:**
   - Referenced issues are labeled as `in-progress`
   - A comment is added to the issue linking to the PR

2. **When a PR is marked Ready for Review:**
   - The `in-progress` label is removed
   - Issues are labeled as `review-ready`

3. **When a PR is merged to `develop`:**
   - Issues are labeled as `merged-to-develop`
   - Issues are NOT closed automatically at this stage

4. **When a PR is merged to `main`:**
   - Issues receive a `released` label
   - GitHub will auto-close the issues if proper keywords were used

### Usage

Simply reference issues in your PR description using one of these keywords:
- `Fixes #123`
- `Resolves #123`
- `Closes #123`

The workflow will automatically track the status of these issues.

## Release Management

**File:** `release-management.yml`

This workflow helps generate release PRs that include all issues that have been merged to develop but not yet released.

### How It Works

1. Creates a new release branch from `develop`
2. Collects all issues with the `merged-to-develop` label
3. Creates a PR from the release branch to `main` with:
   - A list of all included issues
   - References to automatically close these issues when merged

### Usage

Trigger this workflow manually from the Actions tab with:
- **Version:** The version number for this release (e.g., `1.2.0`)

The workflow will create a release PR that includes all pending issues.

## Labels Used

These workflows use the following labels:

- `in-progress`: Issue is being worked on in a draft PR
- `review-ready`: Work is complete and ready for review
- `merged-to-develop`: Implementation has been merged to develop
- `released`: Feature has been released to production

Make sure these labels exist in your repository.
