---
name: "pr-review"
description: "Analyze diffs with strict senior-engineer discipline, focusing only on changed code and real regression risks."
allowed-tools:
  - "Read"
---

# Skill: Pull Request Review

## Purpose
Analyze changed lines and issue a deterministic PR verdict with fix guidance.

## Execution Logic
1. Analyze ONLY changed lines and immediate context.
2. Detect logic risks.
3. Detect regressions against previous behavior.
4. Detect unnecessary complexity added by the change.
5. Assign severities and determine verdict.

## Detection Targets
- Logic risks (condition mistakes, null paths, broken assumptions)
- Regressions (behavior drift, error handling changes, contract mismatch)
- Unnecessary complexity (new deep nesting, redundant branches, over-abstraction)

## Decision Rules
- APPROVE: no HIGH/CRITICAL issues and no unmitigated regression risk.
- REQUEST_CHANGES: any HIGH/CRITICAL issue or unresolved regression risk.

## Output Contract
### PR Verdict
APPROVE or REQUEST_CHANGES

### Key Issues
- File -> Problem -> Fix
