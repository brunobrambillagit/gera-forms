# Gera Forms — Project State

> `STATE.md` is an execution-state index. It does not replace requirements, specs, plans, tasks, ADRs or code.

---

# 1. Metadata

**Last updated:** 2026-09-30  
**Updated by:** User / ChatGPT  
**Repository:** https://github.com/brunobrambillagit/gera-forms.git  
**Branch:** main  
**Commit:** last commit  

---

# 2. Current Lifecycle Phase

**Phase:** `03 — User Stories`

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

**Mode:** `PRODUCT`

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

---

# 4. Active Feature

**Feature:** `None`

**Feature path:** `N/A`

**Feature status:** `N/A`

No Feature Specification is currently active.

---

# 5. Active Task

**Task:** `None`

**Task status:** `N/A`

**Task path:** `N/A`

**Blocker:** `None`

No implementation task is currently active.

---

# 6. Blocking Clarifications

No blocking clarifications.

Product clarifications `CL-001` through `CL-025` have been resolved and incorporated into the approved Product Vision Revision 2 and Product Requirements Revision 2 baseline.

---

# 7. Non-Blocking Open Clarifications

None.

New clarifications discovered during User Stories must be registered explicitly and classified as:

```text
DECISION
EVIDENCE
TECHNICAL
```

with their corresponding status and owner.

New material product behavior must not be introduced silently through User Stories or Acceptance Criteria.

---

# 8. Last Completed

**Last completed item:** `Product Vision Revision 2 and Product Requirements Revision 2 approved`

**Date:** 2026-09-30

**Evidence / artifacts:**

```text
specs/00-product/vision.md
Revision: 2
Status: Approved
Approved: 2026-09-30

specs/00-product/requirements.md
Revision: 2
Status: Approved
Approved: 2026-09-30

Product Clarifications:
CL-001 through CL-025 — RESOLVED

Product Requirements:
81 active PR-* requirements approved

PR-SYNC-002 — RETIRED
Identifier must not be reused.
```

The approved requirements baseline covers the following domains:

```text
AUTH
FORM
VERSION
ASSIGN
SURVEY
OFFLINE
SYNC
LOCATION
FILE
AUDIT
RESULT
PLATFORM
FUTURE
```

---

# 9. Next Valid Action

**Next action:** `Define the User Stories structure by domains and end-to-end workflows, then create the initial US-* and AC-* baseline traced to Product Requirements Revision 2.`

The next work must remain within:

```text
03 — User Stories
```

Do not begin:

```text
04 — MVP Scope
05 — UX / Wireframes
06 — Prototype
07 — Architecture + Constitution
08 — Feature Specification
09 — Plan + Tasks
10 — Implementation
```

until the corresponding lifecycle transition is valid.

---

# 10. Validation State

**Last validation:** `N/A`

**Validated commit:** `N/A`

**Last validation result:** `NOT RUN`

**Commands executed:**

```text
None.
```

**Results:**

```text
No code validation has been executed.
The project has not entered implementation.
```

**Not executed / limitations:**

```text
No automated tests.
No integration tests.
No end-to-end tests.
No build validation.
No deployment validation.

Implementation has not started.
```

---

# 11. Current Risks / Debt Relevant to Active Work

No implementation debt currently exists because implementation has not started.

Current product-definition risks relevant to User Stories:

```text
- User Stories must preserve traceability to the approved
  Product Requirements Revision 2 baseline.

- User Stories must not introduce new product behavior silently.

- Any new material product decision discovered while writing
  User Stories must be registered as a CL-* clarification
  before being assumed.

- User Stories and Acceptance Criteria must not prematurely
  select architecture or implementation technologies.

- Roles and functional permissions must remain conceptually
  distinct unless a later approved decision changes this model.

- Deferred form unassignment must preserve pending work without
  silently granting indefinite authorization to start new surveys.

- "Guardar", "Finalizar" and "Finalizar todos" are distinct
  product actions and must remain semantically separated.

- Finalization requires connectivity.

- A successfully submitted survey becomes non-editable by
  the Surveyor.

- PR-SYNC-002 has been retired and its identifier must never
  be reused.

- Basic result visualization must remain distinct from future
  advanced statistics and visualization capabilities.
```

---

