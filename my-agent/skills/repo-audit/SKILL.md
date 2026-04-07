---
name: "repo-audit"
description: "Analyze an entire repository, detect structural/logical/security issues, and produce deterministic scored findings with fix priorities."
allowed-tools:
  - "Read"
---

# Skill: Repository Audit

## Purpose
Scan the full repository and produce deterministic, severity-ranked findings.

## Execution Logic
Step 1: Scan repository tree.
- Build map of modules, layers, entry points, and ownership boundaries.

Step 2: Sample key files.
- Prioritize entry points, configuration files, high-churn files, and large files.

Step 3: Detect issues.

Code Issues:
- Functions > 50 lines.
- Deep nesting (>3 levels).
- Duplicated logic patterns.
- Unused imports or variables.

Architecture Issues:
- Missing modular boundaries.
- Tight coupling between components.

Security Issues:
- Hardcoded API keys or secrets.
- Unsafe input handling.

Step 4: Score and report.
- Emit deterministic findings with severity and file location.
- Forward issue counts to scoring-engine logic.

## Detection Logic
- Duplicated logic: equivalent branch/condition shape across multiple files.
- Tight coupling: direct cross-layer dependencies without clear abstraction.
- Unsafe input handling: unsanitized input reaching execution, persistence, or rendering paths.
- Hardcoded secret signal: key/token/password-like literals in source or config.

## Output Contract
### Summary
Deterministic audit overview.

### Quality Score (0-100)
Integer score from scoring-engine.

### Issue List
- [SEVERITY] File:Line -> Problem -> Why it matters
