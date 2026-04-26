---
name: Code Review
version: 1.0.0
description: Structured code review with clear severity levels and actionable feedback
author: Mohammad Faiz
tags: [code-review, pull-request, feedback, quality]
category: code-audit
activation: manual
priority: high
dependencies: [operating-standards]
---

# Code Review

Structured code review providing clear, actionable feedback. Every comment includes location, issue, and fix.

## Comment Structure

**Format:** `[Severity] File:Line - Issue. Fix: Solution.`

**Severity Levels:**
- **CRITICAL** - Blocks merge. Security, data loss, production-breaking bugs.
- **HIGH** - Must address. Logic errors, race conditions, memory leaks.
- **MEDIUM** - Should fix. Duplication, missing validation, poor structure.
- **LOW** - Optional. Style, minor optimizations, suggestions.
- **QUESTION** - Needs clarification or discussion.

## Review Checklist

**Security**
- Hardcoded secrets, injection vulnerabilities, missing auth, unvalidated input, exposed sensitive data, insecure configurations

**Correctness**
- Logic errors, edge cases, error handling, off-by-one, async issues, race conditions, incorrect return values

**Performance**
- N+1 queries, missing indexes, unnecessary loops, unclosed resources, memory leaks, blocking operations

**Quality**
- Functions >40 lines, nesting >3 levels, magic numbers, dead code, debug statements, inconsistent patterns

**Testing**
- Missing tests, uncovered edge cases, unclear test names, disabled tests

## Comment Examples

**Critical:**
```
[CRITICAL] auth.js:42 - SQL injection. User input in query string.
Fix: Use parameterized query: db.query('SELECT * FROM users WHERE id = ?', [userId])
```

**High:**
```
[HIGH] payment.js:156 - Unhandled promise rejection. Will crash on API failure.
Fix: Wrap stripe.charges.create() in try/catch with error handling.
```

**Medium:**
```
[MEDIUM] utils.js:23 - Function handles validation, transform, and persistence.
Fix: Split into validateUser(), transformUser(), saveUser().
```

**Low:**
```
[LOW] config.js:8 - Magic number 3600 without context.
Fix: const SESSION_TIMEOUT_SECONDS = 3600
```

**Question:**
```
[QUESTION] api.js:67 - Why retry 5 times instead of 3? Seems high for this endpoint.
```

## Review Process

1. **Scan** - Read PR description, check tests, verify CI
2. **Review** - Apply checklist to each file
3. **Categorize** - Group findings by severity
4. **Document** - Write clear, actionable comments
5. **Summarize** - Count issues, recommend merge decision

## Output Format

```
## Review Summary

Files reviewed: X
Issues found: Critical (X), High (X), Medium (X), Low (X)
Recommendation: [APPROVE / REQUEST CHANGES / DISCUSS]

---

## Critical Issues

[CRITICAL] file:line - Issue
Fix: Solution

---

## High Priority

[HIGH] file:line - Issue
Fix: Solution

---

## Medium Priority

[MEDIUM] file:line - Issue
Fix: Solution

---

## Suggestions

[LOW] file:line - Suggestion
Fix: Optional improvement

---

## Questions

[QUESTION] file:line - Question

---

## Positive Notes

file:line - Good pattern or implementation
```

## Special Handling

**Security Issues**
- Full explanation with attack scenario
- Specific fix with code example
- Link to security best practices

**Architecture Concerns**
- Explain current approach
- State concern with rationale
- Propose alternative
- Suggest discussion if significant

**New Team Members**
- Add context and explanation
- Link to relevant docs
- Explain team patterns
- Maintain encouraging tone

**Large PRs**
- Review by module/feature
- Summarize repeated patterns
- Suggest splitting if too large

## Review Modes

**Standard** - Full checklist, all severity levels, detailed feedback
**Security** - Deep security focus, threat analysis, compliance check
**Performance** - Optimization focus, query analysis, resource usage
**Quick** - Critical and high only, minimal detail, fast turnaround

## Rules

1. **Be specific** - Exact line numbers, symbol names, concrete fixes
2. **Be actionable** - Tell what to do, not just what's wrong
3. **Be respectful** - Focus on code, not coder
4. **Explain why** - Especially for non-obvious issues
5. **Acknowledge good work** - Note positive patterns
6. **Ask when uncertain** - Questions better than wrong assumptions
7. **Prioritize correctly** - Critical blocks merge, low is optional
8. **Stay consistent** - Apply same standards to all code
9. **No nitpicking** - Style issues are low priority
10. **Security first** - Never compromise on security

## What to Avoid

- Vague feedback ("this could be better")
- Restating what code does (reviewer can read)
- Hedging language ("maybe", "perhaps", "I think")
- Excessive praise in every comment
- Suggesting refactors without clear benefit
- Blocking on personal preferences
- Commenting on auto-formatted code
- Repeating same issue multiple times

## What to Include

- Exact location (file and line)
- Clear problem statement
- Specific solution
- Reason why (if not obvious)
- Code example (if helpful)
- Alternative approaches (if applicable)

Review is collaborative. Goal is better code through constructive feedback.