# 12. Resolved Decisions

All currently identified product clarifications are resolved.

## Discovery and Initial Product Baseline

```text
CL-001 — Offline access requires prior online authentication and is valid
         for a maximum of 24 hours from the last valid online login.

CL-002 — Forms must be explicitly downloaded before use, both online
         and offline.

CL-003 — Survey synchronization/submission is initiated manually.

CL-004 — Synchronization states are:
         Pending synchronization,
         Synchronizing,
         Synchronized,
         Synchronization error.

CL-005 — Surveys may be edited before successful submission.
         Successfully submitted surveys are no longer editable
         by the Surveyor.

CL-006 — Published forms are versioned and survey responses remain
         associated with the exact version used.

CL-007 — Location may be captured using device location,
         manual address or map selection.

CL-008 — Successfully submitted local files remain on the device
         until manually deleted by the Surveyor.

CL-009 — Expiration of offline authorization does not delete local
         work. The user must authenticate online again before
         continuing.

CL-010 — A downloaded form version cannot be replaced while draft,
         pending or failed surveys for that version remain.

CL-011 — After a successful version update, only the latest operational
         version of the form is retained locally.

CL-012 — Survey modifications require detailed audit information,
         including question, previous value, new value, user and
         date/time.

CL-013 — Form location configuration may be:
         Required location,
         Optional location,
         No location.
```

## Revision 2 Product Decisions

```text
CL-014 — Administrator User Management

         An Administrator may create and modify users, activate or
         deactivate users, grant or remove permissions and reset
         passwords.

         Users are not functionally deleted. They are deactivated
         when they must no longer operate in Gera Forms.


CL-015 — User Account Data

         User information includes at minimum:
         full name,
         username,
         password,
         role,
         status,
         email,
         phone.


CL-016 — Form Assignment

         When enabling a form, an Administrator may select:
         one Surveyor,
         multiple Surveyors,
         or all Surveyors.

         A functional action equivalent to
         "Seleccionar todos los encuestadores"
         must be available.


CL-017 — Deferred Form Unassignment

         If a form assignment is removed while a Surveyor has pending
         surveys associated with that form, the assignment remains in
         a transitional state.

         The Surveyor must retain the access necessary to resolve
         existing pending surveys.

         Once no pending surveys remain, the unassignment becomes
         effective.

         Deferred unassignment must not cause loss of local work.


CL-018 — Form Draft

         An Administrator may save and modify a form draft as many
         times as necessary.

         Saving a draft does not create a new form version.

         A new version is created only when the Administrator uses
         "Publicar formulario".


CL-019 — Published Form and Next Version

         After a version has been published, the Administrator may
         modify the form to prepare the next version.

         Preparatory changes do not retroactively modify the previously
         published version.

         Publishing again creates the next version.


CL-020 — Required Questions

         Each question may be individually configured as:
         Required,
         Optional.

         Required-question validation applies before a survey may
         be finalized.


CL-021 — Survey Save and Finalization

         "Guardar" saves the current survey as an editable draft.

         A draft may be modified as many times as necessary.

         "Finalizar" validates and sends the survey.

         Finalization requires Internet connectivity.

         After successful submission, the Surveyor may no longer
         modify the survey.


CL-022 — Survey Identification

         Every survey has a visible numeric identifier.

         The identifier is visible to the Administrator and,
         within the applicable access scope, to the Surveyor.

         The survey also retains contextual information such as:
         Surveyor,
         form,
         form version,
         date,
         status,
         responses.

         Technical identifier generation remains a later decision.


CL-023 — Results

         Administrator result consultation includes at minimum:
         survey identifier,
         form,
         version,
         Surveyor,
         date,
         status,
         responses,
         filters,
         search.

         A simple pie chart is included for categorical responses
         whose nature supports this form of aggregation.

         Advanced statistics and visualization remain future
         capabilities.


CL-024 — Finalization Model

         "Guardar" preserves an editable draft.

         "Finalizar" validates and sends one survey.

         "Finalizar todos" replaces the previous global
         synchronization action.

         "Finalizar todos" is used to send multiple surveys.

         Finalization actions require connectivity.

         Successful submission permanently closes Surveyor editing.

         Submission errors preserve local information for retry.


CL-025 — Finalizar Todos Selection Model

         "Finalizar todos" uses manual survey selection.

         The Surveyor selects which surveys are intended for submission.

         Each selected survey is validated individually.

         An invalid selected survey must be corrected before it can
         be submitted.

         An invalid survey does not prevent other valid selected
         surveys from being submitted.

         Non-selected surveys remain unchanged as drafts.
```

