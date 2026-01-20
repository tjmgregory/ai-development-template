# AI Unified Process (AIUP)

AIUP is a **suggested implementation** of the Unified Process (UP), adapted for AI-assisted
development. It's not a rigid framework - adapt it to your needs.

The core idea: **specifications drive code, not the reverse**.

---

## Choosing Your Artifacts

Decide up front which artifacts you need based on project complexity, team size, and domain.
This choice can evolve - you may add artifacts as the project grows - but it's less iterative
than the code itself.

The tables below show artifacts by phase. **AIUP** artifacts are the standard set; others come
from RUP, OpenUP, and modern practices. Pick what fits your project.

**Note**: These lists aren't exhaustive. Depending on your domain, you may need additional
documents not listed here (compliance artifacts, domain-specific specs, regulatory submissions,
etc.). Research what's typical for your industry, or discuss with your AI agent what other
documentation might be valuable for your specific project.

### Phase 1: Inception

| Artifact | Source | Recommended | Purpose |
|----------|--------|-------------|---------|
| Vision | AIUP | Yes | Goals, scope boundaries, success criteria |
| Requirements Catalogue | AIUP | Yes | Functional and non-functional requirements |
| Test Strategy | AIUP | Yes | Test levels, types, environments, responsibilities |
| Stakeholder Map | RUP | Sometimes | Who cares about this project and why |
| Business Case | RUP | Sometimes | Justify investment (enterprise/funded projects) |
| Risk Register | RUP/OpenUP | Sometimes | Track and mitigate significant unknowns |
| Glossary | RUP | Sometimes | Domain terminology (complex domains) |

### Phase 2: Elaboration

| Artifact | Source | Recommended | Purpose |
|----------|--------|-------------|---------|
| Entity Model | AIUP | Yes | Core business concepts, attributes, relationships |
| System Use Cases | AIUP | Yes | Actor-goal interactions |
| Software Architecture | AIUP | Yes | Components, responsibilities, technical decisions |
| Acceptance Tests | AIUP | Yes | "Done" criteria from business perspective |
| Supplementary Spec | RUP | Sometimes | Detailed non-functional requirements |
| ADRs | Modern | Sometimes | Record architectural decisions with rationale |
| API Specification | Modern | Sometimes | OpenAPI/contracts for integrations |
| Deployment Diagram | RUP | Sometimes | Visualise infrastructure topology |

### Phase 3: Construction

| Artifact | Source | Recommended | Purpose |
|----------|--------|-------------|---------|
| Code | AIUP | Yes | The implementation |
| Tests | AIUP | Yes | Unit, integration, E2E tests |
| Iteration Plan | OpenUP | Sometimes | Plan work for time-boxed iterations |

### Phase 4: Transition

| Artifact | Source | Recommended | Purpose |
|----------|--------|-------------|---------|
| UAT Results | AIUP | Sometimes | User acceptance testing outcomes |
| Deployment Runbook | RUP | Sometimes | How to deploy and rollback |
| Improvement Log | Modern | Sometimes | Track learnings and feedback |

### Minimum Viable AIUP

For simple projects, you might only need:

1. **Vision** (one paragraph)
2. **Requirements** (bullet list)
3. **Acceptance Tests** (how you know it works)

Everything else is scaffolding that helps when complexity grows.

### Templates

Templates for key documents are in [`templates/`](templates/):

- [`vision.md`](templates/vision.md) - Goals, scope, success criteria
- [`requirements-catalogue.md`](templates/requirements-catalogue.md) - Functional and non-functional requirements with identifiers

Use identifiers (REQ-001, NFR-001, G-001) for traceability across artifacts.

**Naming convention**: Filenames should match document titles in kebab-case (e.g., "Requirements Catalogue" → `requirements-catalogue.md`).

---

## Documents vs Tickets

**Documents** (specs, requirements, vision) define *what* to build. They are reference
material, not work tracking.

**Tickets** (beads issues) track *work to do*. Beads is the source of truth for what
needs doing.

### The Workflow

1. **Write the document** (e.g., requirements catalogue)
2. **Human reviews and approves** the document
3. **Create tickets from the document**:
   ```bash
   bd create "Implement REQ-001: User login" -t feature -p 2
   bd create "Implement REQ-002: Password reset" -t feature -p 2
   ```
4. **Work is tracked in beads**, not the document

### When Requirements Change

When a requirement changes, there's a natural cascade:

1. **Update the requirement document first** (specs are source of truth)
2. **Search for the requirement ID** to find affected artifacts
3. **Create tickets for updates**:
   ```bash
   bd create "Update UC-003 for REQ-001 change" -t task -p 2
   bd create "Update tests for REQ-001 change" -t task -p 2
   bd create "Update implementation for REQ-001 change" -t task -p 2
   ```
4. **Link the tickets** if they have dependencies:
   ```bash
   bd dep add <impl-ticket> --blocked-by <test-ticket>
   ```

This ensures changes are tracked and nothing is forgotten.

---

## The Four Phases

### Phase 1: Inception

**Purpose**: Establish foundation - what are we building and why?

**Tips**:

- Write requirements yourself first, then ask AI to identify gaps
- Thinking about testing early forces you to think about system boundaries
- Requirements describe needs ("persist data reliably"), not solutions ("use PostgreSQL")

### Phase 2: Elaboration

**Purpose**: Design the system - how will it work?

**Tips**:

- Use cases are about goals, not functions
  - Bad: "Convert Currency" (that's a function)
  - Good: "Import Transactions" (currency conversion happens within)
- The "So What?" test: if you can't articulate user value, it's probably infrastructure
- Acceptance tests are your safety net for AI regeneration

### Phase 3: Construction

**Purpose**: Build it.

**The AIUP difference**:

1. AI generates tests from use cases
2. Humans review tests
3. AI generates code to pass tests
4. Humans review code

**Tips**:

- Write tests BEFORE implementation when possible
- Code is regenerable - don't be precious about it
- When reality diverges from specs, update specs first

### Phase 4: Transition

**Purpose**: Ship it and improve.

**The loop**:

```
Transition → Feedback → New Requirements → Inception → ... (repeat)
```

---

## Project Status

<!-- Update this as you work -->

### Artifacts in Use

Check the artifacts you're using. Add more as the project evolves.

**Inception**:

- [ ] Vision
- [ ] Requirements Catalogue
- [ ] Test Strategy
- [ ] Stakeholder Map
- [ ] Business Case
- [ ] Risk Register
- [ ] Glossary

**Elaboration**:

- [ ] Entity Model
- [ ] System Use Cases
- [ ] Software Architecture
- [ ] Acceptance Tests
- [ ] Supplementary Spec
- [ ] ADRs
- [ ] API Specification
- [ ] Deployment Diagram

**Construction**:

- [ ] Iteration Plan

**Transition**:

- [ ] UAT Results
- [ ] Deployment Runbook
- [ ] Improvement Log

### Current Status

**Do not track phase or progress here.** Use beads:

```bash
bd ready --json    # What's ready to work on
bd list --json     # All issues
bd stats           # Progress overview
```

---

## References

- [AIUP Official Site](https://aiup.dev/)
- [Unified Process (Wikipedia)](https://en.wikipedia.org/wiki/Unified_Process)
- [Writing Effective Use Cases (Cockburn)](https://www.amazon.com/Writing-Effective-Cases-Alistair-Cockburn/dp/0201702258)
