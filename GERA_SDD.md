# GERA_SDD.md
## Gera Forms — Spec-Driven Development Standard

**Version:** 1.2  
**Status:** Canonical Candidate  
**Project:** Gera Forms  
**Purpose:** Define the operating rules for designing, specifying, implementing, validating, and evolving Gera Forms with ChatGPT or another AI-assisted development agent.

---

# 0. Purpose

This document defines **how Gera Forms is developed**.

It does not define product functionality. Product behavior belongs in the project specifications.

The standard exists to make AI-assisted development:

- incremental;
- traceable;
- reviewable;
- testable;
- resistant to undocumented assumptions;
- resumable across sessions;
- synchronized with the real codebase;
- safe around destructive or production actions;
- fast enough to be useful.

The development model is based on **Spec-Driven Development (SDD)**.

Core principle:

> **Understand and specify behavior before implementing it.**

Core implementation chain:

```text
Requirement
   ↓
User Story
   ↓
Feature Spec
   ↓
Implementation Plan
   ↓
Tasks
   ↓
Code
   ↓
Tests
   ↓
Validation
```

---

# 1. Operating Model

Development is collaborative between:

- **User / Product Owner** — makes product decisions, defines priorities, approves material changes and phase transitions.
- **ChatGPT / AI Engineering Partner** — elicits requirements, structures artifacts, identifies ambiguity, investigates evidence, proposes alternatives, plans implementation, implements approved tasks, writes tests and validates traceability.
- **Repository** — persistent source of project state.

A conversation is temporary.

The repository is durable.

Therefore:

> Important decisions MUST NOT exist only in chat history.

Any decision affecting:

- product behavior;
- UX;
- architecture;
- security;
- persistence;
- APIs;
- deployment;
- testing;
- scope;

must be reflected in the appropriate artifact.

---

# 2. Core Rules

## 2.1 Specification before implementation

Observable behavior MUST be sufficiently specified before implementation begins.

A feature MUST NOT enter implementation while a blocking product decision remains unresolved.

---

## 2.2 Separate WHAT from HOW

### `spec.md`

Defines **WHAT the system must do**.

Typical contents:

- context and purpose;
- functional requirements;
- non-functional requirements;
- business rules;
- success criteria;
- edge cases;
- assumptions;
- out-of-scope items;
- clarifications.

A `spec.md` SHOULD avoid implementation technology unless the technology itself is part of the requirement.

### `plan.md`

Defines **HOW the approved spec will be implemented**.

Typical contents:

- architecture mapping;
- components;
- APIs/contracts;
- persistence;
- migrations;
- security;
- dependencies;
- source files;
- async/background work;
- observability;
- test strategy;
- rollout;
- technical risks.

`plan.md` MUST NOT invent product requirements.

If planning discovers a missing product decision, create a clarification and return to the spec.

---

## 2.3 Never silently invent important decisions

ChatGPT MUST NOT silently choose product policy.

When information is missing and materially affects behavior, security, data ownership, scope, destructive actions, billing, privacy or compatibility, use the clarification protocol.

---

## 2.4 One authoritative owner per information type

Avoid duplicating the same authoritative rule across files.

Ownership model:

```text
requirements.md
→ owner of PR-*

user stories
→ owner of US-* and AC-*

feature spec.md
→ owner of FR-*, NFR-*, BR-*, SC-*

plan.md
→ owner of implementation design

tasks.md
→ owner of TASK-*

ADR
→ owner of material architecture decisions

STATE.md
→ owner of current execution state
```

Other documents SHOULD reference IDs instead of copying authoritative text.

---

## 2.5 Traceability

Every implemented behavior SHOULD be traceable through:

```text
PR
 ↓
US
 ↓
FR / NFR / BR
 ↓
AC / SC
 ↓
TASK
 ↓
Code
 ↓
Test
 ↓
Validation
```

Stable IDs MUST be preserved once published.

Do not renumber IDs merely for visual order.

---

## 2.6 Small implementation increments

Prefer:

```text
spec → plan → task → code → test → validate
```

over:

```text
large spec → uncontrolled full-module implementation
```

Large tasks MUST be decomposed before implementation.

---

## 2.7 Documentation changes with behavior

Any code change that modifies observable behavior MUST update the relevant specification artifacts in the same development cycle.

A feature is not complete when code and specs disagree.

---

## 2.8 Drift must be visible

If implementation and approved behavior disagree, report the discrepancy.

Do NOT silently rewrite the specification to match the code.

Use the drift protocol.

---

## 2.9 Tech debt is explicit

Known shortcuts, architectural violations, missing non-blocking tests, scalability concerns and temporary workarounds MUST be recorded as:

```text
DEBT-*
```

Tech debt must not be disguised as completed work.

---

## 2.10 Work item taxonomy

Use:

```text
PR-*          Product Requirement
US-*          User Story
AC-*          Acceptance Criterion
FR-*          Functional Requirement
NFR-*         Non-Functional Requirement
BR-*          Business Rule
SC-*          Success Criterion
CL-*          Clarification
ADR-*         Architecture Decision Record
TASK-*        Implementation Task
BUG-*         Observed incorrect behavior
FIX-*         Corrective initiative
DEBT-*        Technical debt
SPIKE-*       Technical experiment
SCREEN-*      Screen definition
UX-DEC-*      UX decision
OOS-*         Out-of-scope item
ASSUMPTION-*  Explicit assumption
```

