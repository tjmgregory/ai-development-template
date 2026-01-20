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

### 5. Create Inception epic in beads

Create an epic for the Inception phase with tasks for **writing** each chosen artifact:

```bash
bd create "Inception" -t epic -p 1 --json
```

Then create tasks for each Inception artifact they chose, e.g.:

```bash
bd create "Write Vision" -t task -p 1 --json
bd create "Draft Requirements Catalogue" -t task -p 1 --json
bd create "Define Test Strategy" -t task -p 1 --json
```

Link them to the epic as appropriate.

**Important**: These tickets are for *writing the documents*, not implementing features.
Do not auto-generate the document content - the human writes it.

Use templates from `docs/aiup/templates/` as starting points.

Once a document is written and approved, *new* tickets are created for the implementation
work (see "Documents vs Tickets" in `docs/aiup/README.md`).

### 6. Update project status

In `docs/aiup/README.md`, set "Current Phase" to "Inception".

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
