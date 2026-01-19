# Transition Phase

**Purpose**: Validate system with users, deploy to production, and continuously improve.

## When You're Here

You're in transition when you're answering: *"Is it ready for real use?"*

## Activities

### User Acceptance Testing (UAT)

**What it is**: Real users testing the system against their actual needs.

**Why it matters**: Acceptance tests verify the system works as specified. UAT verifies the
specification was correct.

**Good signs**:

- Users can complete their goals
- No surprises ("I thought it would do X")
- Feedback is about polish, not fundamentals

---

### Deployment

**What it is**: Getting the system into production (or whatever "live" means for your context).

**Consider documenting**:

- How to deploy
- Environment configuration
- Rollback procedures
- Monitoring and alerting

---

### Continuous Improvement

**What it is**: Learning from real usage and feeding back into the system.

**The loop**:

1. Users provide feedback
2. Feedback becomes new requirements
3. New requirements go through AIUP phases
4. System improves

---

## Artifacts

### UAT Plan (Optional)

**File**: `uat-plan.md`

**What it is**: Who will test, what scenarios, how feedback is collected.

**When to create**: If you have specific users to test with and want structured feedback.

**Skip if**: You are the only user, or feedback is informal.

---

### Deployment Strategy (Optional)

**File**: `deployment-strategy.md`

**What it is**: How the system gets to production and stays healthy.

**When to create**: If deployment is non-trivial (multiple environments, complex infrastructure).

**Skip if**: Simple deployment (e.g., single script, Vercel auto-deploy).

---

### Improvement Log (Optional)

**File**: `improvement-log.md`

**What it is**: Running log of learnings, feedback, and ideas for improvement.

**When to create**: Good practice for any project you'll maintain over time.

**Format suggestion**:

```markdown
## YYYY-MM-DD

### Feedback
- [What was observed or reported]

### Action
- [What we did about it, or decision to defer]

### Learning
- [What we learned for future development]
```

---

## Phase Completion

Transition doesn't really "complete" - it's ongoing for the life of the system.

**Initial transition is done when**:

- [ ] System is deployed and accessible
- [ ] Initial users have validated core functionality
- [ ] Feedback mechanism is in place
- [ ] Monitoring/alerting is set up (if applicable)

**Ongoing**:

- Collect feedback
- Prioritise improvements
- Run them through AIUP (new requirements → elaboration → construction → transition)

---

## Common Pitfalls

1. **Skipping UAT** - "It passes tests" isn't the same as "users can use it."
2. **No feedback loop** - If you can't learn from usage, you can't improve.
3. **Treating launch as the end** - Transition is continuous, not a one-time event.
4. **Over-engineering deployment** - Start simple. Add complexity when needed.

---

## The Iteration Loop

AIUP is iterative. After transition, you'll likely discover:

- Requirements that were wrong or missing
- Use cases that don't match reality
- Architecture that needs adjustment

That's normal. Feed learnings back into Inception/Elaboration and iterate.

```
Transition → Feedback → New Requirements → Inception → Elaboration → Construction → Transition
```

This is the continuous improvement loop that keeps your system healthy.
