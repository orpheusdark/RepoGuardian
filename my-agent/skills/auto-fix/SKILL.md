---
name: auto-fix
description: Apply safe, deterministic code improvements automatically without altering business logic.
license: MIT
allowed-tools: Read Write
---

# Skill: Auto Fix

## Purpose
Apply strictly safe improvements that increase clarity and maintainability while preserving behavior.

## Allowed Actions
- Remove unused imports.
- Rename unclear local variables with precise intent-revealing names.
- Extract very small helper functions when inputs/outputs/side effects remain identical.
- Remove proven dead local code branches with no runtime path.

## Strict Safety Rules
1. Never change domain rules, authorization logic, pricing logic, or persistence behavior.
2. Never alter public API contracts without explicit confirmation.
3. Never change algorithms.
4. Apply edits only when confidence is High.
5. Stop immediately on ambiguity and request confirmation.

## Execution Steps
Step 1: Identify candidate edits and classify them by safety.
Step 2: Generate patch plan for safe fixes only.
Step 3: For each safe fix, show BEFORE and AFTER snippets.
Step 4: Reject anything that could alter business behavior.
Step 5: Document each applied change and why it is safe.
Step 6: Report blocked items requiring explicit approval.

## Patch Plan Format
- Target: File and symbol
- Change Type: unused import removal | rename | tiny extraction
- Safety Basis: why behavior is preserved
- Validation: how correctness is confirmed

## Safety Decision Logic
- Unused import: safe when symbol has zero references in file scope.
- Local variable rename: safe when scope is local and intent is unambiguous.
- Tiny helper extraction: safe when function boundaries do not alter side effects or error flow.
- Any algorithm change: forbidden.
- Multi-path control-flow changes: unsafe without explicit confirmation.

## Output Contract
### Suggested Patches
- BEFORE snippet
- AFTER snippet

### Safety Notes
- Why each patch is behavior-preserving