These decisions are incorporated into the approved Product Vision Revision 2 and Product Requirements Revision 2 baseline.

---

# 13. Execution Authority

```text
Code/file edits: Allowed when implementation requested
Local tests: Allowed
Spec updates: Allowed
STATE.md updates: Allowed

Git commit: Not authorized unless explicitly requested or an
            established workflow exists
Git push: Not authorized
Merge: Not authorized
Deploy: Not authorized
Production migration: Not authorized
Destructive production action: Not authorized
```

No implementation authority has been exercised yet.

---

# 14. State Integrity Checklist

Before continuing a new session, verify:

```text
[x] Current lifecycle phase matches completed authoritative artifacts
[x] Product Vision Revision 2 is approved
[x] Product Requirements Revision 2 is approved
[x] Product clarifications CL-001 through CL-025 are resolved
[x] Product Requirements contain 81 active PR-* requirements
[x] PR-SYNC-002 remains RETIRED
[x] No active Feature exists
[x] No active Task exists
[x] Next action is compatible with lifecycle phase
[x] Validation state correctly reflects that implementation has not started
[x] Repository and branch are identified

[ ] Commit metadata updated when available
```

If an inconsistency is discovered:

```text
1. reconcile against authoritative artifacts
2. update STATE.md
3. report the inconsistency
4. then continue
```

---

# 15. Approved Product Baseline

## Product Vision

```text
Artifact:
specs/00-product/vision.md

Revision:
2

Status:
Approved

Approved:
2026-09-30

Previous approved baseline:
2026-09-21
```

Product Vision Revision 2 defines the current Gera Forms product direction, including:

```text
- Administrator and Surveyor roles
- functional user permission management
- user activation and deactivation
- no functional user deletion
- online and offline operation
- Progressive Web App
- explicit form download
- offline authentication window
- form drafts
- required and optional questions
- published form versioning
- preparation of subsequent versions without historical mutation
- individual, multiple and all-Surveyor assignment
- deferred form unassignment
- survey drafts
- Guardar
- Finalizar
- Finalizar todos
- manual selection for batch finalization
- submission validation
- survey persistence
- detailed modification auditing
- visible numeric survey identification
- controlled form version updates
- configurable location collection
- offline attachments
- single-organization scope
- administrator access to submitted results
- result search and filtering
- basic pie-chart visualization for compatible categorical responses
```

---

## Product Requirements

```text
Artifact:
specs/00-product/requirements.md

Revision:
2

Status:
Approved

Approved:
2026-09-30

Active requirements:
81

Retired identifiers:
1
```

Requirement domains:

```text
AUTH      — 11
FORM      —  7
VERSION   —  9
ASSIGN    —  7
SURVEY    —  6
OFFLINE   —  4
SYNC      —  6 active
LOCATION  —  5
FILE      —  6
AUDIT     —  4
RESULT    —  6
PLATFORM  —  6
FUTURE    —  4
-----------------
TOTAL     — 81 active
```

Special requirement history:

```text
PR-SYNC-002 — RETIRED

PR-SYNC-002 is not included in the 81 active requirements.

The identifier PR-SYNC-002 must never be reused for another
requirement.
```

---

# 16. Revision History

## Product Baseline Revision 1

```text
Approved:
2026-09-21

Product Vision:
Approved

Product Requirements:
Approved

Active Product Requirements:
70

Resolved Clarifications:
CL-001 through CL-013
```

Revision 1 established the first approved Product Vision and Product Requirements baseline.

---

## Product Baseline Revision 2

```text
Approved:
2026-09-30

Product Vision:
Revision 2 — Approved

Product Requirements:
Revision 2 — Approved

Active Product Requirements:
81

Retired Product Requirement Identifiers:
PR-SYNC-002

Resolved Clarifications:
CL-001 through CL-025
```

Revision 2 supersedes Revision 1 as the current authoritative product baseline while preserving Revision 1 as historical context.