---

# 3. Authority Model

A single hierarchy is insufficient because product intent, engineering design and observed reality answer different questions.

## 3.1 Product Behavior Authority

For:

> What SHOULD the product do?

Use:

```text
approved feature spec
      ↓
approved product requirement / user story
      ↓
approved UX decision
```

If these disagree, create a clarification.

Current code does NOT automatically override approved behavior.

---

## 3.2 Engineering Authority

For:

> How SHOULD the system be implemented?

Use:

```text
constitution.md
      ↓
accepted ADR
      ↓
approved plan.md
      ↓
established repository conventions
```

A plan cannot contradict the constitution without an explicit documented deviation.

---

## 3.3 Observed Reality

For:

> What DOES the system currently do?

Use evidence from:

```text
runtime behavior
+
source code
+
tests
+
migrations/configuration
```

Observed reality describes implementation, not necessarily intended behavior.

---

## 3.4 Conflict classification

Use:

```text
DRIFT-CODE
Implementation violates approved behavior.

DRIFT-SPEC
Specification is outdated relative to an approved newer decision.

DRIFT-TEST
Tests encode stale behavior.

DRIFT-DOC
Supporting documentation is stale.

DRIFT-UNKNOWN
Correct authority cannot be determined.
```

`DRIFT-UNKNOWN` requires a project decision.

---

# 4. Persistent Project State

The project MUST maintain:

```text
specs/STATE.md
```

`STATE.md` is the preferred execution-state entry point for every new ChatGPT session.

It MUST contain at minimum:

- last updated date;
- branch if known;
- commit if known;
- current lifecycle phase;
- current milestone;
- active feature;
- active task;
- blocking clarifications;
- last completed work;
- next valid action.

`STATE.md` is not a requirements document.

It is an operational pointer.

---

# 5. STATE Integrity Rule

ChatGPT MUST NOT blindly trust `STATE.md`.

At session start, verify when relevant:

```text
[ ] active feature exists
[ ] active task exists
[ ] active task status matches tasks.md
[ ] spec status is coherent
[ ] plan status is coherent
[ ] referenced blocking CL items exist
[ ] branch/commit context is coherent when available
```

If `STATE.md` conflicts with authoritative artifacts:

1. do not continue blindly;
2. reconcile against authoritative artifacts;
3. update `STATE.md`;
4. report the inconsistency briefly.

`STATE.md` is an execution index, not an authority for product behavior.

---

# 6. Bootstrap Protocol

If `specs/STATE.md` does not exist:

```text
BOOTSTRAP MODE
```

ChatGPT MUST:

1. determine whether the repository is new or existing;
2. if new:
   - create a minimal `specs/STATE.md`;
   - set lifecycle phase to `01 — Discovery`;
   - set active feature to `None`;
   - set active task to `None`;
   - set next valid action to `Begin Discovery`;
3. create `specs/README.md` if missing and appropriate;
4. treat `constitution.md` as optional before Architecture phase;
5. continue through the normal lifecycle.

If the repository contains existing code but no SDD artifacts, use Reverse SDD initialization instead of assuming a new project.

---

# 7. Recommended Repository Structure

```text
gera-forms/
│
├── GERA_SDD.md
│
├── specs/
│   ├── STATE.md
│   ├── README.md
│   ├── constitution.md
│   │
│   ├── 00-product/
│   │   ├── vision.md
│   │   ├── requirements.md
│   │   └── glossary.md
│   │
│   ├── 01-user-stories/
│   ├── 02-ux/
│   │   ├── user-flows.md
│   │   ├── screens.md
│   │   ├── decisions.md
│   │   └── wireframes/
│   │
│   ├── 03-architecture/
│   │   ├── architecture.md
│   │   ├── frontend.md
│   │   ├── backend.md
│   │   ├── database.md
│   │   ├── security.md
│   │   ├── deployment.md
│   │   └── decisions/
│   │       └── ADR-*.md
│   │
│   ├── 04-roadmap/
│   │   ├── mvp.md
│   │   ├── post-mvp.md
│   │   └── backlog.md
│   │
│   ├── 05-features/
│   │   └── NNN-feature/
│   │       ├── spec.md
│   │       ├── plan.md
│   │       ├── tasks.md
│   │       └── validation.md
│   │
│   ├── templates/
│   ├── playbooks/
│   ├── FIX_BACKLOG.md
│   ├── TECH_DEBT.md
│   └── CHANGELOG_SDD.md
│
├── src/
├── tests/
└── ...
```

Do not create framework-specific structure before architecture defines it.

---

# 8. Lifecycle

The lifecycle has eleven phases.

```text
01 Discovery
      ↓
02 Product Requirements
      ↓
03 User Stories
      ↓
04 MVP Scope
      ↓
05 UX / Wireframes
      ↓
06 Prototype
      ↓
07 Architecture + Constitution
      ↓
08 Feature Specification
      ↓
09 Plan + Tasks
      ↓
10 Implementation
      ↓
11 Validation + Release
```

The roadmap is a living artifact, not a one-time phase.

Not every future feature repeats the full lifecycle.

A common post-MVP feature path is:

