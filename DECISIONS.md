# DECISIONS.md

> Persistent decisions only. Raw discussion belongs in task/report files.
> Bootstrap: 2026-08-28

## Decision status

- `ACCEPTED` — use by default in future work.
- `PROVISIONAL` — working decision; still needs named evidence or human confirmation.
- `SUPERSEDED` — preserved for history but no longer active.
- `REJECTED` — explicitly considered and not used.

---

## D-001 — GitHub is the AI control plane, not automatically the full source tree

**Status:** ACCEPTED  
**Date:** 2026-08-28

### Decision

Use `GreatDarrenSun/dram` as the shared project-memory, state, decision, task and evidence index for ChatGPT / Codex / Cimi / humans.

Do not assume the repository contains all proprietary RTL, simulation environments, specifications or release artifacts.

### Why

The current repository is dominated by task notes, requirement notes and unknown ledgers rather than a complete implementation tree.

### Consequence

When local-only evidence is needed, every task must record exact local path/version/procedure/result and sync a compact evidence summary back to GitHub.

---

## D-002 — Structured state beats dated notebook ordering

**Status:** ACCEPTED  
**Date:** 2026-08-28

### Decision

New AI sessions must start from:

`AI_START_HERE.md → AGENTS.md → PROJECT_STATE.md → DECISIONS.md → TASKS.md → unknows.md`

Historical files such as `0819-*`, `0820*`, `0821` remain evidence/history but are not automatically authoritative because of their filenames or dates.

### Why

The repository already contains a state contradiction: an older unknown ledger still lists HIGH blockers while a later task note claims those areas were closed.

### Consequence

Future status changes must update the structured ledgers.

---

## D-003 — Evidence-first active-path classification

**Status:** ACCEPTED  
**Date:** 2026-08-28

### Decision

For generated/muxed controller paths, distinguish:

`COMPILED → INSTANTIATED → ENABLED → SELECTED → ACTIVE`

Do not label a path ACTIVE merely because its module is present or instantiated.

### Why

This distinction is already central to the repository's DDR5 1N/2N and scheduler-path analysis.

### Consequence

Any future path-closure report must trace selection into the real downstream consumer.

---

## D-004 — Preserve Golden/frozen implementation evidence

**Status:** ACCEPTED  
**Date:** 2026-08-28

### Decision

Default AI work is non-destructive:

- no direct main-branch editing for non-trivial changes;
- do not modify Golden/frozen RTL unless a task explicitly authorizes it;
- prefer branch + PR;
- dynamic validation must not modify DUT RTL merely to obtain PASS.

### Consequence

Repository automation and AI instructions should bias toward reviewable, reversible changes.

---

## D-005 — Current near-term MC architecture target

**Status:** PROVISIONAL  
**Date source:** repository note `问题0821`

### Working decision

The near-term MC target is a minimal controller that can reliably initialize DRAM and support Bootloader/OS operation before advanced performance features.

Working priority:

1. init / MR / PHY-training coordination / DFI readiness;
2. reliable basic read/write, bank state and timing;
3. refresh, turnaround/conflict control and debug sufficient for stable long-run operation;
4. advanced QoS, aggressive reorder and performance optimization later.

### Why provisional

The repository document frames this as a discussion/architecture position to be challenged with experienced SoC MC engineers, not a fully signed-off architecture freeze.

### Closure needed

Promote to ACCEPTED only after a formal architecture review or explicit human decision is recorded.

---

## D-006 — Multi-AI role split

**Status:** ACCEPTED  
**Date:** 2026-08-28

### Decision

Default division of labor:

- ChatGPT: architecture, research, task decomposition, cross-source synthesis and review.
- Codex: repository/local engineering execution, code changes, scripts and reproducible validation.
- Cimi/internal models: high-volume inventory/classification/evidence extraction when advantageous.
- Human: irreversible architecture/business decisions and hardware/proprietary-data actions.

Task-specific assignments in `TASKS.md` override the default.

---

## How to change a decision

Do not edit away the old rationale. Add a new decision or mark the old one SUPERSEDED, with:

- new evidence,
- affected tasks/files,
- reason for change,
- reviewer/owner,
- migration impact.
