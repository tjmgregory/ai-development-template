# Agent Guidelines

<!-- SETUP_NOTICE_START - Delete this block after setup is complete -->

> **First time?** If `SETUP.md` exists in this repo, read and follow it first.
> It will guide you through initialising the project and then self-destruct.

<!-- SETUP_NOTICE_END -->

---

## AI Unified Process (AIUP)

This project follows the **AI Unified Process** - an iterative, requirements-driven development
methodology where specifications drive code, not the reverse.

**Before doing any work**:

- Read `docs/aiup/README.md` for which artifacts this project uses
- Run `bd ready --json` to see what to work on next

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

This project uses **beads (bd)** for **all** issue tracking. Documents define what to build;
beads tracks the work.

```bash
bd ready --json                              # What's ready to work on
bd create "Title" -t feature -p 1 --json     # Create issue
bd update <id> --status in_progress --json   # Claim task (before starting)
bd close <id> -r "Done" --json               # Complete (after pushed)
```

**Types**: `bug`, `feature`, `task`, `epic`, `chore`

**Priorities**: `0` (critical) → `4` (backlog)

Run `bd quickstart` for more.

### Sub-agents and Handoffs

When deferring work to sub-agents or handing off to another session:

- **Create tickets first**: Break work into beads issues before spawning sub-agents
- **One ticket per unit of work**: Each sub-agent should work on a tracked issue
- **Update status**: Mark issues `in_progress` when starting, `closed` when done
- **No silent work**: If it's worth doing, it's worth tracking

### Claude Code Plugin

For Claude Code users: `claude plugin install beads` or see the
[beads plugin](https://github.com/steveyegge/beads/tree/main/claude-plugin) docs.

---

## References

- [AIUP](https://aiup.dev/)
- [beads](https://github.com/steveyegge/beads)
- `docs/aiup/README.md` - Project configuration