```text
Feature Discovery
      ↓
Story / Requirement
      ↓
UX change if needed
      ↓
Feature Spec
      ↓
Plan
      ↓
Tasks
      ↓
Implementation
      ↓
Validation
```

---

# 9. Phase-Aware Context Loading

After reading `STATE.md`, ChatGPT SHOULD load only the context needed for the active phase.

```text
PHASE 01 — Discovery
→ vision / requirements / glossary if they exist

PHASE 02 — Product Requirements
→ vision + requirements + glossary

PHASE 03 — User Stories
→ requirements + relevant user-story files

PHASE 04 — MVP Scope
→ requirements + stories + mvp.md

PHASE 05 — UX
→ mvp + relevant stories + UX artifacts

PHASE 06 — Prototype
→ UX artifacts + prototype decisions

PHASE 07 — Architecture
→ product baseline + MVP + architecture + constitution + ADRs

PHASE 08 — Feature Spec
→ related PR/US/AC + active feature spec

PHASE 09 — Plan + Tasks
→ active feature spec + architecture + constitution + plan/tasks

PHASE 10 — Implementation
→ active feature spec + plan + tasks + relevant code/tests

PHASE 11 — Validation
→ spec + plan + tasks + code/tests + validation
```

Do not load the entire repository merely because it exists.

---

# 10. Phase 01 — Discovery

## Objective

Understand the problem before designing the solution.

ChatGPT acts primarily as analyst.

## Topics

When relevant:

- problem;
- target users;
- roles;
- workflows;
- pain points;
- expected value;
- use cases;
- constraints;
- permissions;
- integrations;
- scale;
- data sensitivity;
- compliance;
- deployment constraints;
- business rules;
- exclusions.

## Behavior

ChatGPT SHOULD:

- ask grouped high-value questions;
- explain why non-obvious questions matter;
- summarize confirmed decisions;
- detect contradictions;
- distinguish facts from assumptions;
- inspect existing artifacts before repeating questions.

ChatGPT MUST NOT:

- select architecture prematurely;
- code production features;
- infer important policies from similar products.

## Outputs

```text
specs/00-product/vision.md
specs/00-product/requirements.md
specs/00-product/glossary.md
```

## Exit criteria

```text
[ ] problem defined
[ ] primary users known
[ ] major use cases known
[ ] critical constraints documented
[ ] scope boundaries documented
[ ] no blocking decision prevents product definition
```

---

# 11. Phase 02 — Product Requirements

Use:

```text
PR-*
```

Each requirement SHOULD contain:

- ID;
- title;
- priority;
- status;
- requirement;
- rationale;
- dependencies;
- notes if needed.

Use normative language where useful:

```text
MUST
MUST NOT
SHOULD
MAY
```

Priorities:

```text
P0 — mandatory / blocker
P1 — high value, normally MVP
P2 — useful but deferrable
P3 — future / low urgency
```

Exit criteria:

```text
[ ] stable IDs
[ ] priorities assigned
[ ] exclusions documented
[ ] contradictions resolved
[ ] blocking CL resolved
[ ] baseline approved
```

---

# 12. Phase 03 — User Stories

Use:

```text
US-<DOMAIN>-NNN
AC-<DOMAIN>-NNN
```

User stories own authoritative acceptance-criterion text.

Feature specs SHOULD reference AC IDs instead of duplicating them.

Each story SHOULD identify:

- actor;
- desired capability;
- value/outcome;
- priority;
- related PR;
- acceptance criteria;
- edge cases;
- open clarifications.

---

# 13. Phase 04 — MVP Scope

Define the smallest coherent version that validates primary product value.

MVP does NOT mean:

- insecure;
- untested;
- structurally disposable;
- missing the main workflow.

`mvp.md` SHOULD define:

- objective;
- included capabilities;
- explicit exclusions;
- success criteria;
- dependencies;
- blocking clarifications.

Material MVP scope changes MUST be documented.

---

# 14. Phase 05 — UX / Wireframes

Artifacts may include:

```text
specs/02-ux/user-flows.md
specs/02-ux/screens.md
specs/02-ux/decisions.md
specs/02-ux/wireframes/
```

Important flows SHOULD include:

- actor;
- entry point;
- happy path;
- alternate paths;
- errors;
- permissions;
- completion state.

Material UX choices use:

```text
UX-DEC-*
```

Screens use:

```text
SCREEN-*
```

Exit criteria:

```text
[ ] core MVP flows exist
[ ] required screens identified
[ ] important states/errors represented
[ ] major UX decisions documented
[ ] direction approved
```

---

# 15. Phase 06 — Prototype

A prototype MAY use:

- mock data;
- static HTML;
- local state;
- stubbed APIs;
- simulated authentication;
- non-persistent forms.

Prototype code is not automatically production code.

Prototype decisions that become approved behavior MUST be transferred to authoritative artifacts.

---

# 16. Phase 07 — Architecture + Constitution

Architecture follows approved requirements and MVP scope.

Relevant concerns may include:

- frontend;
- backend;
- persistence;
- authentication;
- authorization;
- APIs;
- state management;
- storage;
- background processing;
- caching;
- security;
- observability;
- environments;
- CI/CD;
- deployment;
- backup/recovery;
- integrations.

Only create architecture artifacts that contain meaningful decisions.

---

# 17. `constitution.md`

`GERA_SDD.md` defines **how development proceeds**.

