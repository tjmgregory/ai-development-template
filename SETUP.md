# First-Time Setup

**This file exists because this repo was just created from the AIUP template.**

Follow these steps to initialise the project, then delete this file.

---

## Steps

### 1. Get project details from the user

Ask the user:

- What is the project name?
- Brief description (one sentence)
- Should beads sync to a separate branch? (Yes if main is protected)

### 2. Update README.md

Replace `[Project Name]` with the actual project name and fill in the description.

### 3. Initialise beads

```bash
bd init
bd doctor --fix
```

If the user said main is protected, also run:

```bash
bd config set sync_branch beads-sync
```

### 4. Create initial AIUP artifacts

Create the inception directory and `docs/aiup/01-inception/vision.md` with a placeholder:

```markdown
# Vision

<!-- Fill this in to establish project direction -->

## Problem Statement

[What problem are we solving?]

## Solution Overview

[High-level description]

## Goals

- [Goal 1]

## Non-Goals

- [What we're explicitly not doing]

## Success Criteria

[How we know we've succeeded]
```

Update the "Project Status" section in `docs/aiup/README.md`:

- Check the "Vision" checkbox
- Set current phase to "Inception"
- Set next steps to something sensible

### 5. Clean up

Delete this file:

```bash
rm SETUP.md
```

Remove the setup notice from `AGENTS.md` - delete everything between (and including) these
comment markers:

```
<!-- SETUP_NOTICE_START - Delete this block after setup is complete -->
...
<!-- SETUP_NOTICE_END -->
```

### 6. Commit

```bash
git add -A
git commit -m "Initialise project from AIUP template"
```

---

## Done

The repo is now ready for work. The agent can proceed with normal operations as described
in `AGENTS.md`.
