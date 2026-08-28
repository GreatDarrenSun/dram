# evidence/

This directory is the index/home for reproducible technical evidence.

Do not dump arbitrary chat transcripts here.

## What belongs here

Examples:

- simulation logs or compact checked-in extracts;
- waveform screenshots only when accompanied by signal/time explanation;
- parser outputs;
- compile/elaboration configuration snapshots;
- parameter tables;
- DFI decode summaries;
- regression matrices;
- hashes/manifests pointing to local release artifacts;
- exact references to local-only proprietary evidence.

Large/proprietary files may remain local. In that case, commit a small Markdown/JSON/CSV evidence record containing exact path/version/procedure/result.

## Recommended layout

```text
evidence/
  config/
  simulation/
  dfi/
  regressions/
  manifests/
  local_refs/
```

Create subdirectories only when needed.

## Minimum evidence record

Every evidence record should contain:

```text
EVIDENCE_ID:
TASK_ID:
DATE:
EXECUTOR / MODEL:
SOURCE_VERSION:
SOURCE_PATH:
COMMAND / PROCEDURE:
RESULT:
VERDICT:
LIMITATIONS:
RELATED_DECISION / UNKNOWN:
```

## Evidence quality

Preferred order:

1. reproduced dynamic result;
2. runtime/elaboration configuration;
3. active RTL path;
4. compile-time definitions;
5. static report;
6. AI inference.

A report can summarize evidence but should not be the only proof when a stronger artifact exists.