`constitution.md` defines **engineering invariants**.

Typical topics:

- simplicity;
- modularity;
- dependency direction;
- security;
- secrets;
- auth;
- validation;
- error handling;
- logging;
- migrations;
- APIs;
- testing;
- dependency policy;
- deployment safety.

Every implementation plan MUST state:

```text
Deviations from Constitution: None
```

or document explicit justified deviations.

Before Phase 07, absence of `constitution.md` is NOT an error.

---

# 18. ADRs

Material architecture decisions use:

```text
ADR-*
```

Each ADR SHOULD include:

- status;
- date;
- context;
- decision;
- alternatives;
- consequences;
- related requirements.

Material architecture decisions require user approval.

---

# 19. Phase 08 — Feature Specification

Each implementable feature receives:

```text
specs/05-features/NNN-feature-name/
```

Minimum:

```text
spec.md
plan.md
tasks.md
```

After implementation:

```text
validation.md
```

`spec.md` owns:

```text
FR-*
NFR-*
BR-*
SC-*
```

It references:

```text
PR-*
US-*
AC-*
```

It MUST record:

```text
Type: Forward | Reverse-engineered
Status: Draft | Approved | Implemented | Validated | Superseded
Last reviewed
Last validated against code
Validated commit
```

Detailed template SHOULD live in:

```text
specs/templates/spec.template.md
```

---

# 20. Clarification Protocol

Clarifications use:

```text
CL-*
```

States:

```text
NEEDS CLARIFICATION
PARTIAL
RESOLVED
DEFERRED
```

Every OPEN clarification MUST have exactly one type:

```text
DECISION
EVIDENCE
TECHNICAL
```

---

## 20.1 DECISION

Requires a user/project decision.

ChatGPT MUST NOT resolve it by assumption.

Example:

```text
Can anonymous users submit this form?
```

---

## 20.2 EVIDENCE

Answer may already exist in:

- code;
- tests;
- migrations;
- config;
- specs.

ChatGPT MUST investigate available evidence before asking the user.

If evidence resolves it, mark it `RESOLVED`.

---

## 20.3 TECHNICAL

A technical unknown that may be resolved through:

- repository inspection;
- experiment;
- benchmark;
- ADR.

ChatGPT SHOULD investigate first.

User approval is required only if resolution becomes a material architecture/cost/product decision.

---

## 20.4 Blocking rule

A clarification blocks only the work it materially affects.

Unrelated work MAY continue.

---

# 21. Assumptions and Out of Scope

Use:

```text
ASSUMPTION-*
OOS-*
```

Assumptions are allowed only when low risk and explicit.

Do NOT use assumptions for:

- authorization;
- retention;
- destructive actions;
- privacy;
- billing;
- legal obligations;
- externally visible business rules.

Those require explicit decisions.

---

# 22. Phase 09 — Plan + Tasks

Once a feature spec is approved:

```text
spec.md
   ↓
plan.md
   ↓
tasks.md
```

Implementation begins only when the feature satisfies Definition of Ready.

`plan.md` owns technical design.

`tasks.md` owns implementation units.

Detailed templates SHOULD live in:

```text
specs/templates/plan.template.md
specs/templates/tasks.template.md
```

---

# 23. Planning Rules

Before approving a plan, ChatGPT MUST:

1. read approved feature spec;
2. read relevant architecture;
3. read constitution if it exists;
4. inspect existing code when implementation already exists;
5. reuse established patterns where appropriate;
6. identify impacted components;
7. identify required tests;
8. identify migrations/compatibility risks;
9. surface technical unknowns.

ChatGPT MUST NOT:

- change product behavior to simplify implementation;
- add unrelated refactors;
- replace architecture without ADR/approval;
- add material dependencies without justification;
- broaden scope silently.

---

# 24. Task Statuses

Use:

```text
TODO
READY
IN_PROGRESS
BLOCKED
DONE
CANCELLED
```

Allowed transitions:

```text
TODO
 ↓
READY
 ↓
IN_PROGRESS
 ├──→ BLOCKED
 │      ↓
 │   IN_PROGRESS
 │
 └──→ DONE

TODO / READY
 └──→ CANCELLED
```

Rules:

```text
TODO → READY
only when dependencies and specification are satisfied.

READY → IN_PROGRESS
when implementation actually begins.

IN_PROGRESS → BLOCKED
must include blocker reason.

BLOCKED → IN_PROGRESS
only when blocker is resolved.

IN_PROGRESS → DONE
only after completion criteria, tests and documentation sync.

DONE
must never mean "code was generated".
```

---

# 25. Task Selection Priority

When choosing work:

```text
1. If the user explicitly selected a valid task:
   → use that task.

2. Else if STATE.md identifies an IN_PROGRESS task:
   → resume it.

3. Else if STATE.md identifies a BLOCKED task:
   → check whether blocker is resolved.
   → if resolved, resume it.
   → otherwise leave blocked.

4. Else:
   → select the first eligible READY task
     whose dependencies are satisfied.

5. Never start a second implementation task
   merely because another READY task exists.
```

This rule overrides any generic instruction to "select a READY task".

---

# 26. Task Sizing

A task is too large if ChatGPT cannot reasonably:

- explain the change;
- identify affected files;
- implement coherently;
- test it;
- validate against explicit criteria;

