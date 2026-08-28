# State Synchronization Policy

This repository is intended to prevent repeated AI work caused by stale or fragmented project context.

## Rule 1 — A chat result is not project state until synchronized

A conclusion reached in ChatGPT, Codex or Cimi becomes durable project state only after it is reflected in the appropriate structured file and backed by an evidence reference.

## Rule 2 — Sync conclusions, not transcripts

Do not copy full conversations into the repository. Sync:

- the decision,
- the evidence,
- the task result,
- the remaining gap,
- the next action.

## Rule 3 — Freshness is explicit

Every major state snapshot should record the date/source-version boundary it actually covers.

If newer local work exists but is not yet indexed, mark `[NEEDS_SYNC]` rather than pretending the GitHub state is current.

## Rule 4 — Contradictions become tasks

When two notes disagree, do not silently choose one. Create a state-reconciliation task that identifies:

- claim A,
- claim B,
- stronger/weaker evidence,
- exact proof required,
- ledger(s) to update after resolution.

## Rule 5 — Close the ledger

When a blocker is resolved, update the blocker ledger in the same handoff. A separate later note saying "resolved" while the original blocker remains open is considered synchronization debt.
