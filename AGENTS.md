# Agent Guidelines

This document provides essential guidelines for AI agents working on this project.
**Read this document at the start of every session.**

<!-- SETUP_NOTICE_START - Delete this block after setup is complete -->

> **First time?** If `SETUP.md` exists in this repo, read and follow it first.
> It will guide you through initialising the project and then self-destruct.

<!-- SETUP_NOTICE_END -->

---

## 1. AI Unified Process (AIUP)

This project follows the **AI Unified Process** - an iterative, requirements-driven development
methodology where specifications drive code, not the reverse.

**Before doing any work**, read:

- `docs/aiup/README.md` - Process overview and which artifacts this project uses
- The relevant phase directory for your current work

### Core Philosophy

- **Requirements drive everything** - specifications generate code, not the reverse
- **AI handles tedious work** - humans focus on business logic and validation
- **Tests protect evolution** - comprehensive tests ensure consistent behaviour during regeneration
- **Short iterations** - specifications, code, and tests improve together

### The Four Phases

| Phase | Purpose | Key Artifacts |
|-------|---------|---------------|
| **Inception** | Establish foundation | Vision, Requirements, Test Strategy |
| **Elaboration** | Design system | Entity Model, Use Cases, Architecture, Acceptance Tests |
| **Construction** | Build it | Code, Tests |
| **Transition** | Ship it | UAT, Deployment, Improvements |

### Your Responsibilities

1. **Know the current phase** - check `docs/aiup/README.md` for project status
2. **Read before writing** - understand existing specs before generating code
3. **Update specs when reality diverges** - specs are the source of truth
4. **Link work to requirements** - every change should trace back to a requirement
5. **Iterate** - when gaps are discovered, update upstream artifacts first

---

## 2. Issue Tracking with beads

This project uses **beads (bd)** for all issue tracking. Do NOT use markdown TODOs or other
tracking methods.

### Quick Reference

```bash
# Check what's ready to work on
bd ready --json

# Create new issue
bd create "Issue title" -t feature -p 1 --json

# Claim a task (do this BEFORE starting work)
bd update <id> --status in_progress --json

# Complete work (only after pushed to main)
bd close <id> -r "Completed" --json
```

### Issue Types & Priorities

**Types**: `bug`, `feature`, `task`, `epic`, `chore`

**Priorities**: `0` (critical) → `4` (backlog)

### Dependencies

Link related work:

```bash
bd create "Found bug" -p 1 --deps discovered-from:<parent-id> --json
```

### Important Rules

- Always use `--json` flag for programmatic use
- Claim tasks with `in_progress` before starting work
- Only close issues after work is pushed to main
- Do NOT commit `.beads/` files - beads manages its own sync

### More Info

Run `bd quickstart` or see [beads documentation](https://github.com/steveyegge/beads)

---

## 3. Coding Standards

<!--
CUSTOMISE THIS SECTION based on your project needs.
Add coding standards documents if your project requires them.
-->

General principles:

- Follow existing patterns in the codebase
- Write tests alongside code
- Keep commits atomic and focused
- Document non-obvious decisions

---

## 4. Version Control

- **Do not commit unless instructed** (unless project specifies otherwise)
- Follow the project's commit message conventions
- Keep commits focused on single changes

---

## Workflow Summary

### Starting a Session

1. Read this file (AGENTS.md)
2. Read `docs/aiup/README.md` for current project phase and artifacts
3. Check for ready work: `bd ready --json`
4. Understand context before making changes

### During Work

1. Follow AIUP phase requirements
2. Update specs if you discover gaps
3. Link work to requirements
4. Write tests alongside implementation

### Completing Work

1. Ensure tests pass
2. Update any affected documentation
3. Wait for commit instruction (unless told otherwise)

---

## References

- [AI Unified Process](https://aiup.dev/) - Official AIUP documentation
- [beads](https://github.com/steveyegge/beads) - Issue tracking
- `docs/aiup/README.md` - Project-specific AIUP configuration