within one controlled development iteration.

Split oversized tasks.

Prefer vertical behavior slices where practical.

---

# 27. Definition of Ready

A feature is ready when:

```text
[ ] scope clear
[ ] spec approved
[ ] acceptance criteria referenced
[ ] blocking clarifications resolved
[ ] architecture impact understood
[ ] plan approved
[ ] tasks decomposed
[ ] dependencies known
[ ] first task READY or existing task IN_PROGRESS
```

---

# 28. User Intent Classification

Before mutating project artifacts or code, classify the user's intent when it matters.

Use:

```text
DISCUSS
DECIDE
IMPLEMENT
FIX
REVIEW
```

---

## 28.1 DISCUSS

Examples:

```text
"What do you think about anonymous forms?"
"Would option A or B be better?"
```

Behavior:

- analyze;
- compare;
- recommend if useful;
- do NOT mutate repository artifacts unless explicitly requested.

---

## 28.2 DECIDE

Examples:

```text
"Yes, anonymous responses will be allowed."
"Let's use option B."
```

Behavior:

- update authoritative decision/spec artifacts;
- update `STATE.md` if project state changes;
- do NOT automatically implement code unless implementation was also requested.

---

## 28.3 IMPLEMENT

Examples:

```text
"Implement the next task."
"Let's build this feature."
```

Behavior:

- verify Definition of Ready;
- select task using Task Selection Priority;
- implement approved scope;
- test;
- synchronize docs;
- update `STATE.md`.

---

## 28.4 FIX

Examples:

```text
"Fix this bug."
```

Behavior:

- determine expected approved behavior;
- investigate/reproduce;
- register BUG/FIX when appropriate;
- implement correction;
- add regression test;
- validate.

If expected behavior is already canonical, fixing its violation does NOT require a new product approval.

---

## 28.5 REVIEW

Examples:

```text
"Review this implementation."
"Check the spec against code."
```

Behavior:

- inspect only by default;
- report issues;
- do NOT change behavior unless explicitly requested.

---

# 29. Phase 10 — Implementation Protocol

Before modifying code:

```text
1. Read GERA_SDD.md.
2. Read and integrity-check specs/STATE.md.
3. Read constitution.md if it exists and is relevant.
4. Identify active phase/feature.
5. Read feature spec.md.
6. Confirm spec permits implementation.
7. Read plan.md.
8. Read tasks.md.
9. Select task using Task Selection Priority.
10. Inspect relevant code/tests.
11. Check blocking clarifications.
12. Mark task IN_PROGRESS if starting.
13. Implement approved scope only.
14. Add/update tests.
15. Run appropriate validation.
16. Compare result against FR/AC.
17. Update task status.
18. Synchronize specs/plan if needed.
19. Record execution evidence.
20. Update STATE.md.
```

---

# 30. Scope Discipline

When implementing one task, do not silently implement unrelated tasks.

If adjacent issues are discovered:

```text
bug           → BUG-* / FIX-*
debt          → DEBT-*
missing rule  → CL-* or spec change
future idea   → backlog
```

Do not expand scope invisibly.

---

# 31. Code Generation Rules

Generated code MUST:

- follow repository conventions;
- reuse appropriate abstractions;
- avoid speculative abstractions;
- avoid unused extensibility;
- keep responsibilities clear;
- avoid duplicated business rules;
- handle expected failures explicitly;
- respect security boundaries;
- remain testable;
- stay consistent with approved plan.

Prefer the smallest correct change.

---

# 32. Dependency Rule

Before adding a dependency/service evaluate:

- why needed;
- whether existing stack can solve it;
- maintenance cost;
- security impact;
- licensing;
- deployment impact;
- whether ADR is required.

Material dependencies require justification.

---

# 33. Database Change Rule

Schema changes MUST document when applicable:

- migration;
- nullability;
- defaults;
- constraints;
- indexes;
- data migration;
- backward compatibility;
- rollback/recovery.

Do not assume destructive schema changes are acceptable.

---

# 34. API Change Rule

API changes SHOULD identify:

- route/operation;
- request schema;
- response schema;
- errors;
- authentication;
- authorization;
- validation;
- compatibility;
- tests.

Breaking changes must be explicit.

---

# 35. Security Rule

Security-sensitive behavior MUST NOT be inferred from convenience.

Authorization rules require explicit specification.

Examples:

- who may view a form;
- who may edit;
- who may view responses;
- who may delete data;
- anonymous submission;
- public links;
- retention.

Security-sensitive ambiguity is blocking.

---

# 36. Testing Strategy

Use test layers according to risk:

- unit;
- integration;
- API;
- contract;
- component;
- end-to-end;
- migration;
- security;
- regression.

Not every feature requires every layer.

Tests SHOULD reference requirement/criterion IDs when practical.

---

# 37. Regression Rule

Every bug fix SHOULD add/update a regression test when technically reasonable.

A bug is not fully corrected only because one manual example works.

---

# 38. Execution Evidence

After implementation/testing, record evidence.

Recommended format:

```text
VALIDATION EVIDENCE

Commands executed:
- ...

Results:
- ...

Not executed:
- ...

Reason:
- ...
```

Allowed result labels include:

```text
PASS
FAIL
NOT RUN
BLOCKED
```

Never claim:

```text
"probably passes"
"should pass"
```

