# Agent Guidelines

---

## Unified Process

This project follows the **Unified Process (UP)** - an iterative, requirements-driven development
methodology where specifications drive code, not the reverse.

**Before doing any work**:

- Read `docs/unified-process/README.md` for which artifacts this project uses
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

- [Unified Process](https://en.wikipedia.org/wiki/Unified_process) - Process overview
- [AIUP](https://aiup.dev/) - AI-optimised UP variant (basis for recommended artifacts)
- [beads](https://github.com/steveyegge/beads) - Issue tracking
- `docs/unified-process/README.md` - Project configuration

## Landing the Plane (Session Completion)

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd sync
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds
