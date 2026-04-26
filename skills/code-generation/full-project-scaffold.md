---
name: Full Project Scaffold
version: 1.0.0
description: Dual-mode skill for building new projects (Mode A) or auditing existing code (Mode B)
author: Mohammad Faiz
tags: [code-generation, audit, project-scaffold, dual-mode, comprehensive]
category: code-generation
activation: manual
priority: high
dependencies: [operating-standards]
modes: [build, audit]
---

# Full Project Scaffold

Dual-mode: Build new projects (Mode A) or audit existing code (Mode B). Scales complexity automatically.

Detect mode from request. If unclear, ask before proceeding.

**Complexity Scaling:**
- Simple (utility/script): Skip ADR and threat model
- Medium (module/service): Full analysis minus ADR
- Complex (system/API/auth): All phases, no shortcuts

---

## MODE A: BUILD NEW CODE

### Phase A1: Analysis

**Scope Contract**
- Exact inputs, transformations, outputs
- IN-SCOPE and OUT-OF-SCOPE boundaries
- All assumptions stated upfront

**Interface Definition**
- Full function signatures with types
- API contract: request/response/error shapes
- Consistent error format

**Edge Case Inventory**
- Empty/null/undefined for every parameter
- Boundary values: MIN, MAX, just-inside, just-outside
- Malformed or unexpected types
- Concurrent access (if shared state)
- Partial failure scenarios

**Architecture Decision** (complex only)
- Pattern chosen + one alternative rejected
- Module structure and data flow

**Threat Model** (external input/auth/DB/file access)
- Attack surface: every input point, external call
- Trust boundaries: what's untrusted until validated
- Mitigation per threat: specific control

### Phase A2: Tests (Write Before Implementation)

Use real framework: Jest/Vitest (JS/TS), Pytest (Python), testing (Go), JUnit (Java)

**Unit Tests**
- Happy path
- Null/empty/undefined for every param
- Boundary values
- Type mismatches, malformed input
- Special characters, encoding edge cases

**Integration Tests** (if applicable)
- Data flow between layers
- DB: read, write, transaction rollback
- External API: success + failure + timeout
- File system: ENOENT, EACCES, missing files

**Security Tests** (if external input/auth/DB)
- Injection: SQL, NoSQL, command, LDAP (real payloads)
- XSS: `<script>`, `javascript:`, `onerror=`
- Path traversal: `../../../etc/passwd`
- Oversized input: huge strings, deep nesting, large arrays
- Auth bypass: missing/expired/wrong token
- Mass assignment: extra fields
- SSRF: user URLs targeting internal endpoints

**Concurrency Tests** (if shared state)
- Simultaneous writes
- Connection pool exhaustion

### Phase A3: Implementation

Write only code that makes tests pass.

**Structure**
- Function max: 40 lines
- Nesting max: 3 levels
- Single responsibility
- Constants/types/helpers extracted

**Naming**
- Variables: descriptive (user not u)
- Functions: verb + noun (validateUserInput)
- Booleans: is/has/should/can prefix
- Constants: SCREAMING_SNAKE_CASE with full description
- Zero magic numbers/strings

**Hygiene**
- No commented-out code
- No unused imports/variables/unreachable paths
- No debug output (console.log, print, debugger, dd, var_dump)
- Structured logging OK (logger.info, log.Error)
- Comments explain WHY, code explains WHAT

**Type Safety** (typed languages)
- No implicit any
- Narrow unknown types with guards
- Strict mode on
- No prototype pollution

**Security**
- Secrets: Zero hardcoded. All via env vars. Validate on startup.
- Input: Validate type/format/length/range/charset at entry. Reject early.
- Database: Parameterized queries only. Transactions for multi-step writes.
- Web/API: HTTPS only. Verify auth signature/expiry/issuer. Explicit CORS allowlist. Cookies: httpOnly, Secure, SameSite=Strict. Rate limit auth endpoints. SSRF: allowlist user URLs.
- Error handling: Never expose stack traces/paths/schema to client. Log full context server-side.

**Performance & Reliability**
- No blocking sync I/O in async contexts
- All promises awaited or caught
- Timeouts on every external call
- Retry with exponential backoff
- All resources closed: connections, handles, sockets, streams
- Event listeners added and removed in pairs
- Timers cleared on cleanup
- No N+1 queries
- No new dependency without justification + CVE check

### Phase A4: Self-Audit

Mark PASS, FAIL, or N/A:

**Structure**
- [ ] No function >40 lines
- [ ] No nesting >3 levels
- [ ] No magic numbers/strings
- [ ] No dead code/unused imports
- [ ] No debug output in production

**Security**
- [ ] Zero hardcoded secrets
- [ ] All inputs validated at entry
- [ ] All external calls have error handling + timeout
- [ ] No sensitive data in logs/errors
- [ ] DB queries parameterized
- [ ] Auth tokens: signature/expiry/issuer verified
- [ ] SSRF: user URLs allowlisted
- [ ] CORS and cookies configured securely

**Reliability**
- [ ] All async paths covered by try/catch
- [ ] All resources closed in finally blocks
- [ ] Race conditions addressed
- [ ] Non-critical failures degrade gracefully