as equivalent to executed validation.

If a test could not run, say `NOT RUN` and explain why.

---

# 39. Definition of Done

Applicable items:

```text
[ ] approved behavior implemented
[ ] acceptance criteria satisfied
[ ] relevant tests added/updated
[ ] relevant tests pass or explicit NOT RUN/BLOCKED recorded
[ ] error paths considered
[ ] security implications reviewed
[ ] no blocking clarification remains
[ ] documentation synchronized
[ ] no undocumented behavior change
[ ] new debt recorded
[ ] execution evidence recorded
```

---

# 40. Phase 11 — Validation + Release

Each implemented feature SHOULD have:

```text
validation.md
```

It SHOULD record:

- feature ID;
- date;
- result;
- validated commit;
- requirement traceability;
- acceptance-criterion evidence;
- automated tests;
- manual validation;
- known limitations;
- remaining debt;
- deviations from plan;
- release status.

Detailed template SHOULD live in:

```text
specs/templates/validation.template.md
```

---

# 41. Definition of Validated

A feature is validated when:

```text
[ ] implementation exists
[ ] acceptance criteria verified
[ ] relevant tests pass or approved limitations documented
[ ] validation evidence recorded
[ ] deviations documented
[ ] specs reflect approved behavior
[ ] no release-blocking defect remains
[ ] validated commit recorded
```

---

# 42. Spec-vs-Code Review

Periodically and before major releases compare:

```text
Approved Spec
     ↕
Current Code
     ↕
Tests
```

Look for:

- requirements without implementation;
- implementation without requirement;
- stale source-file references;
- outdated architecture;
- stale tests;
- unresolved clarifications;
- undocumented behavior;
- resolved debt still marked open.

A review MUST surface discrepancies before modifying authority artifacts.

---

# 43. Reverse SDD

Primary mode:

```text
specification → implementation
```

When undocumented code already exists:

```text
implementation
      ↓
document observed behavior
      ↓
review
      ↓
decide canonical behavior
```

Reverse-engineered specs MUST say:

```text
Type: Reverse-engineered
```

They describe current reality, not automatically desired future behavior.

---

# 44. Bug Workflow

When a defect is reported:

```text
1. Capture expected behavior.
2. Capture observed behavior.
3. Link expected behavior to spec/AC when available.
4. Reproduce or gather evidence.
5. Identify root cause when possible.
6. Register BUG.
7. Define FIX and acceptance criteria.
8. Implement smallest safe correction.
9. Add regression test.
10. Validate.
11. Update spec only if approved behavior changed.
```

If expected behavior is already approved, no new product approval is required merely to correct the defect.

---

# 45. Tech Debt

Project-level tracking:

```text
specs/TECH_DEBT.md
```

Each debt item SHOULD contain:

- ID;
- status;
- severity;
- origin;
- description;
- impact;
- proposed resolution;
- resolution criteria.

Resolved debt remains historically visible.

---

# 46. FIX Backlog

Use:

```text
specs/FIX_BACKLOG.md
```

Each FIX SHOULD contain:

- status;
- priority;
- type;
- related bug/debt;
- module;
- problem;
- root cause if known;
- chosen resolution;
- acceptance criteria;
- affected files;
- tests;
- follow-up;
- completed date when done.

Do not mark completed until acceptance criteria are verified.

---

# 47. Refactor Rule

A pure refactor preserves observable behavior.

Before refactor:

- identify behavior that must remain unchanged;
- ensure useful tests exist;
- define technical objective.

After refactor:

- run behavior-preservation tests;
- update `plan.md`;
- create ADR if architecture materially changes.

If observable behavior changes, update `spec.md`.

---

# 48. SPIKE Rule

Use:

```text
SPIKE-*
```

for bounded experiments.

A spike defines:

- question;
- scope boundary;
- expected evidence;
- decision it informs.

Spike code is not automatically production code.

---

# 49. Approval Gates

Explicit approval is required for material baselines and decisions:

- product requirement baseline;
- MVP scope;
- material UX decision;
- material architecture decision;
- feature spec before implementation;
- implementation plan before coding;
- breaking/destructive change.

Routine non-blocking work inside approved scope MAY continue without repeated approval.

Do not turn SDD into approval bureaucracy.

---

# 50. Approval Semantics

When context is unambiguous, phrases such as:

```text
"Aprobado."
"Perfecto, avancemos."
"Queda así."
"Tomemos esta opción."
"Pasemos a la siguiente etapa."
```

may approve the artifact/decision currently under review.

Approval is scoped.

General positive feedback does not approve unrelated decisions.

---

# 51. Change Management

When an approved requirement changes:

```text
1. update authoritative requirement
2. identify affected stories
3. identify affected UX
4. identify affected feature specs
5. identify affected plans/tasks
6. identify code impact
7. identify test impact
8. document material decision if needed
9. update STATE.md
```

Do not patch only the code.

---

# 52. Material Change Rule

Material changes include:

- new user-visible behavior;
- changed authorization;
- changed ownership;
- changed persistence semantics;
- breaking API change;
- major workflow change;
- material dependency;
- architecture direction change;
- removal of supported behavior.

Material changes require spec review.

---

# 53. Fast Path

Low-risk changes may use:

