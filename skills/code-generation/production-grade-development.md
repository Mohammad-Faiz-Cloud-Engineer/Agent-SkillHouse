---
name: Production Grade Development
version: 1.0.0
description: Four-phase production code generation with TDD, security, and self-audit
author: Mohammad Faiz
tags: [code-generation, tdd, security, testing, production]
category: code-generation
activation: manual
priority: high
dependencies: [operating-standards]
---

# Production Grade Development

Generate implementation-ready code meeting enterprise security, reliability, and quality standards. Four-phase process: analysis, tests, implementation, self-audit.

## Phase 1: Analysis & Design

**Scope Contract**
- Define exact inputs, transformations, outputs
- List IN-SCOPE and OUT-OF-SCOPE
- State all assumptions clearly

**Interface Definition**
- Function signatures with complete types
- API contracts (request/response/error shapes)
- Consistent error formats

**Edge Case Inventory**
- Empty, null, undefined inputs
- Boundary values (MIN, MAX, just-inside, just-outside)
- Malformed or unexpected types
- Concurrent access if state shared
- Partial failures in multi-step operations

**Architecture Decision** (complex tasks only)
- Pattern chosen + one alternative considered
- Why alternative rejected
- Module structure

**Threat Model** (external input/auth/DB/file access)
- Attack surface: every input point, external call, user-facing surface
- Trust boundaries: what's untrusted until validated
- Mitigation per threat: specific control

**Scale depth to complexity:**
- Simple (utility/script): Skip architecture and threat model
- Medium (module/service): Full analysis except architecture
- Complex (system/API/auth): All five components

## Phase 2: Test Suite

Write tests before implementation. Tests define "done."

**Frameworks:** Jest/Vitest (JS/TS), Pytest (Python), testing (Go), JUnit (Java)

**Unit Tests**
- Happy path
- Null/empty/undefined for every parameter
- Boundary values
- Type mismatches, invalid formats

**Integration Tests** (if applicable)
- Module interaction
- DB operations
- External API success/failure/timeout
- File system errors

**Security Tests** (external input/auth/DB access)
- Injection: SQL, NoSQL, command, LDAP (real payloads)
- XSS: `<script>`, `javascript:`, `onerror=`
- Path traversal: `../../../etc/passwd`
- Oversized input: large strings, deeply nested objects, huge arrays
- Auth bypass: missing/expired/wrong token
- Mass assignment: extra fields
- SSRF: user URLs hitting internal endpoints

**Concurrency Tests** (shared state/parallel operations)
- Simultaneous writes
- Resource exhaustion

## Phase 3: Implementation

Write only code that makes tests pass.

**Structure**
- Max 40 lines per function
- Max 3 levels nesting
- Single responsibility
- Extract constants and types at module level

**Naming**
- Variables: descriptive (user not u, requestTimestamp not ts)
- Functions: verb + noun (validateUserInput, fetchOrderById)
- Booleans: is/has/should/can prefix
- Constants: SCREAMING_SNAKE_CASE with full description
- Zero magic numbers/strings

**Hygiene**
- No commented-out code
- No unused imports/variables/unreachable paths
- No debug output (console.log, print, debugger, dd, var_dump)
- Structured logging OK (logger.info, log.Error)
- Comments explain WHY, code explains WHAT
- No emojis

**Type Safety** (typed languages)
- All params and return types explicit (no implicit any)
- Narrow unknown types with guards, not casts
- Strict mode enabled
- No prototype pollution

**Security (Non-Negotiable)**

*Secrets:* Zero hardcoded API keys, tokens, passwords, certs, credentials. All via env vars or secrets manager. Validate on startup, fail fast if required.

*Input:* Validate type, format, length, range, charset at every entry point. Reject malformed early. Sanitize: escape output, parameterize queries, encode URLs. Check prototype pollution on object merges.

*Database:* Parameterized queries only (no concatenation/interpolation). Use ORM built-in methods. Wrap multi-step writes in transactions. DB user has minimum permissions.

*Web/API:* HTTPS on all external calls. Auth: verify signature, expiry, issuer. Explicit CORS allowlist (never wildcard). Cookies: httpOnly, Secure, SameSite=Strict. Rate limit auth endpoints. Validate user URLs against allowlist before fetching (SSRF prevention). Context-specific output encoding.

*Error Handling:* Never expose stack traces, internal paths, DB schema to clients. Log full context server-side. Return generic message to client, specific detail to logs. Default deny—fail closed.

**Performance & Reliability**
- No blocking sync I/O in async contexts
- All promises awaited or caught (no floating promises)
- Timeout on every external call (network, DB, third-party API)
- Retry with exponential backoff
- Circuit breaker for high-failure external dependencies
- All resources closed: DB connections, file handles, sockets, streams
- Event listeners added and removed in pairs or use once()
- Timers cleared on cleanup
- No N+1 queries (batch or eager load)
- Cache: TTL set, invalidation strategy defined

**Dependencies:** Don't add new dependencies without explicit justification. State dependency, purpose, why standard library insufficient.

## Phase 4: Self-Audit

Before outputting, verify:

| Category | Item | Status |
|----------|------|--------|
| Structure | No function >40 lines | PASS/FAIL/N/A |
| Structure | No nesting >3 levels | PASS/FAIL/N/A |
| Structure | No magic numbers/strings | PASS/FAIL/N/A |
| Structure | No dead code/unused imports | PASS/FAIL/N/A |
| Structure | No debug output in production | PASS/FAIL/N/A |
| Security | Zero hardcoded secrets | PASS/FAIL/N/A |
| Security | All inputs validated at entry | PASS/FAIL/N/A |
| Security | All external calls have error handling + timeout | PASS/FAIL/N/A |
| Security | No sensitive data in logs/errors | PASS/FAIL/N/A |
| Security | DB queries parameterized | PASS/FAIL/N/A |
| Security | Auth tokens verified (signature, expiry, issuer) | PASS/FAIL/N/A |
| Security | SSRF prevention (allowlist for user URLs) | PASS/FAIL/N/A |
| Security | CORS and cookies configured securely | PASS/FAIL/N/A |
| Reliability | All async paths covered by try/catch | PASS/FAIL/N/A |
| Reliability | All resources closed in finally blocks | PASS/FAIL/N/A |
| Reliability | Race conditions identified and addressed | PASS/FAIL/N/A |
| Reliability | Non-critical failures degrade gracefully | PASS/FAIL/N/A |
| Tests | Tests are real and runnable | PASS/FAIL/N/A |
| Tests | Every edge case has test | PASS/FAIL/N/A |
| Tests | Security payloads tested if applicable | PASS/FAIL/N/A |
| Types | No implicit any | PASS/FAIL/N/A |
| Types | All params/returns explicit | PASS/FAIL/N/A |
| Types | Unknown types narrowed, not cast | PASS/FAIL/N/A |

Explain every FAIL with remediation steps.

## Output Format

**1. ANALYSIS**
[Scope, interface definition, edge case inventory, architecture if complex, threat model if security-relevant]

**2. TEST SUITE**
[Complete, runnable tests with framework and setup command]

**3. IMPLEMENTATION**
[Full source files meeting all constraints]

**4. SELF-AUDIT**
[Checklist with status and notes; explain every FAIL]

**5. USAGE EXAMPLE**
[Only for public APIs, exported modules, non-obvious interfaces. Skip for internal helpers.]

## Conflict Resolution

If coding request conflicts with these standards:
1. Apply standards by default
2. State conflict explicitly
3. Offer compliant alternative
4. Deviate only if you explicitly override and acknowledge risk

Now proceed with the coding task. Begin with Phase 1 Analysis.
