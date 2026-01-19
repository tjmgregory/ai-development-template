# Construction Phase

**Purpose**: Generate and review implementation code and tests.

## When You're Here

You're in construction when you're answering: *"Let's build it."*

## The AIUP Difference

In traditional development, construction is where developers write code based on specs.

In AIUP, construction is where:

1. **AI generates tests** from use cases and acceptance criteria
2. **Humans review tests** to ensure they capture intent
3. **AI generates code** to pass those tests
4. **AI validates** code against tests
5. **Humans review** for quality, security, edge cases

The specs you created in Elaboration are the source of truth. Code is generated from them.

## Artifacts

### Tests

**Location**: Wherever your test framework expects them (e.g., `tests/`, `__tests__/`, `*.test.ts`)

**What they are**: Executable encoding of expected behaviour, derived from requirements and use cases.

**The contract**: Tests are the objective contract between requirements and implementation. AI-generated
code must satisfy these tests.

**Tip**: Write tests BEFORE implementation when possible. This is TDD, and it works even better with AI.

---

### Code

**Location**: Your source directories (`src/`, `lib/`, etc.)

**What it is**: The implementation generated from specifications.

**Key mindset**: In AIUP, code is not the primary design artifact - it's a replaceable, test-validated
realisation of the specs. You can regenerate code while preserving intent.

---

### Implementation Notes (Optional)

**File**: `implementation-notes.md` or similar

**What it is**: Decisions made during construction that aren't obvious from the code.

**When to create**: When you make significant implementation decisions that future developers
(or AI agents) should know about.

**Examples**:

- "We chose library X over Y because..."
- "This algorithm works as follows..."
- "Performance optimisation: we cache X because..."

---

## Workflow

### For Each Feature/Use Case

1. **Ensure acceptance tests exist** (from Elaboration)
2. **Generate unit/integration tests** from use case specifications
3. **Review tests** - do they capture the intent?
4. **Generate code** to pass the tests
5. **Run tests** - do they pass?
6. **Review code** - is it correct, secure, maintainable?
7. **Iterate** - if gaps found, update specs and regenerate

### When Reality Diverges from Specs

This will happen. When it does:

1. **Update the spec first** - don't just fix the code
2. **Regenerate affected artifacts** - tests, code
3. **Document why** - in a commit message or implementation note

Specs are the source of truth. If the spec was wrong, fix the spec.

---

## Phase Completion

You're ready to move to Transition when:

- [ ] Core features are implemented
- [ ] All acceptance tests pass
- [ ] Code has been reviewed
- [ ] No known critical bugs

## Common Pitfalls

1. **Skipping test review** - AI-generated tests might miss edge cases or misunderstand intent.
2. **Treating code as precious** - In AIUP, code is regenerable. Don't be afraid to throw it away.
3. **Not updating specs** - If you fix something in code, update the spec. Otherwise they'll diverge.
4. **Gold-plating** - Build what's specified, not more. Additional features need new requirements.
