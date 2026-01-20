# Requirements Catalogue

## Functional Requirements

<!-- What the system must do. Each requirement should be testable. -->

| ID | Requirement | Priority | Notes |
|----|-------------|----------|-------|
| REQ-001 | | | |
| REQ-002 | | | |

### Requirement Detail Template

For complex requirements, expand here:

#### REQ-XXX: [Title]

**Description**: [Detailed description]

**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2

**Dependencies**: [Other requirement IDs this depends on]

---

## Non-Functional Requirements

<!-- Quality attributes: performance, security, usability, etc. -->

| ID | Category | Requirement | Priority | Notes |
|----|----------|-------------|----------|-------|
| NFR-001 | Performance | | | |
| NFR-002 | Security | | | |
| NFR-003 | Usability | | | |

---

## Identifier Reference

Use these IDs to create traceability:

- **In Use Cases**: "This use case fulfils REQ-001, REQ-003"
- **In Tests**: "This test verifies REQ-001"
- **In Tickets**: `bd create "Implement REQ-001: [title]" -t task`

When a requirement changes, search for its ID to find all dependent artifacts.

---

## After Writing This Document

Once requirements are reviewed and approved:

1. Create beads tickets for implementation:
   ```bash
   bd create "Implement REQ-001: [description]" -t feature -p 2
   bd create "Implement REQ-002: [description]" -t feature -p 2
   ```

2. Link related tickets using beads dependencies:
   ```bash
   bd dep add <ticket-id> --blocks <other-ticket-id>
   ```

3. This document becomes the specification reference
4. **When requirements change**: Update this doc first, then create tickets for:
   - Updating affected use cases
   - Updating affected tests
   - Updating affected code
