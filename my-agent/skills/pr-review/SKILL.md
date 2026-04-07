---
name: pr-review
description: Analyze diffs with strict senior-engineer discipline, focusing only on changed code and real regression risks.
license: MIT
allowed-tools: Read
---

# Skill: Pull Request Review

## Purpose
Analyze changed lines and issue a deterministic PR verdict with risk-first fix guidance.

## Execution Logic
Step 1: Analyze ONLY changed lines and immediate context.
Step 2: Detect logic risks.
Step 3: Detect regressions against previous behavior.
Step 4: Detect unnecessary complexity added by the change.
Step 5: Assign severities and determine verdict.
Step 6: Propose the smallest safe patch for each blocking issue.

## Detection Targets
- Logic risks (condition mistakes, null paths, broken assumptions)
- Regressions (behavior drift, error handling changes, contract mismatch)
- Unnecessary complexity (new deep nesting, redundant branches, over-abstraction)

## Severity Rubric
- CRITICAL: security exposure, data loss risk, or systemic failure path.
- HIGH: likely production bug or major regression.
- MEDIUM: maintainability risk that can evolve into defects.
- LOW: minor issue with low immediate risk.

## Decision Rules
- APPROVE: no HIGH/CRITICAL issues and no unmitigated regression risk.
- REQUEST_CHANGES: any HIGH/CRITICAL issue or unresolved regression risk.

## Output Contract
### PR Verdict
APPROVE or REQUEST_CHANGES

### Key Issues
- File -> Problem -> Fix

### High Priority Fixes
- File -> Patch strategy -> Expected risk reduction

### Suggested Patches
- Optional safe patch for each blocking issue
