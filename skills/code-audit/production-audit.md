---
name: Production Audit
version: 1.0.0
description: Comprehensive production codebase audit with severity grading (A/B/C/D)
author: Mohammad Faiz
tags: [audit, production, comprehensive, security, quality]
category: code-audit
activation: manual
priority: high
dependencies: [operating-standards]
scope: production
---

# Production Audit

Senior Staff Engineer conducting comprehensive production codebase audit. Identify every defect, fix what can be fixed immediately, flag what requires human judgment. Deliver Grade A codebase or explicitly state what's blocking it.

## Phase 1: Inventory & Triage

Print complete file tree. Categorize: source | config | test | asset | generated | secret | duplicate | dead

**Mark for deletion:**
- Generated: node_modules/, dist/, build/, .next/, __pycache__/, target/
- Temp/cache: *.log, *.tmp, *.pid, .cache/, coverage/, .nyc_output/
- OS/IDE: .DS_Store, Thumbs.db, .idea/, .vscode/settings.json
- Secrets: .env*, *.pem, *.key, *credentials*.json, *adminsdk*.json
- Backups: *.bak, *.orig, *_old.*, *_copy.*, *.swp

Audit order: core logic → data layer → API layer → utilities → UI → config → tests

If codebase >20 files, state batching plan before beginning.

## Phase 2: Audit Checklists

Apply every checkpoint to every file without exception.

**Security (Zero Tolerance)**
Hardcoded secrets, injection vulnerabilities, input validation, output encoding, XSS surfaces, auth gaps, IDOR, JWT flaws, password handling, session issues, CORS misconfiguration, CSRF protection, cookie security, info leakage, PII/token exposure, path traversal, file uploads, rate limiting, ReDoS, dependency CVEs

**Bugs & Logic (Critical)**
Conditionals, boundaries, returns, scope, async, concurrency, loops, null safety, edge cases, type coercion

**Performance (High)**
N+1 queries, missing indexes, redundant computation, blocking main thread, memory leaks, no connection pooling, missing cache, unbounded queries, bundle bloat

**Error Handling (High)**
Uncovered I/O, silent failures, vague errors, unhandled rejections, no degradation, missing timeouts, resource leaks

**Code Quality (Medium)**
Dead code, duplication, magic values, function size >40 lines or >3 nesting levels, naming, pattern inconsistency, debug noise, type safety

**API Layer (Medium)**
Status codes, request validation, unbounded responses, response shape, breaking changes

**Data Layer (High)**
Parameterization, transactions, schema drift, destructive migrations, connection leaks

**Config & Environment (Medium)**
Startup validation, secret exposure, dev config in production, scattered config, untyped config

**Architecture (Medium)**
Layer mixing, circular imports, tight coupling, illogical structure, duplicated constants/utilities

## Phase 3: Fix & Verify

Surgical fixes. Don't refactor what isn't broken. Rewrite broken logic correctly—don't patch bugs with extra code. Verify: no regressions, existing behavior preserved, tests still pass. State assumptions required to resolve ambiguity. Update .gitignore for patterns identified.

## Phase 4: Output Format

**Files with issues:**
```
FILE: path/to/file.ext
──────────────────────────────────────────
ISSUE #N | Severity | Category
Location: Line X / function name
Problem:  [Exact issue and why wrong]
Impact:   [What breaks or risk created]
Fix:      [What changed and why]
──────────────────────────────────────────
FIXED FILE: [complete corrected file]
```

**Clean files:**
```
FILE: path/to/file.ext — CLEAN
Checks passed: Security ✓ Bugs ✓ Performance ✓ Quality ✓ [all applicable]
```

**Deleted files:**
```
FILE: path/to/file.ext — DELETED
Category: [Generated / Secret / Dead / Duplicate]
Reason:   [Justification]
Action:   [Added to .gitignore / Removed from repo]
```

## Phase 5: Final Report

**Summary**
- Files audited: XXX
- Files deleted: XXX
- Total issues found: XXX
- Issues fixed: XXX
- Issues requiring decision: XXX

**Severity Breakdown**
Table: Category (Security, Bugs/Logic, Performance, Error Handling, Code Quality, API, Data, Config, Architecture, Cleanup) | Critical | High | Medium | Low

**.gitignore Changes**
List patterns added and justification.

**Requires Human Decision**
- Issue: [Problem]
- File: [Location]
- Why: [Reason requiring judgment]
- Options: [A] [B] [C]

**Blockers to Grade A**
List exactly what remains (only if grade isn't A).

**Final Grade: [A / B / C / D]**
- A = Zero critical/high issues. Deploy immediately.
- B = Zero critical. Minor high issues remain. Review before deploy.
- C = Criticals fixed. Significant high/medium remain. Not production-ready.
- D = Critical issues unresolved. Do not deploy.

## Non-Negotiable Rules

1. No file skipped
2. Output complete fixed files—never partial snippets
3. Don't patch bugs. Rewrite logic correctly.
4. Don't break existing behavior—verify before proceeding
5. Follow existing patterns unless pattern is the bug
6. Comments explain WHY, not WHAT
7. State assumptions before acting
8. No partial delivery—audit every file before final report
9. If codebase too large, state batching plan in Phase 1 and execute consistently
