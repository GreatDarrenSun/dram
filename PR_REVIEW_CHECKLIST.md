# AI Project Brain Bootstrap — Review Checklist

Use this checklist when reviewing the bootstrap PR.

## Safety

- [ ] No existing repository file was modified or deleted.
- [ ] No DUT/Golden RTL was modified.
- [ ] Changes are isolated on `ai-project-brain-v1-20260828`.

## Continuity

- [ ] `AI_START_HERE.md` gives a deterministic reading order.
- [ ] `AGENTS.md` defines evidence rules and multi-AI handoff.
- [ ] `PROJECT_STATE.md` states the repository freshness boundary.
- [ ] `DECISIONS.md` separates accepted from provisional decisions.
- [ ] `TASKS.md` defines the next state-reconciliation tasks.

## Anti-repeat / anti-hallucination

- [ ] Historical date-named notes are not automatically treated as current truth.
- [ ] `not found != does not exist` is explicit.
- [ ] COMPILED / INSTANTIATED / ENABLED / SELECTED / ACTIVE are distinguished.
- [ ] Dynamic claims require dynamic/runtime evidence where appropriate.

## Known issue surfaced rather than hidden

- [ ] The conflict between `unknows.md` HIGH blockers and later Phase 2C claims is explicitly recorded.
- [ ] STATE-SYNC-001 is ready to reconcile that conflict after merge.

## ChatGPT Project

- [ ] `CHATGPT_PROJECT_INSTRUCTIONS.md` can be copied into a dedicated ChatGPT Project.

## Merge recommendation

Merge only if the repository is intended to serve as the shared AI project-memory/control plane.
