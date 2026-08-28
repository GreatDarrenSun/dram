# AGENTS.md

This repository is a shared working-memory and evidence index for ChatGPT, Codex, Cimi and human engineers.

## 1. Operating mode

Default role split:

- **ChatGPT**: architecture/research lead, decision framing, cross-source synthesis, task decomposition, review.
- **Codex**: repository/local-code executor, scripting, static/dynamic validation, reproducible edits, PR preparation.
- **Cimi**: large-context coarse analysis, inventory, classification, evidence extraction, batch review when internal/local access is available.
- **Human**: final owner for irreversible architecture choices, proprietary-data release, hardware actions, and ambiguous business decisions.

Do not assume this role split is immutable; `TASKS.md` is authoritative for each task.

## 2. Mandatory start sequence

Read:

1. `AI_START_HERE.md`
2. `PROJECT_STATE.md`
3. `DECISIONS.md`
4. `TASKS.md`
5. `unknows.md`

Do not rescan the entire repository unless the active task explicitly requires it.

## 3. Evidence-first discipline

For every material claim, distinguish:

- `[CONFIRMED]`
- `[INFERRED]`
- `[NEEDS_EVIDENCE]`
- `[STALE]`
- `[BLOCKED]`

Highest-value evidence normally follows:

`dynamic waveform/log > elaborated/runtime config > active RTL path > compile-time define > static note > AI inference`.

When comparing two sources, explain why one outranks the other.

## 4. Active-path rule

For generated/muxed protocol/controller variants, never equate:

`COMPILED = INSTANTIATED = ENABLED = SELECTED = ACTIVE`.

To label a path ACTIVE, prove the chain far enough to show its output is selected into the real downstream path.

## 5. Write safety

Unless the task explicitly authorizes RTL changes:

- do not modify DUT RTL;
- new testbench/scripts/monitors/parsers are allowed only when the task permits them;
- never change RTL merely to make simulation pass;
- preserve Golden/frozen baselines;
- prefer a new branch + PR over direct main-branch edits.

For any write:

- state exact files changed;
- explain why;
- give validation result;
- identify remaining gaps.

## 6. Project freshness rule

The current repository contains historical dated notes. A historical note is not current truth by filename/date alone.

`PROJECT_STATE.md` must explicitly state freshness. If GitHub does not yet contain recent local evidence, mark that section `[STALE]` or `[NEEDS_SYNC]` instead of guessing.

## 7. Task contract

Every non-trivial task in `TASKS.md` should define:

- Task ID
- Goal
- Executor/model
- Inputs and paths
- Allowed writes
- Deliverables
- Acceptance criteria
- Evidence locations
- Result: PASS / PASS_WITH_GAPS / FAIL / BLOCKED
- Next owner

If the user requests a copy-paste instruction for Codex/Cimi, include all of the above and stop conditions.

## 8. Unknown closure

An unknown may be closed only when:

1. the question is answered precisely;
2. supporting evidence location is recorded;
3. assumptions are separated from facts;
4. any local-only evidence is named by exact path/procedure;
5. downstream implications are stated.

If only part is solved, keep it open and narrow the missing evidence.

## 9. Decision record rule

A persistent architecture/project decision belongs in `DECISIONS.md` when it affects future work.

Do not reopen a decision without at least one of:

- new specification evidence,
- new RTL/runtime evidence,
- failed validation,
- changed project objective,
- explicit human request.

## 10. Repository vs local workspace

This GitHub repository may be an index/control plane rather than the full proprietary source tree.

Never assume GitHub contents equal the user's complete local workspace. When local evidence is required, use exact local paths supplied by the user/task and return a compact evidence summary to GitHub.

## 11. Communication style

For technical reports and review material:

- prefer concise Chinese engineering language;
- keep necessary English protocol/RTL terms;
- avoid inflated certainty;
- explicitly call out blockers, assumptions, and evidence gaps;
- prefer tables for status matrices and acceptance results.
