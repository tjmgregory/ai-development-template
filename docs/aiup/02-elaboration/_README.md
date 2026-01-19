# Elaboration Phase

**Purpose**: Design system architecture, create detailed specifications, and derive acceptance
criteria.

## When You're Here

You're in elaboration when you're answering: *"How will this system work?"*

## Artifacts

### Entity Model

**File**: `entity-model.md`

**What it is**: Core business concepts (entities), their attributes, and relationships. The
canonical data view for the application.

**When to create**: When you have domain objects that need to be understood consistently across
the system.

**Good signs**:

- Uses domain language (not technical jargon)
- Relationships are clear
- Attributes have meaning, not just types

**Tip**: Mermaid diagrams work well for visualisation. Keep it at the conceptual level - this
isn't a database schema.

**Skip if**: Very simple system with no real domain model (e.g., a CLI tool).

---

### System Use Cases

**File**: `system-use-cases.md`

**What it is**: What the system must do from an actor's perspective. Actor-goal interactions.

**When to create**: When you have users or external systems interacting with your system.

**Good signs**:

- Each use case passes the "actor test" - would someone initiate this to achieve a goal?
- Focuses on WHAT, not HOW
- Stable even if implementation changes

**Key learning**: Use cases are about goals, not functions.

- Bad: "Convert Currency to GBP" (that's a function)
- Good: "Import and Normalise Transactions" (that's a goal, currency conversion happens within)

**Skip if**: No external actors (e.g., a library or internal tool).

---

### Software Architecture Document

**File**: `software-architecture-document.md`

**What it is**: Main components, responsibilities, interactions (APIs, messaging, data flows),
and cross-cutting decisions (layering, tech stack, deployment).

**When to create**: When you have multiple components or non-trivial technical decisions.

**Good signs**:

- Components have clear responsibilities
- Interactions are defined (who calls whom, how)
- Key decisions are documented with rationale

**Tip**: Can include diagrams (C4, sequence diagrams, etc.) but don't over-engineer. Start simple.

**Skip if**: Single-file script or very simple system.

---

### Acceptance Tests

**File**: `acceptance-tests.md`

**What it is**: Specific test cases that encode "this is what it means for the system to be
acceptable" from a business/user perspective.

**When to create**: As use cases stabilise. These are derived from requirements and use cases.

**Good signs**:

- Each test case is traceable to a requirement
- Tests are concrete (specific inputs, expected outputs)
- Covers happy paths AND edge cases

**Why this matters in AIUP**: Acceptance tests are your safety net. When AI regenerates code,
these tests ensure behaviour is preserved.

---

## Phase Completion

You're ready to move to Construction when:

- [ ] Core entities are modelled (if applicable)
- [ ] Main use cases are documented (if applicable)
- [ ] Architecture decisions are made (if applicable)
- [ ] Acceptance tests define "done" for key features

## Common Pitfalls

1. **Use cases as technical specs** - If it fails the "actor test," it's probably technical design,
   not a use case.
2. **Analysis paralysis** - You don't need to document everything. Focus on what's complex or risky.
3. **Forgetting acceptance tests** - These protect you during construction. Don't skip them.
4. **Too much detail too early** - Elaborate iteratively. Start with the core, add detail as needed.

## The "So What?" Test

For each artifact, ask: "Why does the user/stakeholder care?"

If you can't articulate user value, it might be infrastructure detail that belongs in technical
documentation, not elaboration artifacts.
