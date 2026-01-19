# Agent Guidelines

**Read this document at the start of every session.**

<!-- SETUP_NOTICE_START - Delete this block after setup is complete -->

> **First time?** If `SETUP.md` exists in this repo, read and follow it first.
> It will guide you through initialising the project and then self-destruct.

<!-- SETUP_NOTICE_END -->

---

## AI Unified Process (AIUP)

This project follows the **AI Unified Process** - an iterative, requirements-driven development
methodology where specifications drive code, not the reverse.

**Before doing any work**, read `docs/aiup/README.md` for:

- Which artifacts this project uses
- Current phase and status
- What to work on next

### Core Principles

- **Specifications are the source of truth** - code is generated from them
- **Tests protect regeneration** - safe to regenerate code when specs improve
- **Short iterations** - specs, code, and tests improve together
- **Update upstream first** - when reality diverges, fix the spec before the code

### The Four Phases

| Phase | Purpose |
|-------|---------|
| Inception | Establish foundation (Vision, Requirements, Test Strategy) |
| Elaboration | Design system (Entity Model, Use Cases, Architecture, Acceptance Tests) |
| Construction | Build it (Code, Tests) |
| Transition | Ship it (UAT, Deployment, Improvements) |

---

## Issue Tracking (beads)

This project uses **beads (bd)** for all issue tracking.

```bash
bd ready --json                              # What's ready to work on
bd create "Title" -t feature -p 1 --json     # Create issue
bd update <id> --status in_progress --json   # Claim task (before starting)
bd close <id> -r "Done" --json               # Complete (after pushed)
```

**Types**: `bug`, `feature`, `task`, `epic`, `chore`

**Priorities**: `0` (critical) → `4` (backlog)

Run `bd quickstart` for more.

---

## References

- [AIUP](https://aiup.dev/)
- [beads](https://github.com/steveyegge/beads)
- `docs/aiup/README.md` - Project configuration
