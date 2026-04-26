# Agent-SkillHouse

**Where AI agents master their craft**

Agent-SkillHouse is a collection of structured instruction sets designed to transform how AI coding agents work. Each skill is a carefully crafted markdown file that provides detailed protocols, comprehensive checklists, and quality standards for specific engineering tasks.

Think of these as expert-level playbooks. When you load a skill, you're essentially giving an AI agent years of production engineering experience in a specific domain.

---

## What is a Skill?

A skill is a specialized instruction set that changes how an AI agent approaches a task. Instead of generic responses, you get production-grade output that follows industry best practices.

Each skill includes:
- **Structured metadata** via YAML frontmatter (name, version, dependencies, tags)
- **Clear execution phases** with step-by-step workflows
- **Comprehensive checklists** so nothing gets missed
- **Consistent output formats** for predictable results
- **Non-negotiable rules** that enforce quality standards

---

## Repository Structure

```
.
├── CHANGELOG.md                    # Version history
├── CONTRIBUTING.md                 # How to add new skills
├── LICENSE                         # MIT License
├── QUICK-REFERENCE.md             # Fast lookup guide
├── README.md                       # This file
├── USAGE.md                        # Detailed usage examples
└── skills/
    ├── foundation/                 # Core operating principles
    │   └── operating-standards.md
    ├── code-generation/            # Building new code
    │   ├── full-project-scaffold.md
    │   └── production-grade-development.md
    ├── code-audit/                 # Reviewing existing code
    │   ├── pre-commit-audit.md
    │   ├── production-audit.md
    │   └── static-analysis-debug.md
    ├── specialized/                # Domain-specific skills
    │   ├── image-enhancement.md
    │   ├── ui-ux-design.md
    │   └── efficient-communication.md
    └── skills-manifest.json        # Machine-readable catalog
```

---

## Available Skills

### Foundation

**operating-standards.md** — Core operating principles for all tasks

This is the foundation. It establishes how an agent should think about problems, make decisions, and deliver work. Load this first before any specialized skill.

Key principles:
- Understand before acting
- Plan before executing
- Complete work, no placeholders
- Security defaults always on
- Self-verification before delivery

**When to use:** Every task. This should be your default starting point.

---

### Code Generation

**production-grade-development.md** — Four-phase code generation with TDD and security

Takes you from requirements to production-ready code through a structured process: analysis, tests, implementation, and self-audit. Includes threat modeling for security-sensitive code.

Phases:
- Analysis and design (scope, interface, edge cases, threat model)
- Test suite (unit, integration, security tests)
- Implementation (with strict quality standards)
- Self-audit checklist

**When to use:** Building new features, modules, or APIs from scratch.

---

**full-project-scaffold.md** — Dual-mode for building or auditing complete projects

This skill has two modes. Mode A builds new projects with full scaffolding. Mode B audits existing codebases comprehensively. It scales complexity automatically based on the task.

Modes:
- Mode A: Build new code with tests-first approach
- Mode B: Audit existing code with severity grading

**When to use:** Starting new projects or conducting full codebase reviews.

---

**commit-message-generator.md** — Professional commit messages following Conventional Commits

Analyzes code changes and generates properly formatted commit messages. Follows Conventional Commits specification with context-aware detail levels. Determines when body and footers are needed.

Features:
- Conventional Commits format (type, scope, description)
- Context-aware body inclusion
- Breaking change documentation
- Issue reference formatting
- Project convention detection

**When to use:** Writing commit messages for version control.

---

### Code Audit

**pre-commit-audit.md** — Security and quality gate before pushing to GitHub

The final checkpoint before code reaches version control. Focuses heavily on secrets detection, git hygiene, and blocking issues. Outputs complete fixed files, not suggestions.

Focus areas:
- Secrets scanning (instant blocker)
- Git hygiene (.gitignore, tracked files)
- Security vulnerabilities
- Code quality issues

**When to use:** Before every commit to main branches.

---

**production-audit.md** — Comprehensive audit with A/B/C/D grading

Deep inspection of production codebases. Categorizes every file, applies exhaustive checklists, and delivers a final grade. Includes severity breakdown and remediation priorities.

Audit categories:
- Security (zero tolerance)
- Bugs and logic errors
- Performance issues
- Error handling
- Code quality

**When to use:** Reviewing production code or preparing for deployment.

---

**static-analysis-debug.md** — Root-cause bug diagnosis through code analysis

Specialized in finding bugs that only show up in production. Traces issues to their root cause through static analysis alone—no execution required. Covers race conditions, memory leaks, and async failures.

Bug categories:
- Logic and control flow
- State and data handling
- Async and concurrency
- API and I/O
- Memory and resources

**When to use:** Debugging production issues or investigating hard-to-reproduce bugs.

---

**code-review.md** — Structured code review with severity levels

Production-grade code review providing clear, actionable feedback. Every comment includes file location, issue description, and specific fix. Uses severity system (CRITICAL, HIGH, MEDIUM, LOW, QUESTION).

Features:
- Structured comment format
- Comprehensive checklists (security, correctness, performance, quality)
- Multiple review modes (standard, security, performance, quick)
- Special handling for security issues and large PRs

