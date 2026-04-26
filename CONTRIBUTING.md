# Contributing to Agent-SkillHouse

Thank you for contributing. This guide will help you create high-quality skills that follow repository standards.

---

## Table of Contents

1. [Skill Creation Checklist](#skill-creation-checklist)
2. [Skill Template](#skill-template)
3. [YAML Frontmatter Reference](#yaml-frontmatter-reference)
4. [Skill Structure Guidelines](#skill-structure-guidelines)
5. [Testing Your Skill](#testing-your-skill)
6. [Submission Process](#submission-process)

---

## Skill Creation Checklist

Before submitting a new skill, verify:

- [ ] YAML frontmatter is complete and valid
- [ ] Skill name is descriptive and follows kebab-case
- [ ] Category is appropriate (foundation/code-generation/code-audit/specialized)
- [ ] Dependencies are listed if skill requires other skills
- [ ] Phases are clearly defined with numbered steps
- [ ] Checklists are comprehensive and actionable
- [ ] Output format is structured and consistent
- [ ] Non-negotiable rules are present
- [ ] Skill has been tested with sample tasks
- [ ] README.md is updated with new skill entry
- [ ] skills-manifest.json is updated

---

## Skill Template

Use this template when creating a new skill:

```markdown
---
name: Your Skill Name
version: 1.0.0
description: One-sentence description of what this skill does
author: Your Name or Organization
tags:
  - relevant-tag-1
  - relevant-tag-2
  - relevant-tag-3
category: foundation|code-generation|code-audit|specialized
activation: manual
priority: low|medium|high|critical
dependencies:
  - operating-standards
---

# Your Skill Name

Brief introduction explaining the skill's purpose and when to use it.

---

## PHASE 1: [Phase Name]

Clear description of what happens in this phase.

**Steps:**
1. First step with specific action
2. Second step with specific action
3. Third step with specific action

**Checklist:**
- [ ] Item to verify
- [ ] Another item to verify
- [ ] Final verification item

---

## PHASE 2: [Phase Name]

Description of second phase.

**Checklist:**

**CRITICAL ITEMS**
- Item that blocks progression
- Another blocking item

**HIGH PRIORITY**
- Important but not blocking
- Another high priority item

**MEDIUM PRIORITY**
- Nice to have
- Another medium item

---

## PHASE 3: [Phase Name]

Description of third phase.

---

## OUTPUT FORMAT

Specify exactly how the agent should structure its output:

```
[Example output structure]
```

For files with issues:
```
FILE: path/to/file.ext
──────────────────────────────────────────
ISSUE #N | Severity | Category
Location: [Where]
Problem:  [What]
Impact:   [Why it matters]
Fix:      [How to resolve]
──────────────────────────────────────────
FIXED FILE: [complete corrected file]
```

---

## NON-NEGOTIABLE RULES

1. Rule that must never be violated
2. Another absolute requirement
3. Critical constraint
4. Quality standard
5. Security requirement
6. Output requirement
7. Process requirement
8. Verification requirement
9. Scope requirement
10. Delivery requirement

---

## CONFLICT RESOLUTION

If a user request conflicts with these standards:
1. Apply the standards by default
2. State the conflict explicitly
3. Offer a compliant alternative
4. Deviate only with explicit user override
```

---

## YAML Frontmatter Reference

### Required Fields

```yaml
name: string           # Human-readable skill name
version: string        # Semantic version (1.0.0)
description: string    # One-sentence description
category: string       # One of: foundation, code-generation, code-audit, specialized
```

### Optional Fields

```yaml
author: string         # Creator name or organization
tags: array           # List of relevant tags
activation: string    # manual (default) or auto
priority: string      # low, medium, high, critical
dependencies: array   # List of required skill IDs
scope: string         # Specific scope (e.g., pre-commit, production)
modes: array          # Available modes (e.g., [build, audit])
```

### Example

```yaml
---
name: API Security Audit
version: 1.0.0
description: Comprehensive security audit for REST APIs
author: Security Team
tags:
  - security
  - api
  - audit
  - rest
category: code-audit
activation: manual
priority: critical
dependencies:
  - operating-standards
scope: api-security
---
```

---

## Skill Structure Guidelines

### 1. Clear Phases

Break the skill into logical phases:

```markdown
## PHASE 1: PREPARATION
[What to do before starting]

## PHASE 2: EXECUTION
[Main work happens here]

## PHASE 3: VERIFICATION
[Check the work]

## PHASE 4: DELIVERY
[Output format]
```

### 2. Actionable Checklists

Use severity indicators:

```markdown
**CRITICAL** — Blocks progression
- Item that must be addressed
- Another blocking item

**HIGH** — Important but not blocking
- High priority item
- Another important item

**MEDIUM** — Should be addressed
- Medium priority item

**LOW** — Nice to have
- Low priority item
```

### 3. Structured Output Formats

Provide templates:

```markdown
## OUTPUT FORMAT

**For successful completion:**
```
RESULT: [Summary]
STATUS: SUCCESS
DETAILS:
  - Item 1
  - Item 2
```

**For issues found:**
```
ISSUE: [Description]
SEVERITY: [Critical/High/Medium/Low]
LOCATION: [Where]
FIX: [How to resolve]
```
```

### 4. Non-Negotiable Rules

Always include 5-10 absolute rules:

```markdown
## NON-NEGOTIABLE RULES

1. No file gets skipped
2. Output complete files, never snippets
3. Fix root causes, not symptoms
4. State assumptions before acting
5. No partial delivery
```

### 5. Conflict Resolution

Handle edge cases:

```markdown
## CONFLICT RESOLUTION

If a user request conflicts with these standards:
1. Apply the standards by default
2. State the conflict explicitly
3. Offer a compliant alternative
4. Deviate only with explicit user override
```

---

## Testing Your Skill

### Test Cases

Create at least 3 test cases:

1. **Simple Task**: Basic usage
2. **Complex Task**: Full capability demonstration
3. **Edge Case**: Unusual or challenging scenario

### Example Test

```markdown
# Test Case 1: Simple Task

Skill: production-grade-development.md
Task: Create a function to validate email addresses

Expected Output:
- Phase 1: Analysis with scope, interface, edge cases
- Phase 2: Complete test suite
- Phase 3: Implementation
- Phase 4: Self-audit checklist
- Phase 5: Usage example

Actual Output: [Record results]
Pass/Fail: [Mark result]
```

### Validation Checklist

- [ ] Skill loads without errors
- [ ] All phases execute in order
- [ ] Output matches specified format
- [ ] Non-negotiable rules are enforced
- [ ] Dependencies are resolved correctly
- [ ] Edge cases are handled
- [ ] Conflict resolution works

---

## Submission Process

### 1. Create the Skill File

```bash
# Create in appropriate category folder
touch skills/code-audit/your-skill-name.md
```

### 2. Add YAML Frontmatter

```markdown
---
name: Your Skill Name
version: 1.0.0
description: What it does
category: code-audit
tags: [tag1, tag2]
dependencies: [operating-standards]
---
```

### 3. Write Skill Content

Follow the template and structure guidelines above.

### 4. Update skills-manifest.json

```json
{
  "id": "your-skill-name",
  "name": "Your Skill Name",
  "path": "code-audit/your-skill-name.md",
  "category": "code-audit",
  "version": "1.0.0",
  "description": "What it does",
  "tags": ["tag1", "tag2"],
  "priority": "medium",
  "activation": "manual",
  "dependencies": ["operating-standards"]
}
```

### 5. Update README.md

Add entry to the Skills Catalog section:

```markdown
**`your-skill-name.md`** — Brief description
- Key feature 1
- Key feature 2
- **When to use:** When to use this skill
```

### 6. Test Thoroughly

Run all test cases and validate output.

### 7. Submit Pull Request

Include:
- Skill file
- Updated skills-manifest.json
- Updated README.md
- Test results
- Example usage

---

## Skill Categories

### Foundation
Core operating principles that apply to all tasks. Must be loaded first. No dependencies on other skills. Establishes quality bar.

### Code Generation
Skills for building new code from scratch. Typically depends on foundation skills. Includes TDD, security, testing. Produces complete, runnable code.

### Code Audit
Skills for reviewing and fixing existing code. Depends on foundation skills. Includes security, bugs, performance. Produces fixed files and reports.

### Specialized
Domain-specific skills for unique tasks. May or may not depend on foundation. Highly focused on specific domain. Clear scope boundaries.

---

## Best Practices

### Do

- Use clear, descriptive names
- Break complex skills into phases
- Provide comprehensive checklists
- Include structured output formats
- State non-negotiable rules
- Test with multiple scenarios
- Document dependencies
- Use severity indicators (CRITICAL/HIGH/MEDIUM/LOW)

### Don't

- Create overly broad skills
- Skip YAML frontmatter
- Use vague instructions
- Omit output format specifications
- Forget to update manifest
- Submit untested skills
- Mix multiple concerns in one skill
- Use ambiguous language

---

## Examples of Good Skills

### Example 1: Focused Scope

```markdown
---
name: SQL Injection Audit
version: 1.0.0
description: Detect and fix SQL injection vulnerabilities
category: code-audit
tags: [security, sql, injection]
---

# SQL Injection Audit

Focused specifically on SQL injection detection and remediation.
```

### Example 2: Clear Phases

```markdown
## PHASE 1: DETECTION
Scan all database queries for string concatenation

## PHASE 2: ANALYSIS
Classify each finding by severity

## PHASE 3: REMEDIATION
Convert to parameterized queries

## PHASE 4: VERIFICATION
Confirm all queries are safe
```

### Example 3: Actionable Checklist

```markdown
**CRITICAL**
- [ ] No string concatenation in queries
- [ ] All user input parameterized
- [ ] No dynamic table/column names from user input

**HIGH**
- [ ] ORM used correctly
- [ ] Prepared statements for all queries
```

---

## Questions?

- Check existing skills for examples
- Review the USAGE.md guide
- Open an issue for clarification
- Join discussions in pull requests

---

## License

By contributing, you agree that your contributions will be licensed under the BSD 2-Clause License.

Copyright (c) 2026, Mohammad Faiz
