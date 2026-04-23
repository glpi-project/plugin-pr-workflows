# plugin-pr-workflows

Reusable GitHub Actions workflows for pull request checks.

## Usage

Call this workflow from your repository:

```yaml
on:
  pull_request:
    types: [opened, synchronize, reopened, edited, assigned, unassigned, labeled, unlabeled]

jobs:
  checks:
    uses: "glpi-project/plugin-pr-workflows/.github/workflows/pullrequest-workflow.yml@v1"
```

> **Important:** all types listed above must be present:
> - `edited` — re-runs checks when the PR description is updated (e.g. ticking checklist items)
> - `assigned` / `unassigned` — re-runs checks when assignees change
> - `labeled` / `unlabeled` — re-runs checks when labels change

## Jobs

### `check-checklist`

Fails if any checklist item (`- [ ]`) remains unchecked in the PR description.

### `check-author-assigned`

Fails if the PR author is not in the assignees list. Re-runs on every assignee change (`assigned`/`unassigned` events).

### `check-label`

Fails if no label has been applied to the PR. Re-runs on every label change (`labeled`/`unlabeled` events).

### `check-changelog`

Fails if `CHANGELOG.md` has not been modified in the PR.
