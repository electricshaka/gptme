# Kiro-Style Agent Instructions and Guardrails

This directory defines the **Kiro-style** workflow for major change requests: structured **requirements**, **design**, and **tasks** documents that agents must create and use, with clear instructions and guardrails.

## Purpose

- **Single source of truth** per change request: `requirements.md`, `design.md`, `tasks.md`.
- **Agent instructions**: All agents that work on a change request MUST read and update these docs as appropriate.
- **Guardrails**: Tasks that implement features MUST trace back to requirements and design; outputs are validated against these docs where applicable.

## Path Convention

For each major change request (e.g. one sprint or one feature batch), create or use a folder:

```
change_requests/gptme/          # one folder per project
  requirements.md
  design.md
  tasks.md
```

With optional sprint/request id:

```
change_requests/gptme/sprint_{sprint_number}/
  requirements.md
  design.md
  tasks.md
```

Agents receive `sprint_number` and `feature_request` in inputs; the path is `change_requests/gptme/requirements.md` (and same for design.md, tasks.md), or `change_requests/gptme/sprint_{sprint_number}/` when using sprint subfolders.

## Document Roles

| Document | Owner (suggested) | Content |
|----------|-------------------|--------|
| **requirements.md** | Business analyst / Tech lead | User stories, EARS acceptance criteria, scope (MVP vs future), non-functional requirements |
| **design.md** | Tech lead / Architect | Technical design, data flow, interfaces (API, types), architecture decisions |
| **tasks.md** | Tech lead / PM | Ordered task list with dependencies, linked to requirement IDs and design sections; explicit per-task status; test and accessibility requirements |

## Agent Instructions (inject into backstory or task context)

Agents MUST:

1. **Before implementing**: Read `change_requests/gptme/requirements.md` and `design.md` (and `tasks.md` if doing task execution). If these files do not exist for the current change request, the agent responsible for the phase MUST create them first (see tasks below).
2. **When creating/updating specs**: Use the templates in `config/kiro_style/templates/` and write to the path above. Use EARS format for acceptance criteria in requirements.md.
3. **When implementing**: Trace every code/artifact change to a requirement ID and design section. Do not implement features not listed in requirements.md or design.md.
4. **Guardrail**: Do not add scope (features, APIs, UI) that is not in requirements.md or design.md. If something is missing, propose it in the doc first, then implement.

## Guardrails (validation)

- **Scope guardrail**: Implementation tasks should reference requirement IDs (e.g. MVP-F001) and design section numbers. Use `crew_ai_sdlc.guardrails.kiro_guardrails.kiro_scope_guardrail` on tasks to require that output mentions at least one requirement ID or design section.
- **Doc-first**: The task `create_kiro_change_request_docs` runs before `feature_triage_and_planning` and creates requirements.md, design.md, tasks.md. Downstream tasks are instructed to read these first.
- **Optional**: `kiro_docs_exist_guardrail(output, req_path, design_path, tasks_path)` can validate that a planning output confirms creation of all three files.

## Templates

See `config/kiro_style/templates/` for:

- `requirements.md` – User stories, EARS criteria, MVP scope
- `design.md` – Technical design, data flow, interfaces
- `tasks.md` – Task list with dependencies, per-task status, and links to requirements/design

## Integration

- **SDLC crew**: Tasks `feature_triage_and_planning` and similar can be extended to also produce `requirements.md`, `design.md`, `tasks.md` in `change_requests/gptme/`, or new tasks can be added that run first and create these from `feature_request`.
- **Run inputs**: Ensure `sprint_number` and `feature_request` are passed so agents know which change-request folder to use.