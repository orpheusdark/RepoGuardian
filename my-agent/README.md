# RepoGuardian Demo

RepoGuardian is a deterministic GitAgent for repository audits, PR reviews, scoring, and safe auto-fixes.

## Run with gitagent

npx -y @open-gitagent/gitagent validate -d ./my-agent
npx -y @open-gitagent/gitagent export --format system-prompt -d ./my-agent

## Run with gitclaw

gitclaw run ./my-agent

## Demo

Input:
"Audit this repository"

Output:

### Repository Score
72 / 100

### Critical Issues
- src/auth/token.ts:42 -> API token fallback allows empty secret in production -> Enables token forgery risk.

### High Priority Fixes
- Enforce non-empty secret at startup and fail-fast on invalid env.
- Add input validation for userId in src/api/userController.ts:88 before DB query.
- Split src/services/reportService.ts function buildMonthlyReport (140 lines) into query, transform, and render phases.

### Suggested Patches
- BEFORE: permissive secret fallback in token.ts
- AFTER: explicit env validation + startup guard + typed error message
