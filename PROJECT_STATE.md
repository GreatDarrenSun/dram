# PROJECT_STATE.md

> Repository control-plane snapshot
> Bootstrap date: 2026-08-28
> Repository main-branch evidence currently observed through: 2026-08-21

## 1. Current mission

`需求` defines the target platform as an FPGA-based tester focused on **LPDDR6 + DDR6**, with DDR5/GDDR6 reserved, and organizes requirements across platform, protocol/PHY/DFI, test engine, debug/DFX, software/process and test coverage.

A later design-question document states a near-term architecture goal of a **minimal MC capable of reliable Bootloader/OS operation**, prioritizing protocol correctness, timing, refresh, init/training and basic datapath before advanced QoS/reordering/performance features.

Status: `[CONFIRMED_FROM_REPO]`

## 2. Repository contents today

The repository is currently a mixed control/evidence notebook rather than a full RTL source tree. Top-level contents include:

- dated analysis/task notes (`0813`, `0817`, `0819-*`, `0820*`, `0821`),
- `unknows.md`,
- `问题0821`,
- `需求`,
- other historical notes.

This means GitHub should currently be treated as a **project memory / handoff / evidence index**, not automatically as the complete proprietary implementation workspace.

Status: `[CONFIRMED_FROM_REPO]`

## 3. DDR5 analysis status visible in repository

A later task note (`0820-tocx`) states the following work had been completed before dynamic validation:

- Phase 1: compile configuration, inventory, hierarchy, protocol/config matrix;
- Phase 1.5: active scheduler closure, DDR5→PAS CPE, DDR4→Legacy CPE, ECC disabled, memory geometry resolved, HIF/XPI/DDRC topology resolved;
- Phase 2A: AXI WRITE command/data paths and association complete;
- Phase 2A.5: DDR5 1N/2N selection and WDATARAM read pipeline analyzed;
- Phase 2B: AXI READ request/DFI/return path and RT FIFO matching complete;
- stated gate: `READY_FOR_SIMULATION_VALIDATION = YES`.

Status: `[HISTORICAL_CLAIM_NEEDS_RECONCILIATION]`

Reason: `unknows.md` still lists six HIGH blockers that overlap with items the later note claims were closed.

## 4. Known state conflict requiring reconciliation

`unknows.md` still lists these HIGH items:

- U-001 active scheduler path;
- U-002 DDR5 vs DDR4 runtime mode;
- U-003 XPI↔CPF/CPE topology;
- U-004 ECC enable;
- U-005 single vs dual channel;
- U-006 rank count.

But `0820-tocx` states that active scheduler/configuration/topology/ECC/geometry closure was already completed.

Therefore:

`STATE_LEDGER_CONSISTENCY = FAIL`

This is not necessarily a technical failure. It is a **project-memory synchronization failure**.

### Required closure

A new executor must compare the later reports/evidence against each U-001…U-006 item and then:

1. mark each item CLOSED / PARTIAL / OPEN;
2. attach exact evidence path/location;
3. preserve unresolved runtime-only gaps;
4. update `unknows.md` rather than leaving contradictory ledgers.

## 5. Freshness boundary

No repository commit newer than 2026-08-21 was observed during this bootstrap before the control-plane change itself.

Therefore technical work performed after 2026-08-21 in local workspaces, ChatGPT, Codex, Cimi, generated reports or release folders is currently:

`[NEEDS_SYNC_TO_GITHUB_CONTROL_PLANE]`

Do not infer those technical results into this file without evidence or an explicit sync task.

## 6. Current project-control status

| Area | Status | Meaning |
|---|---|---|
| GitHub connection | CONFIRMED | ChatGPT can access the repository |
| AI start entry | PRESENT | `AI_START_HERE.md` |
| Shared agent rules | PRESENT | `AGENTS.md` |
| State ledger | PRESENT | this file |
| Decision ledger | PRESENT | `DECISIONS.md` |
| Task ledger | PRESENT | `TASKS.md` |
| ChatGPT Project instructions | PRESENT | `CHATGPT_PROJECT_INSTRUCTIONS.md` |
| Evidence index | PRESENT | `evidence/README.md` |
| Report index | PRESENT | `reports/README.md` |
| Workflow/state-sync policy | PRESENT | `docs/` |
| HIGH-unknown reconciliation | OPEN | first recommended technical-control task |
| Post-2026-08-21 external-work sync | OPEN | requires explicit evidence import |

## 7. Next recommended sequence

1. Run **STATE-SYNC-001**: reconcile U-001…U-006 using existing repository/local evidence; do not rescan everything.
2. Run **STATE-SYNC-002**: import the latest post-2026-08-21 validated project milestones into structured GitHub summaries.
3. After those two sync tasks, use `PROJECT_STATE.md` as the authoritative current-state entry for new AI sessions.

## 8. Rule for future updates

Update this file only when project truth materially changes. Do not use it as a raw activity log.

Every state change should point to:

- task ID,
- evidence path,
- commit/PR or local artifact,
- verdict,
- date,
- remaining gap.
