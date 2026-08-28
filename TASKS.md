# TASKS.md

> Active task ledger for human + ChatGPT + Codex + Cimi handoff.
> Do not use this as a raw chat log.

## Status values

- `READY`
- `IN_PROGRESS`
- `PASS`
- `PASS_WITH_GAPS`
- `FAIL`
- `BLOCKED`
- `DEFERRED`

---

## BRAIN-BOOTSTRAP-001 — Build AI project control plane

**Status:** IN_PROGRESS  
**Owner:** ChatGPT  
**Model:** GPT-5.6 Sol  
**Branch:** `ai-project-brain-v1-20260828`

### Goal

Turn `GreatDarrenSun/dram` from a dated-note collection into a structured shared project memory for multiple AI executors.

### Deliverables

- `AI_START_HERE.md`
- `AGENTS.md`
- `PROJECT_STATE.md`
- `DECISIONS.md`
- `TASKS.md`
- `CHATGPT_PROJECT_INSTRUCTIONS.md`
- `evidence/README.md`
- `reports/README.md`

### Acceptance criteria

- Main branch untouched until PR review.
- New AI sessions have a deterministic reading order.
- Evidence/freshness rules prevent old notes being mistaken for current truth.
- Existing contradictory state is explicitly surfaced rather than silently rewritten.
- A reviewable PR is opened.

### Reviewer

Human owner.

---

## STATE-SYNC-001 — Reconcile HIGH unknowns with later DDR5 evidence

**Status:** READY  
**Recommended executor:** Codex  
**Recommended model:** GPT-5.3-Codex-Spark if available; otherwise use the strongest current Codex reasoning model and record the actual model before execution.  
**Reviewer:** ChatGPT / human

### Goal

Reconcile `unknows.md` U-001 through U-006 against the later repository/local evidence without rescanning the whole project.

### Required inputs

Repository:

- `AI_START_HERE.md`
- `AGENTS.md`
- `PROJECT_STATE.md`
- `unknows.md`
- `0819-1`
- `0819-2`
- `0819-2-toCX`
- `0820`
- `0820-tocx`

Local RTL / generated Knowledge Base only as needed to prove missing claims.

### Questions to close

- U-001 active scheduler path
- U-002 DDR5 vs DDR4 runtime mode
- U-003 XPI↔CPF/CPE topology
- U-004 ECC enable
- U-005 single vs dual channel
- U-006 rank count

### Constraints

- Do not modify DUT RTL.
- Do not perform a full repository rescan unless a specific item cannot be resolved from indexed evidence.
- Distinguish compile-time, instantiated, enabled, selected and active.
- Runtime-mode claims require runtime/config evidence, not only defines.
- `not found` is not sufficient closure.

### Required outputs

Create/update a report:

`reports/STATE_SYNC_001_HIGH_UNKNOWN_RECONCILIATION.md`

For each U-001…U-006 include:

- Verdict: CLOSED / PARTIAL / OPEN
- Exact answer
- Evidence path + line/signal/module/command
- Evidence class: static/runtime/dynamic
- Confidence
- Remaining gap
- Downstream impact

Then update `unknows.md` so it no longer contradicts stronger evidence.

Update `PROJECT_STATE.md` only if the reconciliation materially changes current project truth.

### Acceptance criteria

PASS requires all six items to be either:

- CLOSED with traceable evidence, or
- explicitly narrowed to a precise remaining local/runtime dependency.

No broad original HIGH question may remain unchanged if later evidence already answers part of it.

### Copy-paste instruction for Codex

```text
TASK_ID: STATE-SYNC-001

You are the repository/local RTL executor for GreatDarrenSun/dram.

Model: use GPT-5.3-Codex-Spark if available; otherwise use the strongest current Codex reasoning model and record the exact model in the report.

Goal:
Reconcile unknows.md U-001..U-006 against later repository/local evidence. Do NOT rescan the entire project.

Read first, in order:
1. AI_START_HERE.md
2. AGENTS.md
3. PROJECT_STATE.md
4. DECISIONS.md
5. TASKS.md
6. unknows.md
7. 0819-1
8. 0819-2
9. 0819-2-toCX
10. 0820
11. 0820-tocx

Questions:
U-001 active scheduler path
U-002 DDR5 vs DDR4 runtime mode
U-003 XPI↔CPF/CPE topology
U-004 ECC enable
U-005 single vs dual channel
U-006 rank count

Rules:
- Do not modify DUT RTL.
- Use local RTL/Knowledge Base only when the repository evidence is insufficient.
- For path selection distinguish COMPILED / INSTANTIATED / ENABLED / SELECTED / ACTIVE.
- Runtime claims require runtime/config evidence.
- Do not convert not-found into false/disabled.
- Preserve contradictory historical notes; resolve the structured ledger instead of deleting history.

Deliverables:
1. reports/STATE_SYNC_001_HIGH_UNKNOWN_RECONCILIATION.md
2. updated unknows.md
3. update PROJECT_STATE.md only if truth materially changes

For each U-001..U-006 report:
- CLOSED / PARTIAL / OPEN
- exact answer
- evidence file/path + line/signal/module
- evidence type
- confidence
- remaining gap
- downstream impact

Stop condition:
If local proprietary RTL or runtime evidence is required but unavailable, do not guess. Mark the exact item PARTIAL/OPEN, name the precise missing file/signal/test needed, and continue with the other items.

Final handoff:
TASK_ID
EXECUTOR / MODEL
VERDICT
CHANGED
EVIDENCE
CLOSED
OPEN
RISKS
NEXT_OWNER
NEXT_ACTION
```

---

## STATE-SYNC-002 — Import post-2026-08-21 validated milestones

**Status:** READY_AFTER_STATE-SYNC-001  
**Recommended executor:** ChatGPT Work for synthesis + Codex for repository writeback  
**Reviewer:** human

### Goal

Bring validated work performed after the repository's current freshness boundary into the GitHub control plane without dumping full chat transcripts.

### Inputs

Use only authoritative artifacts supplied/connected at execution time:

- local reports,
- release manifests,
- simulation/regression results,
- current GitHub commits/PRs,
- explicitly selected project files.

### Required outputs

- update `PROJECT_STATE.md` with current milestones and freshness date;
- update `DECISIONS.md` with durable decisions only;
- update `TASKS.md` with completed/in-progress task IDs;
- add compact evidence index entries under `evidence/`;
- add conclusion reports under `reports/` only when useful.

### Acceptance criteria

- No chat-only claim is promoted to `[CONFIRMED]` without an artifact/evidence reference.
- Old work is not duplicated if an existing report already proves it.
- Each imported milestone has date, evidence location, verdict and remaining gap.

---

## Template for future tasks

```text
## TASK-ID — Short title

Status:
Executor:
Model:
Reviewer:

Goal:

Inputs:

Allowed writes:

Forbidden writes:

Required outputs:

Evidence required:

Acceptance criteria:

Stop conditions:

Next owner:
```
