# STATE.template.md
## Gera Forms — Project State Template

> Copy this file to `specs/STATE.md` when initializing the project.
>
> `STATE.md` is an execution-state index. It does not replace requirements, specs, plans, tasks, ADRs or code.

---

# 1. Metadata

**Last updated:** YYYY-MM-DD  
**Updated by:** User | ChatGPT | Developer | Other  
**Repository:** ...  
**Branch:** ...  
**Commit:** ...  

Use `N/A` when branch or commit does not yet exist.

---

# 2. Current Lifecycle Phase

**Phase:** `01 — Discovery`

Allowed values:

```text
01 — Discovery
02 — Product Requirements
03 — User Stories
04 — MVP Scope
05 — UX / Wireframes
06 — Prototype
07 — Architecture + Constitution
08 — Feature Specification
09 — Plan + Tasks
10 — Implementation
11 — Validation + Release
```

**Mode:** `DISCOVERY`

Suggested modes:

```text
DISCOVERY
PRODUCT
UX
ARCHITECTURE
SPEC
PLAN
TASK
IMPLEMENT
REVIEW
DEBUG
RELEASE
```

---

# 3. Current Milestone

**Milestone:** `MVP`

Examples:

```text
MVP
Post-MVP 1
Beta
v1.0
Hardening
Internal Pilot
```

---

# 4. Active Feature

**Feature:** `None`

When active, use:

```text
FEATURE-001 — <Feature Name>
```

**Feature path:** `N/A`

Example:

```text
specs/05-features/001-form-builder/
```

**Feature status:** `N/A`

Allowed spec statuses:

```text
Draft
Approved
Implemented
Validated
Superseded
```

---

# 5. Active Task

**Task:** `None`

When active:

```text
TASK-001 — <Task Name>
```

**Task status:** `N/A`

Allowed task statuses:

```text
TODO
READY
IN_PROGRESS
BLOCKED
DONE
CANCELLED
```

**Task path:** `N/A`

**Blocker:** `None`

If blocked, include the concrete blocker and related `CL-*`, dependency, test failure or external dependency.

---

# 6. Blocking Clarifications

No blocking clarifications.

When present:

```text
- CL-001
  Type: DECISION | EVIDENCE | TECHNICAL
  Status: NEEDS CLARIFICATION | PARTIAL
  Owner: User | ChatGPT | Technical Investigation
  Blocks: <phase / feature / task>
  Question: <short question>
```

Every open clarification MUST have a type.

---

# 7. Non-Blocking Open Clarifications

None.

Use the same format as blocking clarifications.

These do not stop unrelated work.

---

# 8. Last Completed

**Last completed item:** `None — project initialization`

**Date:** YYYY-MM-DD

**Evidence / artifact:**

```text
N/A
```

Examples:

```text
PR-001..PR-008 approved
US-FORM-001..US-FORM-005 approved
TASK-004 DONE
FEATURE-002 validated
ADR-003 accepted
```

---

# 9. Next Valid Action

**Next action:** `Begin Discovery`

Be concrete.

Good:

```text
Resolve CL-FORM-003 and then approve MVP scope.
Resume TASK-007 and run API integration tests.
Create user stories for PR-004 through PR-008.
```

Weak:

```text
Continue working.
```

---

# 10. Validation State

**Last validation:** `N/A`

**Validated commit:** `N/A`

**Last validation result:** `NOT RUN`

Allowed:

```text
PASS
PASS WITH DEBT
FAIL
NOT RUN
BLOCKED
```

**Commands executed:**

```text
None.
```

**Results:**

```text
None.
```

**Not executed / limitations:**

```text
None.
```

---

# 11. Current Risks / Debt Relevant to Active Work

None.

Only include items that materially affect current work.

Example:

```text
- DEBT-004 — Missing integration coverage for publishing workflow.
- BUG-002 — Draft autosave fails after session expiry.
```

Do not turn `STATE.md` into the full debt backlog.

---

# 12. Pending Decisions

None.

Only list decisions that are currently relevant.

Example:

```text
- CL-012 / DECISION — Decide whether anonymous submission is allowed in MVP.
```

---

# 13. Execution Authority

Default:

```text
Code/file edits: Allowed when implementation requested
Local tests: Allowed
Spec updates: Allowed
STATE.md updates: Allowed

Git commit: Not authorized unless explicitly requested or established workflow exists
Git push: Not authorized
Merge: Not authorized
Deploy: Not authorized
Production migration: Not authorized
Destructive production action: Not authorized
```

Change only when the user explicitly authorizes a different workflow.

---

# 14. State Integrity Checklist

Before continuing a new session, verify:

```text
[ ] active feature path exists, if applicable
[ ] active task exists, if applicable
[ ] task status matches tasks.md
[ ] feature status matches spec.md
[ ] plan status is coherent
[ ] blocking CL references exist
[ ] next action is compatible with lifecycle phase
[ ] branch/commit values are coherent when available
```

If inconsistent:

```text
1. reconcile against authoritative artifacts
2. update STATE.md
3. report the inconsistency
4. then continue
```

---

# 15. Bootstrap Values for a New Project

Use these defaults:

```text
Phase: 01 — Discovery
Mode: DISCOVERY
Milestone: MVP
Feature: None
Task: None
Blocking Clarifications: None
Last Completed: Project initialization
Next Action: Begin Discovery
Validation: NOT RUN
```

---

# 16. Example — New Project

```text
Phase:
01 — Discovery

Mode:
DISCOVERY

Milestone:
MVP

Active Feature:
None

Active Task:
None

Blocking Clarifications:
None

Last Completed:
Project initialization

Next Valid Action:
Begin Discovery by defining the problem, target users and primary use cases.
```

---

# 17. Example — Implementation Session

```text
Phase:
10 — Implementation

Mode:
IMPLEMENT

Milestone:
MVP

Active Feature:
FEATURE-003 — Form Publishing

Feature path:
specs/05-features/003-form-publishing/

Feature status:
Approved

Active Task:
TASK-007 — Publish a valid draft form

Task status:
IN_PROGRESS

Blocking Clarifications:
None

Last Completed:
TASK-006 — Publish endpoint authorization

Next Valid Action:
Resume TASK-007. Do not select another READY task.

Validation:
NOT RUN
```

---

# 18. Example — Blocked Decision

```text
Phase:
08 — Feature Specification

Mode:
SPEC

Milestone:
MVP

Active Feature:
FEATURE-004 — Anonymous Responses

Active Task:
None

Blocking Clarifications:
- CL-014
  Type: DECISION
  Status: NEEDS CLARIFICATION
  Owner: User
  Blocks: FEATURE-004
  Question: Can anonymous respondents submit more than once?

Next Valid Action:
Resolve CL-014 before approving FEATURE-004.
```

---

**End of STATE.template.md**
