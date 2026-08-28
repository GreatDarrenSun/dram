# AI START HERE

> Repository: `GreatDarrenSun/dram`
> Purpose: make this repository the shared project memory for ChatGPT / Codex / Cimi.
> Last bootstrap: 2026-08-28

## Why this file exists

Do **not** start a new AI session by rescanning the whole repository or treating the newest-looking note as the current truth.

The repository historically contains date-named task notes such as `0819-1`, `0820-tocx`, `0821`, plus `unknows.md` and `需求`. Those files are useful evidence/history, but they are not automatically the current project state.

## Mandatory reading order

Every new AI executor should read, in this order:

1. `AGENTS.md` — operating rules, evidence discipline, write boundaries.
2. `PROJECT_STATE.md` — current project snapshot and freshness status.
3. `DECISIONS.md` — decisions already made; do not reopen without new evidence.
4. `TASKS.md` — active work, owner/model, inputs, outputs, acceptance criteria.
5. `unknows.md` — unresolved technical questions / evidence gaps.
6. Only then open legacy dated notes and RTL/evidence as required by the active task.

## Source-of-truth hierarchy

When sources conflict, use this priority:

1. Reproducible RTL / compile / elaboration / simulation / waveform evidence.
2. Current structured project state in `PROJECT_STATE.md` and current task acceptance evidence.
3. Current decision records in `DECISIONS.md`.
4. Current unknown/evidence ledger.
5. Historical reports and dated task notes.
6. Chat summaries or unsupported AI inference.

A newer date does not automatically beat stronger evidence.

## Evidence labels

Use these labels in reports and task closure:

- `[CONFIRMED]` — directly supported by repository evidence or reproduced result.
- `[INFERRED]` — reasoned from evidence but not directly proven.
- `[NEEDS_EVIDENCE]` — material claim still missing proof.
- `[STALE]` — evidence/status may have been superseded.
- `[BLOCKED]` — cannot proceed without a named missing input/environment.

Never convert `not found` into `does not exist` without an exhaustive basis.

## Handoff rule

At the end of every meaningful AI task:

1. Update `PROJECT_STATE.md` only if project state materially changed.
2. Update `DECISIONS.md` only for decisions that should persist.
3. Update `TASKS.md` with result, evidence location, and next executor.
4. Update/close the corresponding item in `unknows.md` when evidence is sufficient.
5. Put reproducible evidence under `evidence/` and conclusion-oriented reports under `reports/` when those artifacts are committed here.
6. Record exact repository paths, commit/PR references, commands, and PASS/FAIL criteria.

## No-repeat rule

Before starting a new analysis, search the state/decision/task/unknown files for the same question. Reuse existing validated evidence. Re-open a closed question only if:

- source RTL/configuration changed,
- prior evidence was incomplete or contradicted,
- a newer specification changes semantics,
- or the user explicitly requests revalidation.

## Local-only evidence

Large/proprietary RTL, simulation outputs, internal documents, or local paths may not live in this GitHub repository. When a conclusion depends on them, record:

- exact local path,
- executor/model,
- command or procedure,
- output artifact path,
- evidence hash/version if available,
- and whether GitHub contains a summary only.

Do not fabricate local evidence from repository notes.
