# AI Unified Process (AIUP)

AIUP is a **suggested implementation** of the Unified Process (UP), adapted for AI-assisted
development. It's not a rigid framework - adapt it to your needs.

The core idea: **specifications drive code, not the reverse**.

## Flexibility

Decide up front which artifacts you need based on project complexity, team size, and how much
AI assistance you're using.

### Customisation Checklist

| Artifact | Purpose | When to Include |
|----------|---------|-----------------|
| Vision | Align stakeholders on goals | Always recommended |
| Requirements Catalogue | Document what the system must do | Always recommended |
| Test Strategy | Define testing approach | Recommended for anything non-trivial |
| Entity Model | Define data structures | Recommended if you have domain objects |
| System Use Cases | Define actor-goal interactions | Recommended for user-facing systems |
| Software Architecture | Define technical structure | Recommended for multi-component systems |
| Acceptance Tests | Define "done" criteria | Always recommended |

### Minimum Viable AIUP

For simple projects, you might only need:

1. **Vision** (one paragraph)
2. **Requirements** (bullet list)
3. **Acceptance Tests** (how you know it works)

---

## The Four Phases

### Phase 1: Inception

**Purpose**: Establish foundation - what are we building and why?

**Artifacts**:

- **Vision** - Goals, objectives, scope boundaries, success criteria
- **Requirements Catalogue** - Functional and non-functional requirements, each testable and
  traceable to business value
- **Test Strategy** - Test levels, types, environments, tooling, responsibilities

**Tips**:

- Write requirements yourself first, then ask AI to identify gaps
- Thinking about testing early forces you to think about system boundaries
- Requirements describe needs ("persist data reliably"), not solutions ("use PostgreSQL")

---

### Phase 2: Elaboration

**Purpose**: Design the system - how will it work?

**Artifacts**:

- **Entity Model** - Core business concepts, attributes, relationships. Use domain language,
  not technical jargon. Mermaid diagrams work well.
- **System Use Cases** - Actor-goal interactions. Each should pass the "actor test": would
  someone initiate this to achieve a specific goal?
- **Software Architecture** - Components, responsibilities, interactions, key technical decisions
- **Acceptance Tests** - Specific test cases encoding "done" from a business perspective

**Tips**:

- Use cases are about goals, not functions
  - Bad: "Convert Currency" (that's a function)
  - Good: "Import Transactions" (currency conversion happens within)
- The "So What?" test: if you can't articulate user value, it's probably infrastructure
- Acceptance tests are your safety net for AI regeneration

---

### Phase 3: Construction

**Purpose**: Build it.

**Outputs**: Code and tests (in your source directories, not here)

**The AIUP difference**:

1. AI generates tests from use cases
2. Humans review tests
3. AI generates code to pass tests
4. Humans review code

**Tips**:

- Write tests BEFORE implementation when possible
- Code is regenerable - don't be precious about it
- When reality diverges from specs, update specs first

---

### Phase 4: Transition

**Purpose**: Ship it and improve.

**Activities**: UAT, deployment, feedback collection, continuous improvement

**The loop**:

```
Transition → Feedback → New Requirements → Inception → ... (repeat)
```

---

## Project Status

<!-- Update this as you work -->

**Artifacts in use**:

- [ ] Vision
- [ ] Requirements Catalogue
- [ ] Test Strategy
- [ ] Entity Model
- [ ] System Use Cases
- [ ] Software Architecture
- [ ] Acceptance Tests

**Current phase**: Inception (not started)

**Next steps**:

1. [First thing to do]
2. [Second thing to do]

---

## References

- [AIUP Official Site](https://aiup.dev/)
- [Unified Process (Wikipedia)](https://en.wikipedia.org/wiki/Unified_Process)
- [Writing Effective Use Cases (Cockburn)](https://www.amazon.com/Writing-Effective-Cases-Alistair-Cockburn/dp/0201702258)
