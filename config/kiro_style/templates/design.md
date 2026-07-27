# Technical Design – gptme

**Change request / Sprint:** {feature_request}  
**Project:** gptme

---

## 1. Overview

Short technical overview and architecture approach for this change request.

---

## 2. Data Flow

Describe main data flows (user → system → storage / APIs). Use diagrams or bullet lists.

- Flow 1: ...
- Flow 2: ...

---

## 3. Components / Modules

| Component | Responsibility | Interfaces |
|-----------|-----------------|------------|
| ... | ... | ... |

---

## 4. Interfaces (API / Types)

### 4.1 API endpoints (if applicable)

| Method | Path | Description | Request/Response |
|--------|------|-------------|-------------------|
| GET | /api/... | ... | ... |

### 4.2 Data types / DTOs (if applicable)

```ts
// Example TypeScript or describe in prose
interface ExampleDto {
  id: string;
  name: string;
}
```

---

## 5. Architecture Decisions

- **ADR-1**: [Decision]. Rationale: ...
- **ADR-2**: ...

---

## 6. Traceability to Requirements

| Design section | Requirement IDs |
|----------------|-----------------|
| §2 Data Flow | REQ-001, REQ-002 |
| §4.1 API | REQ-003 |

---

*All implementation must align with this design. No new APIs or components without updating this document.*