**When to use:** Reviewing pull requests or conducting code reviews.

---

### Specialized

**image-enhancement.md** — Professional camera simulation and image enhancement

Simulates a Sony A1 camera with 85mm f/1.4 lens. Focuses on identity preservation and photographic realism. Includes detailed lighting, color grading, and output specifications.

Technical specs:
- Camera: Sony A1 (full-frame, 50MP)
- Lens: 85mm f/1.4 at f/1.6
- Output: 4K resolution
- Style: Editorial realism

**When to use:** AI image enhancement requiring photographic quality.

---

**ui-ux-design.md** — Designer-grade interface engineering

Transforms generic UI into production-quality interfaces. Covers color systems, typography scales, spacing grids, motion design, and component standards. Enforces accessibility requirements.

Design principles:
- Personality-driven design
- Clear visual hierarchy
- Motion-aware interactions
- Accessibility-first approach

**When to use:** Building user interfaces that need to look professionally designed.

---

**efficient-communication.md** — Token-efficient communication mode

Reduces response verbosity by 60-80% while maintaining complete technical accuracy. Three compression levels (minimal, standard, maximum) for different scenarios. Preserves code quality and never compresses security warnings.

Compression levels:
- Minimal: 60% reduction, professional tone
- Standard: 70% reduction, technical brevity
- Maximum: 80% reduction, ultra-terse

**When to use:** Working within token limits, cost optimization, or rapid information exchange.

---

## How to Use Skills

### For Kiro AI

Reference skills directly in your prompt:

```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Build a REST API for user authentication with JWT tokens
```

### For Other AI Agents

Copy the skill content (including YAML frontmatter) into your prompt:

```
[Paste content from operating-standards.md]
[Paste content from production-grade-development.md]

Task: Build a REST API for user authentication with JWT tokens
```

### Dependency Management

Some skills depend on others. Check the YAML frontmatter for dependencies. Generally, load foundation skills first, then specialized skills.

Example with dependencies:
```
#skills/foundation/operating-standards.md  (dependency)
#skills/code-audit/production-audit.md     (main skill)

Task: Audit this production codebase
```

---

## Common Workflows

**Building a new feature:**
```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: Create a payment processing module with Stripe integration
```

**Debugging production issues:**
```
#skills/foundation/operating-standards.md
#skills/code-audit/static-analysis-debug.md

Task: Find the root cause of memory leaks in the user service
```

**Pre-deployment audit:**
```
#skills/foundation/operating-standards.md
#skills/code-audit/pre-commit-audit.md

Task: Final security check before pushing to production
```

**Designing interfaces:**
```
#skills/specialized/ui-ux-design.md

Task: Design a landing page hero section for a SaaS product
```

---

## Skill Characteristics

Every skill follows these principles:

**Structured metadata** — YAML frontmatter with name, version, tags, category, and dependencies

**Explicit phases** — Clear execution steps with defined boundaries

**Quality standards** — Non-negotiable rules that enforce production-grade output

**Security defaults** — No hardcoded secrets, input validation, parameterized queries

**Complete output** — No snippets, no placeholders, no "TODO" comments

**Self-verification** — Built-in checklists before delivery

**Complexity scaling** — Adjusts depth based on task complexity (simple/medium/complex)

---

## Contributing

We welcome contributions. See CONTRIBUTING.md for detailed guidelines.

Quick steps:
1. Create a new skill using the template
2. Add YAML frontmatter with all required fields
3. Structure content into clear phases
4. Include comprehensive checklists
5. Define output format
6. Add non-negotiable rules
7. Test with sample tasks
8. Update skills-manifest.json
9. Update this README
10. Submit pull request

---

## Skill Metadata Format

Each skill includes YAML frontmatter:

```yaml
---
name: Skill Name
version: 1.0.0
description: What this skill does
author: Agent-SkillHouse
tags:
  - relevant-tag
category: foundation|code-generation|code-audit|specialized
activation: manual
priority: low|medium|high|critical
dependencies:
  - other-skill-name
---
```

---

## Documentation

- **README.md** — This file (overview and catalog)
- **USAGE.md** — Detailed usage guide with examples
- **QUICK-REFERENCE.md** — Fast lookup cheat sheet
- **CONTRIBUTING.md** — Guidelines for adding skills
- **CHANGELOG.md** — Version history

---

## Statistics

- Total skills: 11
- Categories: 4
- Documentation pages: 5
- Total lines: 8000+

---

## License

BSD 2-Clause License. See LICENSE file for details.

Copyright (c) 2026, Mohammad Faiz

---

## Maintenance

When adding new skills:
1. Add YAML frontmatter at the top
2. Place in appropriate category folder
3. Use kebab-case naming (e.g., static-analysis-debug.md)
4. Follow existing structure (phases, checklists, rules)
5. Specify dependencies if required
6. Update skills-manifest.json
7. Update this README
8. Test thoroughly before submitting

---

**Agent-SkillHouse** — Production-grade skills for AI coding agents.

Created by Mohammad Faiz | https://github.com/Mohammad-Faiz-Cloud-Engineer/Agent-SkillHouse