Revision 2 incorporates:

```text
- expanded user administration
- minimum user account data
- user deactivation instead of deletion
- functional permission management
- form drafts
- required and optional questions
- preparation of subsequent form versions
- multiple and all-Surveyor assignment
- deferred form unassignment
- survey drafts
- explicit Guardar behavior
- explicit Finalizar behavior
- Finalizar todos
- manual batch selection
- individual validation during batch finalization
- visible numeric survey identification
- expanded result consultation
- search and filters
- basic compatible categorical-response visualization
- correction of previous requirement-count inconsistencies
```

---

# 17. Current Traceability State

Current traceability:

```text
Product Vision Revision 2
           │
           ▼
Product Requirements Revision 2
81 active PR-* — APPROVED
           │
           ▼
User Stories (US-*) — NEXT
           │
           ▼
Acceptance Criteria (AC-*) — NEXT
```

Future traceability:

```text
Product Vision
      ↓
PR-*
      ↓
US-*
      ↓
AC-*
      ↓
Feature Specification
      ↓
Implementation Plan
      ↓
TASK-*
      ↓
Code
      ↓
Tests
      ↓
Validation
```

User Stories must reference the Product Requirements they satisfy.

Acceptance Criteria must remain authoritative within their corresponding User Stories.

A User Story must not silently introduce product behavior absent from the approved Product Vision, Product Requirements or an explicitly resolved clarification.

---

# 18. Current Repository Documentation State

Expected documentation state after synchronizing the approved Revision 2 artifacts:

```text
gera-forms/
├── GERA_SDD.md
└── specs/
    ├── STATE.md                         ← CURRENT FILE
    ├── README.md
    │
    ├── 00-product/
    │   ├── vision.md                    ✓ REVISION 2 — APPROVED
    │   ├── requirements.md              ✓ REVISION 2 — APPROVED
    │   └── glossary.md                  Pending
    │
    └── 01-user-stories/                 ← NEXT
```

No framework-specific source structure should be inferred from this state.

Architecture has not yet been selected.

---

# 19. Current Phase Objective

The objective of `03 — User Stories` is to translate Product Requirements Revision 2 into user-centered behaviors with explicit Acceptance Criteria while preserving traceability.

The current phase must:

```text
1. identify coherent user workflows and domains;

2. define stable US-<DOMAIN>-NNN identifiers;

3. associate User Stories with relevant PR-* requirements;

4. define explicit AC-* Acceptance Criteria;

5. make Acceptance Criteria authoritative within their
   corresponding User Stories;

6. identify new ambiguities instead of silently resolving them;

7. register material new decisions through CL-*;

8. avoid architecture and implementation decisions;

9. preserve the distinction between product behavior and
   technical implementation;

10. prepare an approved User Stories baseline for MVP Scope.
```

---

# 20. User Stories Domain Baseline

User Stories should initially be organized using the approved Product Requirements domains where appropriate:

```text
AUTH
FORM
VERSION
ASSIGN
SURVEY
OFFLINE
SYNC
LOCATION
FILE
AUDIT
RESULT
```

The following requirement domains are primarily cross-cutting or scope-oriented and do not necessarily require a one-to-one User Story structure:

```text
PLATFORM
FUTURE
```

Story boundaries must be determined by coherent user behavior rather than mechanically creating one User Story for every Product Requirement.

---

# 21. Initial End-to-End User Story Flows

The User Stories phase should cover the following primary Administrator flow:

```text
Authenticate
    ↓
Manage users
    ↓
Create form
    ↓
Save/edit form draft
    ↓
Configure questions
    ↓
Configure required/optional behavior
    ↓
Configure location behavior
    ↓
Publish version
    ↓
Assign to one/multiple/all Surveyors
    ↓
Manage assignment lifecycle
    ↓
Consult submitted surveys
    ↓
Search/filter results
    ↓
Consult basic compatible visualizations
    ↓
Consult audit information
```

The primary Surveyor flow is:

```text
Authenticate online
    ↓
Obtain temporary offline authorization
    ↓
View assigned forms
    ↓
Download form
    ↓
Start survey
    ↓
Work online/offline
    ↓
Guardar
    ↓
Continue/edit draft
    ↓
Validate
    ↓
Finalizar
       or
Finalizar todos
    ↓
Submit
    ↓
Successful submission
       or
Error + retry
    ↓
Successful survey becomes non-editable
```

