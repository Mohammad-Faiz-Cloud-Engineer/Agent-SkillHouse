# Quick Reference

Fast lookup for Agent-SkillHouse skills. Copy and paste the patterns you need.

---

## Common Patterns

### Pattern 1: Build New Feature
```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md

Task: [Your feature description]
```

### Pattern 2: Audit Before Commit
```
#skills/foundation/operating-standards.md
#skills/code-audit/pre-commit-audit.md

Task: Audit this codebase before pushing to GitHub
```

### Pattern 3: Debug Production Issue
```
#skills/foundation/operating-standards.md
#skills/code-audit/static-analysis-debug.md

Task: Find root cause of [issue description]
```

### Pattern 4: Full Project Scaffold
```
#skills/foundation/operating-standards.md
#skills/code-generation/full-project-scaffold.md

Task: MODE A - Build [project description]
```

### Pattern 5: Production Audit
```
#skills/foundation/operating-standards.md
#skills/code-audit/production-audit.md

Task: Comprehensive audit of production codebase
```

---

## Skills by Category

### Foundation (Load First)
- `operating-standards.md` — Core principles for all tasks

### Code Generation
- `production-grade-development.md` — TDD + security + self-audit
- `full-project-scaffold.md` — Build (Mode A) or Audit (Mode B)

### Code Audit
- `pre-commit-audit.md` — Pre-GitHub security gate
- `production-audit.md` — Comprehensive audit (A/B/C/D grade)
- `static-analysis-debug.md` — Root-cause bug analysis

### Specialized
- `image-enhancement.md` — Camera simulation + enhancement
- `ui-ux-design.md` — Designer-grade UI/UX engineering

---

## Task to Skill Mapping

| Task Type | Skills to Load |
|-----------|----------------|
| Build API endpoint | `operating-standards` + `production-grade-development` |
| Build full project | `operating-standards` + `full-project-scaffold` |
| Fix bugs | `operating-standards` + `static-analysis-debug` |
| Pre-commit check | `operating-standards` + `pre-commit-audit` |
| Production review | `operating-standards` + `production-audit` |
| Audit existing code | `operating-standards` + `full-project-scaffold` (Mode B) |
| Image processing | `image-enhancement` |
| UI/UX design | `ui-ux-design` |

---

## Skill Properties

| Skill | Priority | Dependencies | Modes |
|-------|----------|--------------|-------|
| operating-standards | High | None | — |
| production-grade-development | High | operating-standards | — |
| full-project-scaffold | High | operating-standards | Build, Audit |
| pre-commit-audit | Critical | operating-standards | — |
| production-audit | High | operating-standards | — |
| static-analysis-debug | High | operating-standards | — |
| image-enhancement | Medium | None | — |
| ui-ux-design | High | None | — |

---

## Cheat Sheet

### Load a Skill (Kiro)
```
#skills/category/skill-name.md
```

### Load Multiple Skills
```
#skills/foundation/operating-standards.md
#skills/code-generation/production-grade-development.md
```

### Specify Mode (Dual-Mode Skills)
```
#skills/code-generation/full-project-scaffold.md

Task: MODE A - [build task]
```
or
```
Task: MODE B - [audit task]
```

### Override Rules (Use Sparingly)
```
#skills/code-generation/production-grade-development.md

Override: Skip Phase 2 (tests) for prototype

Task: [Your task]
```

---

## Output Formats

### Code Generation
```
## 1. ANALYSIS
[Scope, interface, edge cases, threat model]

## 2. TEST SUITE
[Complete runnable tests]

## 3. IMPLEMENTATION
[Full source files]

## 4. SELF-AUDIT
[Checklist with PASS/FAIL]

## 5. USAGE EXAMPLE
[How to use the code]
```

### Code Audit
```
FILE: path/to/file.ext
──────────────────────────────────────────
ISSUE #N | Severity | Category
Location: Line X / function name
Problem:  [What's wrong]
Impact:   [What breaks]
Fix:      [What changed]
──────────────────────────────────────────
FIXED FILE: [complete corrected file]
```

### Final Report
```
SUMMARY
- Files audited: XXX
- Issues found: XXX
- Issues fixed: XXX

SEVERITY BREAKDOWN
[Table with categories and severity levels]

FINAL GRADE/STATUS: [A/B/C/D or APPROVED/CONDITIONAL/BLOCKED]
```

---

## Common Mistakes

### Wrong Order
Wrong:
```
#skills/code-generation/production-grade-development.md
#skills/foundation/operating-standards.md  (Load foundation FIRST)
```

Correct:
```
#skills/foundation/operating-standards.md  (Foundation first)
#skills/code-generation/production-grade-development.md
```

### Missing Dependencies
Wrong:
```
#skills/code-audit/production-audit.md
(missing operating-standards dependency)
```

Correct:
```
#skills/foundation/operating-standards.md  (Dependency)
#skills/code-audit/production-audit.md     (Main skill)
```

### Wrong Skill for Task
Wrong:
```
#skills/specialized/image-enhancement.md

Task: Build a REST API  (Wrong skill!)
```

Correct:
```
#skills/code-generation/production-grade-development.md

Task: Build a REST API  (Correct!)
```

---

## Pro Tips

1. Always load foundation first unless using specialized skills
2. Check dependencies in YAML frontmatter
3. Match skill to complexity: simple task = simple skill
4. Use Mode A/B for dual-mode skills
5. Provide context for better results
6. Chain skills for complex workflows
7. Test with examples before production use

---

## Quick Links

- [Full Documentation](README.md)
- [Usage Guide](USAGE.md)
- [Contributing Guide](CONTRIBUTING.md)
- [Skills Manifest](skills/skills-manifest.json)

---

## Need Help?

| Question | Answer |
|----------|--------|
| Which skill do I need? | See Task to Skill Mapping above |
| How do I load skills? | See Cheat Sheet above |
| What's the output format? | See Output Formats above |
| Can I chain skills? | Yes, see Common Patterns above |
| How do I contribute? | See CONTRIBUTING.md |

---

Last Updated: 2026  
Version: 1.0.0  
Created by Mohammad Faiz
