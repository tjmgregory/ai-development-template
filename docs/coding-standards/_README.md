# Coding Standards

This directory is for project-specific coding standards.

## When to Add Standards

Add coding standards when you need to ensure consistency across:

- Multiple contributors (human or AI)
- Different parts of the codebase
- Future maintenance

## Suggested Standards to Consider

Depending on your project, you might document:

### Error Handling & Logging

- How errors should be handled and propagated
- Logging levels and what to log
- Error message formats

### Testing Philosophy

- Test naming conventions
- What to unit test vs integration test
- Mocking guidelines

### Complexity & Clarity

- Maximum function length/complexity
- Naming conventions
- Comment guidelines

### Language-Specific

- TypeScript: strict mode settings, type preferences
- Python: formatting (black/ruff), type hints
- Go: error handling patterns, package structure

### Project-Specific

- API design conventions
- Database access patterns
- Security requirements

## Format

Standards should be:

- **Concise** - Easy to read and reference
- **Actionable** - Clear guidance, not vague principles
- **Justified** - Explain why, not just what

## Example Structure

```markdown
# [Standard Name]

## Principle
[The core idea in one sentence]

## Guidelines
- [Specific actionable guideline]
- [Another guideline]

## Examples

### Good
[Code example]

### Bad
[Code example]

## Why
[Brief explanation of the reasoning]
```

---

*Delete this file and add your own standards as needed.*