**Tests**
- [ ] All tests real and runnable
- [ ] Every edge case has test
- [ ] Security payloads tested

**Types** (typed languages)
- [ ] No implicit any
- [ ] All params/returns explicitly typed
- [ ] Unknown types narrowed with guards

---

## MODE B: AUDIT EXISTING CODE

### Phase B1: Inventory

1. Print full file tree
2. Categorize: source | config | test | asset | generated | secret | duplicate | dead
3. Flag for deletion:
   - Secrets: .env*, *.pem, *.key, *.cert, credentials.json, adminsdk*.json
   - Generated: node_modules/, dist/, build/, .next/, __pycache__/, target/
   - Temp: *.log, *.tmp, .cache/, coverage/, .nyc_output/
   - OS/IDE: .DS_Store, .idea/, .vscode/settings.json (personal)
   - Dead: *.bak, *.orig, *_old.*, scratch.*, TODO.txt
4. Audit order: core logic → data layer → API → utilities → UI → config → tests
5. If >20 files, state batch plan before starting

### Phase B2: Checklists (Every File)

**Security (Zero Tolerance)**
- Hardcoded secrets, injection, input validation, output encoding, XSS, auth gaps, IDOR, JWT flaws, password handling, session issues, CORS, CSRF, cookie security, info leakage, PII/tokens in logs, path traversal, file uploads, rate limiting, ReDoS, SSRF, prototype pollution, dependency CVEs

**Bugs & Logic (Critical)**
- Wrong operators, boundaries, returns, scope, async, concurrency, loops, null safety, edge cases, type coercion

**Performance (High)**
- N+1 queries, missing indexes, redundant computation, blocking main thread, memory leaks, no connection pooling, missing cache, unbounded queries, bundle bloat

**Error Handling (High)**
- Uncovered I/O, silent failures, vague errors, unhandled rejections, no degradation, missing timeouts, resource leaks

**Code Quality (Medium)**
- Dead code, duplication, magic values, function size >40 lines, nesting >3 levels, misleading names, pattern inconsistency, debug noise, unjustified any types

**API Layer (Medium)**
- Wrong status codes, missing request validation, unbounded responses, inconsistent response shape

**Data Layer (High)**
- Queries using string interpolation, multi-step writes not atomic, connections not closed

**Config & Environment (Medium)**
- Required env vars not validated on startup, debug mode in production, scattered config, .env.example missing

**Architecture (Medium)**
- Layer mixing, circular imports, tight coupling, illogical structure, duplicated constants/utilities

### Phase B3: Fix & Verify

- Surgical fixes only
- Fix root cause, not symptoms
- State assumptions before acting
- Verify no regression
- No new dependencies without justification
- No placeholders

### Output Format

**Files with issues:**
```
FILE: path/to/file.ext
──────────────────────────────────────────
ISSUE #N | Severity | Category
Location: Line X / function name
Problem:  [Exact issue]
Impact:   [What breaks]
Fix:      [What changed]
──────────────────────────────────────────
FIXED FILE: [complete corrected file]
```

**Clean files:**
```
FILE: path/to/file.ext — CLEAN
Checks passed: Security ✓ Bugs ✓ Performance ✓ Quality ✓
```

**Deleted files:**
```
FILE: path/to/file.ext — DELETED
Category: [Secret / Generated / Dead / Duplicate]
Reason:   [Justification]
Action:   [Added to .gitignore / Removed from tracking]
```

### Final Report

**Summary**
- Files audited: XXX
- Files deleted: XXX
- Total issues found: XXX
- Issues fixed: XXX
- Issues requiring decision: XXX

**Severity Breakdown**
Table with categories (Security, Bugs/Logic, Performance, Error Handling, Code Quality, API, Data, Config, Architecture) and severity columns (Critical, High, Medium, Low).

**Requires Human Decision**
- Issue: [Problem]
- File: [Location]
- Why: [Reason needing judgment]
- Options: [A] [B] [C]

**Blockers to Grade A**
List what remains (only if grade isn't A).

**Final Grade: [A / B / C / D]**
- A = Zero critical/high issues. Production-ready.
- B = Zero critical. Minor high issues remain. Review before deploy.
- C = Criticals fixed. High/medium remain. Not production-ready.
- D = Critical issues unresolved. Do not deploy.

---

## Non-Negotiable Rules

1. Detect mode from request. Ask if unclear.
2. State assumptions explicitly before acting.
3. No file skipped. No partial output. No snippets.
4. Fix root causes, not symptoms.
5. Don't touch working code. Only fix confirmed issues.
6. Follow existing patterns unless pattern is the bug.
7. No new dependencies without justification.
8. Comments explain WHY, code explains WHAT.
9. No debug output in any production path.
10. No placeholder implementations or TODO fixes.
11. If codebase too large, state batching plan in Phase B1.
12. Mode B: static analysis only. Don't claim to have run code.

## Conflict Resolution

If request conflicts with standards:
1. Apply standards by default
2. State conflict explicitly
3. Offer compliant alternative
4. Deviate only if user explicitly overrides