```text
Clarify expected behavior
      ↓
Update requirement/spec if needed
      ↓
Technical plan
      ↓
Task
      ↓
Implement
      ↓
Test
      ↓
Validate
```

Fast path MUST NOT bypass:

- security;
- privacy/data ownership;
- destructive actions;
- breaking changes;
- material architecture decisions.

---

# 54. Execution Authority Boundaries

A request to implement code does NOT automatically authorize every repository or production action.

Default implementation authority may include:

- edit project files;
- create/update tests;
- run local tests;
- update specs;
- update `STATE.md`.

Unless already authorized by an established workflow, explicit user instruction is required for:

- `git commit`;
- `git push`;
- merge;
- deployment;
- production migration;
- destructive production operation;
- deletion of production data;
- irreversible external actions.

Planning a commit/deploy is not the same as executing it.

---

# 55. New Session Protocol

With repository access:

```text
1. Read GERA_SDD.md.
2. If STATE.md is missing → enter BOOTSTRAP MODE.
3. Otherwise read and integrity-check STATE.md.
4. Load context according to active phase.
5. Read constitution.md only when it exists and is relevant.
6. Inspect code only when current work requires it.
7. Report briefly:
   - current phase
   - current milestone
   - active feature
   - active task
   - blocking clarifications
   - next valid action
8. Continue from the next valid step.
```

Do not re-interview the user about documented decisions.

---

# 56. Session End Protocol

Before ending meaningful work:

```text
[ ] decisions documented
[ ] new CL items recorded and typed
[ ] active task status updated
[ ] DEBT/BUG/FIX recorded if needed
[ ] specs synchronized
[ ] execution evidence recorded
[ ] STATE.md updated
[ ] next valid action identifiable
```

Then summarize:

```text
Completed:
Current state:
Pending:
Next valid action:
```

---

# 57. Working Modes

ChatGPT may operate in:

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

Mode does not override lifecycle gates.

---

# 58. Mandatory ChatGPT Behavior

ChatGPT MUST:

- use project artifacts before asking repeated questions;
- distinguish facts, assumptions and recommendations;
- investigate EVIDENCE clarifications before asking the user;
- require a type for every open CL;
- preserve stable IDs;
- keep scope explicit;
- identify requirement changes;
- synchronize docs with behavior;
- run tests when possible;
- record NOT RUN/BLOCKED when tests cannot execute;
- avoid claiming success without evidence;
- stop only work actually blocked by missing decisions;
- keep `STATE.md` current;
- resume IN_PROGRESS work before selecting new READY work unless user directs otherwise.

---

# 59. Prohibited ChatGPT Behavior

ChatGPT MUST NOT:

- invent important requirements;
- silently choose product policy;
- jump from vague idea to production code;
- broaden scope invisibly;
- rewrite architecture opportunistically;
- add material dependencies without justification;
- claim tests passed when not run;
- mark work complete based only on generated code;
- resolve user-owned decisions by assumption;
- hide debt;
- use chat history as the only record of material decisions;
- commit/push/deploy merely because implementation was requested.

---

# 60. `specs/README.md`

`specs/README.md` is the navigation index.

It SHOULD contain:

- SDD purpose;
- module/feature index;
- links to product/UX/architecture/roadmap artifacts;
- debt/fix links;
- naming conventions.

It SHOULD NOT duplicate real-time execution state from `STATE.md`.

---

# 61. SDD Changelog

Use:

```text
specs/CHANGELOG_SDD.md
```

for material baseline changes.

Do not log trivial wording corrections.

---

# 62. Artifact Statuses

## Specs

```text
Draft
Approved
Implemented
Validated
Superseded
```

## Plans

```text
Draft
Approved
Implemented
Superseded
```

## ADRs

```text
Proposed
Accepted
Superseded
Deprecated
```

## Tasks

```text
TODO
READY
IN_PROGRESS
BLOCKED
DONE
CANCELLED
```

Statuses MUST represent reality.

---

# 63. Code Validation Metadata

Forward specs initially use:

```text
Last validated against code: N/A
Validated commit: N/A
```

After implementation/review:

```text
Last validated against code: YYYY-MM-DD
Validated commit: <commit>
```

Behavior-changing merges should update these fields when specs are synchronized.

---

# 64. Decomposition Rule

Split a feature/module when multiple responsibilities make it difficult to:

- reason about;
- specify;
- implement;
- test;
- maintain.

The parent spec may become an index.

Do not decompose prematurely.

---

# 65. Prototype-to-Production Rule

Prototype behavior that becomes approved product behavior MUST be transferred into authoritative artifacts.

Do not expect production implementation to reverse-engineer requirements from prototype code alone.

---

# 66. Release Gate

Before a milestone release:

```text
[ ] P0 scope accounted for
[ ] critical AC validated
[ ] critical automated tests pass
[ ] security-sensitive flows reviewed
[ ] migrations validated
[ ] critical bugs resolved
[ ] critical debt reviewed
[ ] spec/code drift reviewed
[ ] deployment path known
[ ] recovery/rollback considered where relevant
[ ] release status recorded
```

Non-critical accepted debt may remain if explicitly documented.

---

# 67. Initial Project Sequence

For a new Gera Forms repository:

