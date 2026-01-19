# AI Unified Process (AIUP)

This directory contains AIUP artifacts for this project.

## What is AIUP?

AIUP is a **suggested implementation** of the Unified Process (UP), adapted for AI-assisted
development. It's not a rigid framework - it's a set of practices you can adapt to your needs.

The core idea: **specifications drive code, not the reverse**. AI generates code from well-defined
requirements, and tests protect behaviour when code is regenerated.

### AIUP vs Traditional UP

| Traditional UP | AIUP |
|----------------|------|
| Humans write all code | AI generates code from specs |
| Documentation often lags | Specs are the source of truth |
| Tests written after code | Tests protect regeneration |
| Long iteration cycles | Short cycles (days, not months) |

## Flexibility

**AIUP is not prescriptive.** Decide up front which artifacts you need based on:

- Project complexity
- Team size
- Regulatory requirements
- How much AI assistance you're using

### Customisation Checklist

Review this when starting your project:

#### Inception Phase

| Artifact | Purpose | When to Include |
|----------|---------|-----------------|
| Vision | Align stakeholders on goals | Always recommended |
| Requirements Catalogue | Document what the system must do | Always recommended |
| Test Strategy | Define testing approach | Recommended for anything non-trivial |
| Stakeholders | Identify who cares about this | Useful for multi-stakeholder projects |

#### Elaboration Phase

| Artifact | Purpose | When to Include |
|----------|---------|-----------------|
| Entity Model | Define data structures | Recommended if you have domain objects |
| System Use Cases | Define actor-goal interactions | Recommended for user-facing systems |
| Software Architecture | Define technical structure | Recommended for multi-component systems |
| Acceptance Tests | Define "done" criteria | Always recommended |

#### Construction Phase

| Artifact | Purpose | When to Include |
|----------|---------|-----------------|
| Code | The implementation | Obviously |
| Tests | Verify behaviour | Always |
| Implementation Notes | Capture decisions | Optional, for complex implementations |

#### Transition Phase

| Artifact | Purpose | When to Include |
|----------|---------|-----------------|
| UAT Plan | User acceptance testing | If you have users to test with |
| Deployment Strategy | How to ship | If deployment is non-trivial |
| Improvement Log | Track learnings | Good practice for any project |

### Minimum Viable AIUP

For a simple project, you might only need:

1. **Vision** (one paragraph of what you're building)
2. **Requirements** (bullet list of must-haves)
3. **Acceptance Tests** (how you know it works)

Everything else is optional scaffolding that helps when complexity grows.

---

## Project Configuration

<!-- FILL THIS IN when you start your project -->

### Artifacts in Use

- [ ] Vision
- [ ] Requirements Catalogue
- [ ] Test Strategy
- [ ] Entity Model
- [ ] System Use Cases
- [ ] Software Architecture Document
- [ ] Acceptance Tests
- [ ] UAT Plan
- [ ] Deployment Strategy
- [ ] Improvement Log

### Current Phase

**Phase**: Inception (not started)

**Status**: [Describe current status]

**Next Steps**:

1. [First thing to do]
2. [Second thing to do]

---

## Directory Structure

```
docs/aiup/
├── README.md                 # This file
├── 01-inception/             # Foundation phase
├── 02-elaboration/           # Design phase
├── 03-construction/          # Build phase
└── 04-transition/            # Ship phase
```

Each phase directory has a `_README.md` explaining what artifacts belong there and when to
create them.

---

## Additional Guidelines

You may also want to add:

- `docs/coding-standards/` - Language-specific coding standards
- `docs/architecture/` - Architecture Decision Records (ADRs)
- `docs/runbooks/` - Operational procedures
- `history/` - Planning documents and session logs

These are separate from AIUP but complement it well.

---

## References

- [AIUP Official Site](https://aiup.dev/)
- [Unified Process (Wikipedia)](https://en.wikipedia.org/wiki/Unified_Process)
- [Writing Effective Use Cases (Cockburn)](https://www.amazon.com/Writing-Effective-Cases-Alistair-Cockburn/dp/0201702258)