Supporting flows include:

```text
Form version update

Deferred form unassignment

Offline authorization expiration

Offline attachment preservation

Submission error recovery

Survey modification auditing
```

These flows are organizational guidance for Phase 03 and do not replace the approved Product Requirements.

---

# 22. Terminology Baseline for User Stories

The following terminology should be used consistently during User Stories:

```text
Guardar
    Save the current survey as an editable draft.

Borrador
    Survey that remains editable and has not been successfully
    submitted.

Finalizar
    Validate and initiate definitive submission of one survey.
    Requires connectivity.

Finalizar todos
    Allow the Surveyor to manually select multiple surveys for
    validation and submission.
    Requires connectivity.

Sincronizado
    Survey whose submission has completed successfully and whose
    correct reception has been confirmed by the central system.

Error de sincronización
    Submission attempt failed and local information remains
    available for retry.

Publicar formulario
    Generate a new identifiable published form version.

Desasignación diferida
    Transitional assignment state used when assignment has been
    removed but existing pending work must still be resolved.
```

User Stories may refine presentation wording later during UX, but must preserve these functional meanings unless a new approved product decision changes them.

---

# 23. Deferred Technical Decisions

The following remain deliberately unresolved because they belong to later lifecycle phases:

```text
- authentication mechanism
- offline authentication implementation
- password storage mechanism
- detailed permission implementation
- local storage technology
- local database selection
- central database selection
- file storage technology
- synchronization protocol
- conflict-resolution implementation
- connectivity-detection implementation
- survey identifier generation strategy
- frontend framework
- backend framework
- map provider
- geocoding provider
- GPS implementation details
- VPS infrastructure design
- Docker adoption
- deployment topology
- API design
- database schema
```

User Stories and Acceptance Criteria must not silently select these technical solutions.

If a technical question becomes necessary before completing User Stories, it must be registered as a `TECHNICAL` clarification and deferred to the appropriate lifecycle phase unless it blocks a product decision.

---

# 24. Resume Instructions

When work resumes:

```text
1. Read GERA_SDD.md.

2. Read specs/STATE.md.

3. Verify that specs/00-product/vision.md is:
   Revision 2 — Approved — 2026-09-30.

4. Verify that specs/00-product/requirements.md is:
   Revision 2 — Approved — 2026-09-30.

5. Verify that Product Requirements contains:
   81 active PR-* requirements.

6. Verify that PR-SYNC-002 remains RETIRED.

7. Verify that CL-001 through CL-025 remain RESOLVED.

8. Remain in Phase 03 — User Stories.

9. Define the User Stories structure by domains and
   end-to-end workflows.

10. Create stable US-* identifiers.

11. Create AC-* Acceptance Criteria owned by their
    corresponding User Stories.

12. Trace each User Story to the applicable PR-* requirements.

13. Register any newly discovered material ambiguity as CL-*.

14. Do not select architecture.

15. Do not begin implementation.

16. Update STATE.md whenever project execution state changes.
```

---

# 25. Current State Summary

```text
Project:
Gera Forms

Milestone:
MVP

Lifecycle Phase:
03 — User Stories

Mode:
PRODUCT

Active Feature:
None

Active Task:
None

Blocking Clarifications:
None

Open Non-Blocking Clarifications:
None

Resolved Clarifications:
CL-001 through CL-025

Product Vision:
Revision 2 — APPROVED — 2026-09-30

Product Requirements:
Revision 2 — APPROVED — 2026-09-30

Active Product Requirements:
81

Retired Product Requirement Identifiers:
PR-SYNC-002

User Stories:
Not started

Acceptance Criteria:
Not started

MVP Scope:
Not started

UX / Wireframes:
Not started

Prototype:
Not started

Architecture + Constitution:
Not started

Feature Specifications:
Not started

Implementation:
Not started

Validation:
NOT RUN

Next Valid Action:
Define the User Stories structure by domains and end-to-end
workflows, then create the initial US-* and AC-* baseline traced
to Product Requirements Revision 2.
```

---

**End of STATE.md**