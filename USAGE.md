# Usage Guide

This guide explains how to use Agent-SkillHouse skills effectively across different AI platforms.

---

## Table of Contents

1. [Quick Start](#quick-start)
2. [Skill Structure](#skill-structure)
3. [Loading Skills](#loading-skills)
4. [Chaining Skills](#chaining-skills)
5. [Platform-Specific Usage](#platform-specific-usage)
6. [Best Practices](#best-practices)
7. [Common Workflows](#common-workflows)
8. [Troubleshooting](#troubleshooting)

---

## Quick Start

Basic pattern for using any skill:

```
[Load skill content]

Task: [Your specific request]
```

Example:

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Build a REST API endpoint for user authentication with JWT tokens
```

---

## Skill Structure

Every skill follows this structure:

```markdown
---
name: Skill Name
version: 1.0.0
description: What this skill does
tags: [tag1, tag2]
category: foundation|code-generation|code-audit|specialized
dependencies: [other-skills]
---

# Skill Name

[Phases, checklists, rules, output formats...]
```

### Components

**YAML Frontmatter** — Metadata about the skill (name, version, dependencies, tags)

**Phases** — Step-by-step execution workflow

**Checklists** — Comprehensive coverage items to ensure nothing is missed

**Output Formats** — Structured templates for consistent results

**Non-Negotiable Rules** — Quality constraints that must be followed

---

## Loading Skills

### Method 1: File Reference (Kiro)

```
#skills/foundation/operating-standards.md
#skills/code-audit/pre-commit-audit.md

Task: Audit my codebase
```

### Method 2: Direct Copy-Paste

Copy the entire skill content (including YAML frontmatter) into your prompt:

```
---
name: Operating Standards
version: 1.0.0
...
---

# Agent Operating Standards
[rest of content]

Task: [Your request]
```

### Method 3: Skill ID (if supported by your platform)

```
@skill:operating-standards
@skill:production-grade-development

Task: Build a payment processing module
```

---

## Chaining Skills

### Foundation Plus Specialized

Always load foundation skills first:

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Create a secure file upload handler
```

### Multiple Audits

Chain audit skills for comprehensive review:

```
#skills/foundation/operating-standards.md
#skills/code-audit/static-analysis-debug.md
#skills/code-audit/pre-commit-audit.md

Task: Debug and audit this codebase before deployment
```

### Dependency Resolution

Skills with dependencies automatically require their parent skills. Check the YAML frontmatter to see what's needed.

```
# This skill requires operating-standards
#skills/code-audit/production-audit.md

Task: Audit production codebase
```

---

## Platform-Specific Usage

### Kiro AI

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Build user registration API
```

### Claude / ChatGPT / Other Platforms

Copy skill content directly into your prompt:

```
[Paste operating-standards.md content]
[Paste production-grade-development.md content]

Task: Build user registration API
```

### API Integration

```python
import requests

skill_content = open('skills/foundation/operating-standards.md').read()
task = "Build a REST API for user management"

response = requests.post('https://api.ai-service.com/chat', json={
    'messages': [
        {'role': 'system', 'content': skill_content},
        {'role': 'user', 'content': task}
    ]
})
```

---

## Best Practices

### 1. Always Load Foundation First

Good:
```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md
```

Bad:
```
#skills/code-generation/production-grade-development.md
(missing foundation)
```

### 2. Match Skill to Task Complexity

**Simple task** (utility function):
```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Write a function to validate email addresses
```

**Complex task** (full system):
```
#skills/foundation/operating-standards.md
#skills/code-generation/full-project-scaffold.md

Task: Build a complete e-commerce checkout system
```

### 3. Use Audit Skills Sequentially

Step 1 - Debug:
```
#skills/code-audit/static-analysis-debug.md
Task: Find bugs in this code
```

Step 2 - Pre-commit check:
```
#skills/code-audit/pre-commit-audit.md
Task: Final audit before commit
```

### 4. Specify Mode for Dual-Mode Skills

```
#skills/code-generation/full-project-scaffold.md

Task: MODE A - Build a new authentication service
```

or

```
#skills/code-generation/full-project-scaffold.md

Task: MODE B - Audit existing authentication service
```

### 5. Provide Context

```
#skills/code-audit/production-audit.md

Context:
- Language: TypeScript
- Framework: Express.js
- Database: PostgreSQL
- Current issues: Memory leaks in production

Task: Audit this codebase
```

---

## Common Workflows

### Workflow 1: New Feature Development

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Build a real-time notification system with WebSockets
```

### Workflow 2: Bug Investigation

```
#skills/foundation/operating-standards.md
#skills/code-audit/static-analysis-debug.md

Task: Find the root cause of race conditions in the payment processor
```

### Workflow 3: Pre-Deployment Audit

```
#skills/foundation/operating-standards.md
#skills/code-audit/pre-commit-audit.md

Task: Final security and quality check before pushing to GitHub
```

### Workflow 4: Production Incident

```
#skills/foundation/operating-standards.md
#skills/code-audit/static-analysis-debug.md

Task: Analyze this production error log and identify the bug
```

### Workflow 5: Full Project Scaffold

```
#skills/foundation/operating-standards.md
#skills/code-generation/full-project-scaffold.md

Task: MODE A - Create a complete REST API for a task management system
Requirements:
- User authentication (JWT)
- CRUD operations for tasks
- PostgreSQL database
- Express.js framework
- TypeScript
```

### Workflow 6: UI/UX Design

```
#skills/specialized/ui-ux-design.md

Task: Design and build a landing page hero section for a SaaS product
Requirements:
- Bold, modern personality
- Clear visual hierarchy
- Animated interactions
- Mobile-responsive
- Dark mode support
```

---

## Troubleshooting

### Issue: Agent ignores skill instructions

**Solution:** Ensure skill is loaded before the task. Load order matters.

Correct:
```
Load skill first
Then task
```

Incorrect:
```
Task first
Then skill
```

### Issue: Incomplete output

**Solution:** Check if foundation skill is loaded. Most specialized skills depend on it.

```
#skills/foundation/operating-standards.md
[other skills]
```

### Issue: Wrong output format

**Solution:** Verify you're using the correct skill for your task type.

- Code generation → `code-generation/`
- Code review → `code-audit/`
- Specialized tasks → `specialized/`

### Issue: Dependencies not resolved

**Solution:** Manually load dependency skills. Check YAML frontmatter for required dependencies.

```
#skills/foundation/operating-standards.md  (dependency)
#skills/code-audit/production-audit.md     (main skill)
```

---

## Advanced Usage

### Custom Skill Combinations

Create your own workflow by combining skills:

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md
#skills/code-audit/static-analysis-debug.md

Task: Build a payment processor, then audit it for bugs
```

### Skill Overrides

Override specific rules when needed (use sparingly):

```
#skills/code-generation/production-grade-development.md

Override: Skip Phase 2 (tests) for this prototype

Task: Quick prototype of a recommendation algorithm
```

### Context Injection

Provide additional context for better results:

```
#skills/code-audit/production-audit.md

Project Context:
- Monorepo with 50+ microservices
- Node.js + TypeScript
- High-traffic production (1M+ requests/day)
- Recent security audit flagged 3 critical issues

Task: Comprehensive audit focusing on security and performance
```

---

## Skill Catalog Quick Reference

| Skill | Category | Use When |
|-------|----------|----------|
| operating-standards | Foundation | Every task (load first) |
| production-grade-development | Code Gen | Building new features/modules |
| full-project-scaffold | Code Gen | Starting new projects or full audits |
| pre-commit-audit | Audit | Before pushing to GitHub |
| production-audit | Audit | Reviewing production code |
| static-analysis-debug | Audit | Finding bugs through code analysis |
| image-enhancement | Specialized | AI image processing tasks |
| ui-ux-design | Specialized | Building designer-grade interfaces |

---

## Getting Help

- **Skill not working?** Check dependencies in YAML frontmatter
- **Unexpected output?** Verify you loaded the foundation skill
- **Need a new skill?** See CONTRIBUTING.md
- **Questions?** Open an issue in the repository

---

## Next Steps

1. Browse the skills catalog in README.md
2. Try the quick start examples above
3. Explore common workflows
4. Create your own skill combinations
5. Contribute new skills to the repository
