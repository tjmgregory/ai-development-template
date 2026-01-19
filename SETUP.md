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

### 4. Choose artifacts

Walk through `docs/aiup/README.md` with the user to decide which artifacts they'll use.

For each phase, review the artifact table and ask which ones apply to this project. Consider:

- Project complexity (simple script vs multi-service system)
- Team size (solo vs multiple contributors)
- Domain complexity (well-understood vs novel)
- Compliance/enterprise needs (audit trails, sign-offs)

**At minimum**, most projects should use:

- Vision
- Requirements Catalogue
- Acceptance Tests

Update the "Artifacts in Use" checklist in `docs/aiup/README.md` to reflect their choices.

This can evolve later - artifacts can be added as the project grows.

### 5. Create inception directory

Create `docs/aiup/01-inception/` for the inception artifacts.

If Vision was selected (it usually is), create `docs/aiup/01-inception/vision.md`:

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

### 6. Update project status

In `docs/aiup/README.md`, update the "Current Phase" section:

- Set phase to "Inception"
- Set next steps based on chosen artifacts (e.g., "Fill in Vision", "Draft Requirements")

### 7. Clean up

Delete this file:

```bash
rm SETUP.md
```

Remove the setup notice from `AGENTS.md` - delete everything between (and including):

```
<!-- SETUP_NOTICE_START - Delete this block after setup is complete -->
...
<!-- SETUP_NOTICE_END -->
```

### 8. Commit

```bash
git add -A
git commit -m "Initialise project from AIUP template"
```

---

## Done

The repo is now ready for work. The agent can proceed with normal operations as described
in `AGENTS.md`.