```text
1. Approve GERA_SDD.md.
2. Create STATE.md from STATE.template.md.
3. Create specs/README.md.
4. Run Discovery.
5. Create vision / requirements / glossary.
6. Create user stories + AC.
7. Define MVP scope.
8. Create UX flows/wireframes.
9. Prototype critical flows.
10. Define architecture + constitution.
11. Create first feature spec.
12. Create plan.
13. Create tasks.
14. Implement one task at a time.
15. Validate.
16. Repeat.
```

---

# 68. Default ChatGPT Start Prompt

```text
Read GERA_SDD.md first.

Then:
- if specs/STATE.md exists, read and integrity-check it;
- if it does not exist, enter BOOTSTRAP MODE.

Follow the SDD lifecycle defined in GERA_SDD.md.

Do not invent missing product or architecture decisions.
Use CL-* for unresolved questions.
Every open CL must be typed as DECISION, EVIDENCE or TECHNICAL.
Investigate EVIDENCE clarifications before asking me.
Resume IN_PROGRESS work before selecting new READY work unless I direct otherwise.
Do not implement code unless the active feature satisfies Definition of Ready.
Maintain traceability between requirements, tasks, code and tests.
Do not commit, push, merge, deploy or run destructive production actions unless explicitly authorized or already covered by an established workflow.

Report:
1. current phase,
2. current milestone,
3. active feature,
4. active task,
5. blocking clarifications,
6. next valid action.
```

---

# 69. Process Health Review

Periodically verify:

```text
[ ] specs help implementation
[ ] decisions are easy to locate
[ ] IDs are traceable
[ ] new session can resume from STATE.md
[ ] STATE.md matches authoritative artifacts
[ ] specs match code
[ ] CLs are typed
[ ] tasks are small enough
[ ] IN_PROGRESS work resumes correctly
[ ] tests link to behavior
[ ] authoritative text is not duplicated
[ ] low-risk work is not over-bureaucratic
```

If process becomes bureaucratic, simplify while preserving:

- decision safety;
- traceability;
- code/spec consistency;
- security.

---

# 70. Templates and Playbooks

Detailed templates and specialized workflows SHOULD live outside this core document.

Recommended:

```text
specs/templates/
├── STATE.template.md
├── requirement.template.md
├── user-story.template.md
├── spec.template.md
├── plan.template.md
├── tasks.template.md
├── validation.template.md
├── adr.template.md
└── fix.template.md

specs/playbooks/
├── debug.md
├── refactor.md
├── security-change.md
└── release.md
```

ChatGPT SHOULD load them only when needed.

---

# 71. Versioning

Use semantic-style process versions:

```text
1.0
1.1
1.2
2.0
```

Examples:

```text
1.1 → operational simplification
1.2 → execution hardening
2.0 → material lifecycle/authority redesign
```

---

# 72. Revision History

## 1.2 — Canonical Candidate

Changes from 1.1:

- added Bootstrap Protocol;
- added phase-aware context loading;
- added STATE integrity verification;
- made CL type mandatory;
- added formal task-state transitions;
- added deterministic task-selection priority;
- guaranteed resume of IN_PROGRESS before new READY work;
- added user-intent classification:
  - DISCUSS;
  - DECIDE;
  - IMPLEMENT;
  - FIX;
  - REVIEW;
- clarified that canonical bug fixes do not require redundant product approval;
- added standard execution evidence;
- added explicit `NOT RUN` / `BLOCKED` validation outcomes;
- added Git / merge / deploy / production authority boundaries;
- clarified constitution is optional before Architecture phase;
- moved detailed templates/playbooks out of the core standard;
- retained Forward SDD, Reverse SDD, traceability and drift handling.

## 1.1

Operational simplification and `STATE.md` introduction.

## 1.0

Initial full Gera Forms SDD draft.

---

# 73. Canonical Promotion Criteria

This candidate may be promoted to:

```text
Status: Canonical
```

when a clean-session simulation confirms that ChatGPT can:

```text
[ ] bootstrap a new project without missing-file ambiguity
[ ] resume an existing project from STATE.md
[ ] resume IN_PROGRESS work correctly
[ ] distinguish discussion from decision and execution
[ ] investigate EVIDENCE clarifications before asking
[ ] implement one READY task without scope drift
[ ] fix canonical bugs without redundant approval
[ ] record real validation evidence
[ ] avoid unauthorized commit/push/deploy actions
[ ] finish with STATE.md synchronized
```

---

# 74. Final Operating Contract

```text
1. Understand before designing.
2. Define MVP before deeply designing deferred scope.
3. Separate WHAT from HOW.
4. Keep one authoritative owner per rule.
5. Never silently invent material decisions.
6. Investigate evidence before asking unnecessary questions.
7. Keep project state explicit and verified.
8. Load context according to lifecycle phase.
9. Preserve traceability.
10. Approve material baselines, not every minor action.
11. Resume active work before opening new work.
12. Implement in small tasks.
13. Test observable behavior.
14. Record execution evidence.
15. Keep specs synchronized with code.
16. Record drift, debt and bugs explicitly.
17. Treat repository state as durable memory.
18. Respect Git/deploy/production authority boundaries.
19. Prefer simple process over bureaucracy.
20. Do not use simplicity to bypass security or product decisions.
21. Validate implementation against approved behavior.
22. Iterate until the product goal is achieved.
```

---

**End of GERA_SDD.md — Version 1.2 Canonical Candidate**
