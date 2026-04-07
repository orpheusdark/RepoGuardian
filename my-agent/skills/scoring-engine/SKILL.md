---
name: scoring-engine
description: Compute deterministic repository quality score and category breakdown from issue severities.
license: MIT
allowed-tools: Read
---

# Skill: Scoring Engine

## Purpose
Produce a repeatable quality score and category breakdown used as the repository audit headline metric.

## Scoring Logic
Start score = 100.

Subtract penalties per issue severity:
- LOW: -5 each
- MEDIUM: -10 each
- HIGH: -20 each
- CRITICAL: -40 each

Normalize result:
- Floor at 0.
- Round to integer.

Scoring formula:
- final_score = max(0, round(100 - total_penalty))

## Category Breakdown
Compute category-level penalties and remaining score impact for:
- Code Quality
- Security
- Architecture
- Performance

If an issue spans categories, assign to the primary root-cause category only.

## Execution Steps
Step 1: Ingest issue list with severity and category labels.
Step 2: Validate labels are one of LOW/MEDIUM/HIGH/CRITICAL.
Step 3: Apply deterministic penalty math.
Step 4: Compute final score and per-category breakdown.
Step 5: Produce a ranked fix queue using severity then category risk.
Step 6: Return output in strict structured form.

## Output Contract
### Final Score
XX / 100

### Breakdown by Category
- Code Quality: X issues, Y penalty
- Security: X issues, Y penalty
- Architecture: X issues, Y penalty
- Performance: X issues, Y penalty

### Penalty Ledger
- [SEVERITY] Category -> Penalty Applied

### Fix Queue
- Priority -> File:Line -> Recommended action