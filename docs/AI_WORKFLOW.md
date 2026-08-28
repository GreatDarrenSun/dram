# Multi-AI Working Loop

Recommended execution loop:

```text
Human goal
   ↓
ChatGPT: frame decision / define task / choose executor
   ↓
TASKS.md: task contract
   ↓
Codex or Cimi: execute against repository/local evidence
   ↓
evidence/: reproducible proof
   ↓
reports/: compact conclusion
   ↓
ChatGPT: review / challenge / synthesize
   ↓
PROJECT_STATE.md / DECISIONS.md / unknows.md updated
   ↓
Human review for irreversible decisions
```

## Why this reduces repeated work

The next AI does not need the entire previous conversation. It reads the structured state, task contract and evidence references, then opens only the source required for the current question.

## Minimal handoff packet

A completed executor should provide:

```text
TASK_ID
EXECUTOR / MODEL
VERDICT
SOURCE VERSION
FILES/AREAS INSPECTED
FILES CHANGED
EVIDENCE
CLOSED ITEMS
OPEN ITEMS
RISKS
NEXT OWNER
NEXT ACTION
```

## What not to do

Avoid:

- copying entire chat transcripts into GitHub;
- creating a new dated note for every iteration without updating state;
- letting two agents independently solve the same unresolved item without knowing about each other;
- claiming a blocker is closed only in chat while leaving `unknows.md` stale;
- treating an AI-generated report as stronger than the underlying RTL/simulation evidence.
