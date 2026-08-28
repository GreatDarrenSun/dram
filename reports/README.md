# reports/

This directory contains conclusion-oriented engineering reports.

Reports explain what the evidence means. Reproducible raw/compact evidence should live under `evidence/` or be referenced by exact local path.

## Naming

Prefer stable task IDs:

```text
reports/<TASK_ID>_<SHORT_TITLE>.md
```

Example:

```text
reports/STATE_SYNC_001_HIGH_UNKNOWN_RECONCILIATION.md
```

Avoid relying only on date-based filenames because dates do not communicate task identity or whether a conclusion is superseded.

## Required header

Each substantial report should begin with:

```text
TASK_ID:
DATE:
EXECUTOR:
MODEL:
SOURCE VERSION:
VERDICT: PASS / PASS_WITH_GAPS / FAIL / BLOCKED
```

## Required content

A good report normally contains:

1. Goal / scope
2. Inputs
3. What was actually inspected/run
4. Findings with evidence paths
5. Facts vs inferences
6. Gaps / blockers
7. Impact on architecture/project state
8. Files changed
9. Acceptance result
10. Next owner/action

## Supersession

Do not delete an old report because a new result contradicts it.

Mark the old conclusion superseded from `DECISIONS.md`, `PROJECT_STATE.md`, `TASKS.md`, or a newer report, and explain the evidence change.
