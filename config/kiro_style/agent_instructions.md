# Kiro-Style Agent Instructions (inject into agents/tasks)

Use the following as **mandatory instructions** for any agent working on a change request that uses the Kiro-style workflow.

---

## 1. Change-request document path

For the current run, use:

- **Requirements:** `change_requests/gptme/requirements.md`
- **Design:** `change_requests/gptme/design.md`
- **Tasks:** `change_requests/gptme/tasks.md`

If sprint-specific folders are used: `change_requests/gptme/sprint_{sprint_number}/requirements.md` (and same for design.md, tasks.md).

Replace `{sprint_number}` with the actual value from your run inputs.

---

## 2. Before you implement

1. **Check if the three docs exist** for this change request (requirements.md, design.md, tasks.md in the path above).
2. **If they do not exist**: Your planning phase MUST create them first using the templates in `config/kiro_style/templates/`. Use the `file_writer` tool to write:
   - `change_requests/gptme/requirements.md` – user stories, EARS acceptance criteria, MVP scope (max 5–7 MUST HAVE), future iterations.
   - `change_requests/gptme/design.md` – technical design, data flow, interfaces, architecture decisions, traceability to requirement IDs.
   - `change_requests/gptme/tasks.md` – ordered task list with dependencies, each task linked to requirement IDs and design sections, and an explicit per-task `Status`; include test and accessibility requirements.
3. **If they exist**: READ them before implementing. Do not implement features, APIs, or UI that are not in requirements.md or design.md.

---

## 3. When you create or update requirements.md

- Use **EARS** for acceptance criteria: "When [trigger], the system shall [behavior]"; "The system shall [behavior]".
- Define **MVP scope** with IDs (MVP-F001, MVP-F002, …). Maximum 5–7 MUST HAVE features.
- Put everything else in **Future Iterations** (SHOULD, COULD, WON'T).
- Include **non-functional requirements** (performance, security, accessibility, compliance) where relevant.

---

## 4. When you create or update design.md

- Describe **data flow** and **components**.
- Define **interfaces** (API endpoints, request/response, types).
- Record **architecture decisions** (ADRs) briefly.
- Add a **traceability** section mapping design sections to requirement IDs.

---

## 5. When you create or update tasks.md

- List **tasks in dependency order**. Each task must include: `Task ID`, `Status`, description, requirement IDs, design section, depends-on, and tests/a11y.
- Use a consistent status vocabulary: `Not Started`, `In Progress`, `Blocked`, `Done`.
- Keep `Status` current whenever task progress changes.
- Identify **critical path**.
- Do not add implementation tasks that are not traceable to requirements and design.

---

## 6. Guardrails (mandatory)

- **Scope:** Do not implement features or APIs that are not in requirements.md or design.md. If something is missing, add it to the appropriate doc first, then implement.
- **Traceability:** When delivering code or artifacts, reference requirement IDs (e.g. MVP-F001, REQ-001) and design sections (e.g. §4.1) in commit messages, PR descriptions, or deliverable summaries.
- **Quality:** All outputs must meet professional human work standards. No placeholders or incomplete work. Iterate until acceptance criteria are met.
- **CI/CD EXCLUSION:** Do NOT implement GitHub Actions, CI/CD pipelines, or automated test runners. The organization has limited GitHub Actions minutes per month and local test runners are not always active. Focus on code quality improvements (lint fixes, type safety, console.log removal, bug fixes) instead.

---

## 7. Summary

- **One set of three docs per change request:** requirements.md, design.md, tasks.md.
- **Create first** if missing; **read first** before implementing.
- **EARS** in requirements; **traceability** in design and tasks.
- **Task tracking:** include explicit per-task status in tasks.md.
- **Guardrails:** no scope outside the docs; trace deliverables to requirement IDs and design sections.