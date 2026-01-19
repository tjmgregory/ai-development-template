# Inception Phase

**Purpose**: Establish project foundation, gather requirements, and plan testing approach.

## When You're Here

You're in inception when you're answering: *"What are we building and why?"*

## Artifacts

### Vision

**File**: `vision.md`

**What it is**: The overarching goals, objectives, and direction. A shared understanding of what
the project aims to achieve.

**When to create**: At the very start. This is usually the first artifact.

**Good signs**:

- Stakeholders can read it and nod
- It answers "why does this exist?"
- It defines scope boundaries (what's NOT included)

**Template starting point**:

```markdown
# Vision

## Problem Statement
[What problem are we solving?]

## Solution Overview
[High-level description of the solution]

## Goals
- [Goal 1]
- [Goal 2]

## Non-Goals (Out of Scope)
- [Thing we're explicitly not doing]

## Success Criteria
[How do we know we've succeeded?]
```

---

### Requirements Catalogue

**File**: `requirements-catalogue.md`

**What it is**: A comprehensive list of functional requirements (what the system must do) and
non-functional requirements (performance, security, usability).

**When to create**: After vision is clear. This translates vision into concrete needs.

**Good signs**:

- Each requirement is testable
- Requirements trace back to business value
- Both functional and non-functional needs are captured

**Tips**:

- Write the ones you know first, then ask AI to identify gaps
- Use a consistent format (ID, description, priority, acceptance criteria)
- Don't over-engineer - you can add detail as you go

---

### Test Strategy

**File**: `test-strategy.md`

**What it is**: The big picture of quality: test levels, types of testing, environments, tooling,
and responsibilities.

**When to create**: Once requirements are taking shape. Helps you think about what "done" means.

**Good signs**:

- Defines where tests will live (unit, integration, e2e)
- Identifies high-risk areas needing more coverage
- Practical given your constraints (time, tools, team)

**Tip**: Thinking about testing early forces you to think about the boundaries of your system.

---

### Stakeholders (Optional)

**File**: `stakeholders.md`

**What it is**: Who cares about this project and what do they need?

**When to create**: For multi-stakeholder projects where different people have different needs.

**Skip if**: Solo project or single clear stakeholder.

---

## Phase Completion

You're ready to move to Elaboration when:

- [ ] Vision is documented and agreed
- [ ] Core requirements are captured (doesn't need to be exhaustive)
- [ ] You know how you'll test things
- [ ] Stakeholders (if any) are aligned

## Common Pitfalls

1. **Over-documenting** - You don't need perfect docs to move forward. Iterate.
2. **Skipping vision** - Even a paragraph helps. Don't jump to requirements.
3. **Requirements as solutions** - "Use PostgreSQL" is a solution. "Persist data reliably" is a requirement.
