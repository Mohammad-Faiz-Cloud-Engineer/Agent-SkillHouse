---
name: Commit Message Generator
version: 1.0.0
description: Professional commit message generation following Conventional Commits with context-aware formatting
author: Mohammad Faiz
tags: [git, commit, conventional-commits, version-control]
category: code-generation
activation: manual
priority: medium
dependencies: []
---

# Commit Message Generator

Generates professional commit messages following Conventional Commits specification. Analyzes changes and produces clear, contextual messages with appropriate detail levels.

## Message Structure

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Commit Types

- `feat` - New feature or capability
- `fix` - Bug fix or correction
- `docs` - Documentation only
- `refactor` - Code restructuring without behavior change
- `perf` - Performance improvement
- `test` - Test additions or modifications
- `build` - Build system or dependency changes
- `ci` - CI/CD configuration
- `style` - Code formatting (no logic change)
- `chore` - Maintenance tasks

**Breaking Changes:** Add `!` after type/scope: `feat!:` or `feat(api)!:` + include `BREAKING CHANGE:` footer

## Description Guidelines

**Length:** 50-72 characters maximum

**Voice:** Imperative present tense
- Good: "add user authentication"
- Bad: "added authentication", "adds auth"

**Content:** What changed, not how
- Good: "add JWT token validation"
- Bad: "create new function validateToken in auth.js"

**Format:**
- Lowercase after colon (unless proper noun)
- No period at end
- Concise and specific

## Body Guidelines

**Include body when:**
- Non-obvious reasoning or context
- Breaking changes with migration path
- Security implications
- Performance impact details
- Complex refactoring rationale
- Issue/PR references needed

**Skip body when:**
- Self-explanatory changes
- Simple bug fixes
- Obvious refactoring
- Documentation updates

**Format:**
- Blank line after description
- Wrap at 72 characters
- Use bullet points for lists
- Explain why, not what (diff shows what)

## Scope Usage

**Use scope for:**
- Multi-module projects
- Clear component boundaries
- Changelog generation
- Team convention

**Common scopes:** `api`, `auth`, `db`, `ui`, `cli`, `config`, `deps`

**Skip scope for:**
- Single-module projects
- Cross-cutting changes
- Unclear boundaries

## Footer Format

**Issue references:**
```
Closes #123
Fixes #456
Refs #789
```

**Breaking changes:**
```
BREAKING CHANGE: API endpoint /v1/users renamed to /v2/users.
Update all client calls before June 2026.
```

**Co-authors:**
```
Co-authored-by: Name <email@example.com>
```

## Examples

### Simple Feature
```
feat(auth): add password reset functionality
```

### Bug Fix with Context
```
fix(api): prevent race condition in order processing

Multiple concurrent requests could create duplicate orders.
Added transaction locking to ensure atomic order creation.

Fixes #234
```

### Breaking Change
```
feat(api)!: change user endpoint response format

BREAKING CHANGE: GET /api/users now returns array under
'data' key instead of root array.

Before: response[0].name
After: response.data[0].name

Closes #456
```

### Performance
```
perf(search): add database index on user.email

Reduces search query time from 2.3s to 45ms for
10M user database. Adds 50MB to index size.
```

### Security Fix
```
fix(auth): prevent SQL injection in login

Parameterized all database queries in authentication
flow. Previous string concatenation allowed injection.

Security advisory: INTERNAL-2026-001
```

### Revert
```
revert: feat(api): add user preferences endpoint

This reverts commit abc123def456.

Endpoint causing performance issues in production.
Will reimplement with caching in next sprint.
```

## Analysis Process

1. **Examine Changes** - Review diff to understand scope and impact
2. **Identify Type** - Determine primary commit type
3. **Extract Scope** - Identify affected component (if applicable)
4. **Write Description** - Concise imperative summary
5. **Evaluate Body Need** - Decide if context required
6. **Add Footers** - Include references and metadata
7. **Verify Format** - Check length, grammar, convention

## Quality Checklist

- [ ] Type is accurate and follows convention
- [ ] Description is imperative present tense
- [ ] Description length ≤72 characters
- [ ] No period at end of description
- [ ] Body explains why (if included)
- [ ] Body wrapped at 72 characters
- [ ] Breaking changes documented in footer
- [ ] Issues referenced correctly
- [ ] No spelling or grammar errors
- [ ] No implementation details in description
- [ ] Scope is accurate (if used)

## Context Awareness

**Small Changes (1-5 lines):** Description only, no body unless security/breaking

**Medium Changes (5-50 lines):** Description + scope, body if reasoning non-obvious

**Large Changes (50+ lines):** Description + scope + body with context, consider splitting

**Breaking Changes:** Always include body and footer with migration path

**Security Changes:** Always include body, reference advisory if exists

## Rules

1. **Follow Conventional Commits** - Type, scope, description format
2. **Imperative mood** - "add" not "added" or "adds"
3. **Lowercase description** - Unless proper noun
4. **No period** - At end of description
5. **Explain why** - In body, not what (diff shows what)
6. **72 character wrap** - For description and body
7. **Breaking changes** - Always documented with migration
8. **Security fixes** - Always include context
9. **Issue references** - At end of body or in footer
10. **One concern** - Per commit when possible

## What to Avoid

- Implementation details in description
- Vague descriptions ("update code", "fix bug")
- Past tense ("added", "fixed")
- Personal pronouns ("I", "we")
- AI attribution or tool mentions
- Emoji (unless project convention)
- Redundant information from diff
- Overly verbose explanations
- Unrelated changes in one commit

## Project Convention Detection

Check for existing patterns and match detected convention:
- Capitalization style
- Scope usage frequency
- Body inclusion rate
- Footer format preferences
- Type preferences

## Integration

**Git Hooks:** Can be used with `prepare-commit-msg` hook

**CI/CD:** Validate with commitlint or similar

**Changelog:** Enables automated changelog generation

**Semantic Versioning:** Commit types determine version bumps (feat=minor, fix=patch, breaking=major)

Generates commit message only. Does not execute git commands or stage files.
