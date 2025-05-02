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

**Note:** These labels are automatically created by the workflows if they don't exist in the repository. You don't need to manually create them.

## Automatic Label Creation

Both workflows include functionality to automatically create any required labels if they don't already exist in the repository. This means:

1. No manual setup of labels is required
2. The workflows will work in any repository without prior configuration
3. Labels will have consistent colors and descriptions across all repositories

The labels are created with the following properties:

| Label | Color | Description |
|-------|-------|-------------|
| `in-progress` | Blue (#0052cc) | Issue is being worked on in a draft PR |
| `review-ready` | Purple (#5319e7) | Work is complete and ready for review |
| `merged-to-develop` | Green (#0e8a16) | Implementation has been merged to develop |
| `released` | Blue (#1d76db) | Feature has been released to production |
