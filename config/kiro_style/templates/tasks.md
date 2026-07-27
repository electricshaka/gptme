# Tasks – gptme

**Change request / Sprint:** {feature_request}  
**Project:** gptme

Tasks are ordered by dependency. Each task links to requirements and design sections.

---

## Task List

| Task ID | Status | Description | Requirement IDs | Design § | Depends on | Tests / QA |
|---------|--------|-------------|-----------------|----------|------------|------------|
| T-001 | Not Started | [Task title] | MVP-F001, REQ-001 | §2, §4.1 | - | Unit, integration |
| T-002 | Not Started | ... | MVP-F001 | §4.2 | T-001 | Unit |
| T-003 | Not Started | ... | MVP-F002 | §3 | T-001 | Integration, a11y |

Allowed `Status` values: `Not Started`, `In Progress`, `Blocked`, `Done`.

---

## Dependencies (critical path)

- T-001 (no deps)
- T-002 → T-001
- T-003 → T-001
- ...

---

## Acceptance per task

- **T-001**: [ ] Acceptance criteria from requirements met; design § implemented.
- **T-002**: [ ] ...
- **T-003**: [ ] ...

---

## Test & accessibility requirements

- Unit tests: ...
- Integration tests: ...
- Accessibility (a11y): ...

---

*Implementation order must follow dependencies. Each deliverable must reference Task ID and Requirement IDs.*