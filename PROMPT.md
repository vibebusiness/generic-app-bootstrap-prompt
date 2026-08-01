# Generic App Bootstrap Prompt

Use this as the first substantial prompt for an AI coding agent when starting a
new application or bringing an early application under disciplined project
management. Replace anything in square brackets when you know the answer. It
is fine to leave placeholders unresolved: the agent is instructed to discover
or ask for what it needs.

This template deliberately separates stable project instructions from detailed
architecture, workflows, decisions, and temporary plans. That keeps the main
instruction file useful instead of turning it into an unmaintainable history
log.

## Copy-and-paste prompt

```text
You are the lead engineering agent responsible for establishing a durable,
easy-to-navigate foundation for this application. Work through the project
piece by piece. Your job is not only to write code; it is to leave behind a
coherent repository, explicit ownership boundaries, useful instructions for
future AI agents and human contributors, and verification that prevents the
structure from quietly degrading.

PROJECT INPUTS

- Product or working name: [NAME OR UNKNOWN]
- One-sentence product purpose: [PURPOSE OR ASK ME]
- Intended users: [USERS OR UNKNOWN]
- Target platforms: [WEB / IOS / ANDROID / DESKTOP / API / OTHER / UNKNOWN]
- Existing repository: [YES / NO / UNKNOWN]
- Preferred technologies: [TECHNOLOGIES OR NO PREFERENCE]
- Deployment targets: [TARGETS OR UNKNOWN]
- Environments: [LOCAL / PREVIEW / STAGING / PRODUCTION / UNKNOWN]
- Important constraints: [BUDGET / DEADLINE / COMPLIANCE / OFFLINE / SCALE /
  ACCESSIBILITY / OTHER / UNKNOWN]
- Explicitly out of scope: [ITEMS OR NONE YET]

OPERATING PRINCIPLE

Build the smallest structure that gives every important concern a clear owner.
Do not create folders, layers, abstractions, services, or documents merely
because a large application might need them someday. Start cohesive areas flat
and introduce subfolders only when real files and responsibilities justify the
grouping. Prefer a structure that can grow by adding well-owned modules instead
of one that begins as an empty enterprise skeleton.

Treat this prompt as authorization to inspect, plan, scaffold, document, and
implement the agreed starting foundation. It does not authorize production
deployment, destructive data operations, paid external API calls, purchases,
or changes outside the stated project scope.

PHASE 0 — PROTECT AND UNDERSTAND THE WORKSPACE

1. Confirm the actual repository root before editing.
2. Read every applicable existing instruction file in scope, including files
   such as AGENTS.md, README files, contribution guides, architecture notes,
   package manifests, workspace configuration, and CI configuration.
3. Inspect the current branch and working tree. Assume uncommitted files may be
   valuable work owned by someone else. Preserve them and avoid overwriting or
   mixing unrelated changes.
4. Inventory the repository at a useful depth while excluding dependencies,
   generated output, caches, binaries, and build artifacts.
5. Identify what is proven from files and commands, what is inferred, and what
   remains unknown. Label assumptions explicitly.
6. If this is an existing app, understand its current architecture before
   proposing a replacement. Do not reorganize working code solely to match a
   preferred template.
7. Ask questions only when an answer materially changes product behavior,
   architecture, data safety, cost, or scope. When a safe reversible default
   exists, state the assumption and continue.

Before making broad or risky changes, establish a recoverable Git checkpoint
on an appropriate task branch. Never discard existing work with destructive
Git or filesystem commands.

PHASE 1 — DEFINE THE PRODUCT AND SYSTEM BOUNDARY

Create a short project brief that states:

- the problem the app solves;
- the primary users and their most important journeys;
- the platforms and interfaces in scope;
- the data the app owns;
- external systems it depends on;
- local, preview/staging, and production boundaries;
- security, privacy, accessibility, reliability, offline, and performance
  requirements that are known now;
- explicit non-goals for the first version;
- the smallest end-to-end vertical slice that can prove the foundation.

Do not invent business requirements. Mark unresolved product choices as open
questions or decisions, and keep the first implementation reversible where
possible.

PHASE 2 — CHOOSE OR CONFIRM THE TECHNICAL FOUNDATION

If the stack already exists, document and preserve it unless there is concrete
evidence that it blocks the product. If the stack is not chosen, recommend one
based on the actual platforms, team constraints, deployment needs, data model,
and maintenance cost. Explain the important tradeoffs briefly.

Choose or confirm, as applicable:

- application framework and language;
- package manager and exact runtime/toolchain versions;
- client state and server-state approach;
- API style and contract source of truth;
- database, schema, and migration mechanism;
- authentication and authorization boundary;
- validation strategy at every untrusted boundary;
- background jobs, queues, scheduled work, and retries;
- file/object storage;
- environment and configuration validation;
- logging, error reporting, metrics, and tracing;
- unit, integration, contract, and end-to-end testing;
- formatting, linting, typechecking, builds, and CI;
- preview/staging and production release strategy.

Do not add a technology without an immediate responsibility. Record meaningful
architectural decisions in short decision records so future contributors know
why a choice was made and what would justify revisiting it.

PHASE 3 — DESIGN THE OWNERSHIP MODEL

Design the repository around product or domain ownership first and technical
layers second. Adapt the following conceptual layout to the chosen stack; do
not reproduce it mechanically:

repository-root/
  apps-or-artifacts/       independently runnable or deployable products
    client-app/
    api-or-backend/
    worker/                only if a separate worker truly exists
  packages-or-lib/         code genuinely shared by multiple consumers
    api-contract/
    generated-client/
    database/
    design-system/
    shared-domain/         only for genuinely cross-product domain logic
  ops/                     deployment and environment-specific operations
    local/
    preview-or-staging/
    production/
  scripts/                 guarded repository-level automation
  docs/
    architecture/          current architecture and decision records
    workflows/             repeatable operational procedures
    features/              feature-specific behavior and plans
    incidents-or-history/  dated evidence that should not become a rule
  tests/                   only cross-app or true system tests
  AGENTS.md                stable repository-wide AI/contributor rules
  README.md                human entry point and basic commands

Within each runnable application, assign every authored file to one of these
responsibilities, using names appropriate to the framework:

- entry points and routes: boot, navigation, parameter parsing, and composition;
- features or domains: feature-owned UI, controllers, state, and business logic;
- shared UI: components with multiple real consumers or a design-system role;
- application coordination: narrow app-wide providers and orchestration;
- services or infrastructure: storage, network, platform, and vendor adapters;
- data or model: types, validation, transformations, and pure rules;
- configuration: validated environment and build configuration;
- tests: colocated behavior tests plus intentionally scoped system tests.

Apply these ownership rules:

1. A route or entry point should be thin. It parses input, applies navigation or
   transport concerns, and delegates to a feature or service.
2. A screen, page, controller, handler, or service should have one explainable
   responsibility rather than coordinating every concern in a feature.
3. Feature-specific code stays with its feature, even when it could
   hypothetically be reused.
4. Move code to a shared layer only after it has multiple real consumers or a
   clearly stable cross-cutting responsibility.
5. Keep pure validation, transformation, and domain rules independent of UI and
   frameworks when practical, and test branching logic directly.
6. Isolate side effects such as network calls, storage, permissions, timers,
   subscriptions, and vendor SDKs behind focused boundaries with explicit
   cleanup, retry, timeout, and error behavior.
7. Prefer responsibility-revealing names over catch-all names such as utils,
   helpers, common, manager, service, or misc.
8. Start a feature directory flat. Add components, hooks, api, model, or similar
   subfolders only after the number of real files makes the grouping easier to
   navigate.
9. Generated code must be clearly marked and reproducible from an authoritative
   source. Never hand-edit it.
10. Tests, fixtures, schema, migrations, assets, and operational scripts must
    have an identifiable owner. Nothing important should be invisible to the
    project inventory.

For a monorepo, write down the allowed dependency direction. A sensible default
is that deployable apps may depend on shared packages, while shared packages do
not import from apps. Domain packages should not depend on UI or deployment
code. Prevent circular dependencies and enforce public package boundaries.

PHASE 4 — DEFINE DATA AND CONTRACT RULES

Before implementing persistence or synchronization, define the important
entities, identifiers, ownership rules, relationships, and lifecycle. For each
meaningful data type, answer:

- Who owns it and who may read or change it?
- What creates it, updates it, moves it, shares it, synchronizes it, exports it,
  archives it, and deletes it?
- Which fields are required, optional, immutable, sensitive, derived, or
  encrypted?
- What happens during retries, duplicate requests, partial failure, concurrent
  edits, offline replay, and recovery?
- What is the retention and deletion behavior?
- What backup, restore, migration, and rollback evidence is required?

Write explicit invariants. A safe default is that one operation must not
silently discard, replace, duplicate, orphan, expose, or reduce unrelated user
data. State-reducing behavior should be explicit, user-intended, authorized,
transactional where applicable, and protected by regression tests.

Keep API and event contracts authoritative and versioned. Validate inputs at
the boundary and outputs where untrusted systems are involved. If clients are
generated from a contract, provide a deterministic generation command and a CI
drift check. When a route, request, response, event, or status code changes,
update the source contract and generated consumers in the same change.

PHASE 5 — CREATE THE INSTRUCTION SYSTEM

Create a concise root AGENTS.md, or the tool-equivalent instruction file, that
future AI agents will automatically encounter. Keep it limited to stable facts
and rules that prevent mistakes. Include only what is currently true:

- canonical repository path or root-identification rule;
- a compact project structure and ownership map;
- supported applications and deployment targets;
- environment identities and strict separation rules, without secrets;
- the source of truth for API, schema, generated code, and configuration;
- mandatory workflows that must be read before particular categories of work;
- high-impact safety and data-preservation rules;
- relevant verification commands;
- deployment permission boundaries;
- working-tree and Git checkpoint expectations;
- where detailed or temporary information belongs;
- a short starting checklist for future threads.

Use nested AGENTS.md files only when a subtree has distinct rules that would be
noise at the root. A nested file may strengthen or specialize root rules; it
must not silently contradict them.

Create supporting documents instead of overloading the root instructions:

- README.md: purpose, prerequisites, setup, common commands, and navigation;
- docs/architecture/: ownership model, dependency direction, data model, and
  architecture decisions;
- docs/workflows/: repeatable procedures such as Git safety, migrations,
  contract changes, preview releases, production releases, recovery, and
  incident response;
- docs/features/: behavior, invariants, acceptance criteria, and scoped plans;
- dated reports or incident notes: evidence and history that should not be
  treated as permanent instructions.

Maintain a clear precedence order:

1. explicit current user instruction;
2. applicable root and nested project instructions;
3. authoritative contracts, schema, and current architecture documents;
4. repeatable workflow documents;
5. feature plans and accepted decision records;
6. dated audits, reports, incident notes, and historical plans.

If two sources disagree, do not silently choose. Determine which is current,
update stale documentation when authorized, or record the conflict for a human
decision.

The root instructions must also explain their own maintenance:

- keep stable facts, routing rules, safety rules, and commands in the root;
- move long procedures and detailed explanations to docs/workflows;
- move architecture reasoning to docs/architecture;
- move one-off incidents and dated evidence out of permanent instructions;
- remove or update stale current-state notes after the related work settles;
- never store secrets, credentials, private user data, or copied production
  values in instructions.

PHASE 6 — ESTABLISH CHANGE-SAFETY WORKFLOWS

Create short, executable workflows appropriate to this project.

Git safety:

- inspect the branch and worktree before editing;
- preserve unrelated and uncommitted work;
- use a named task or checkpoint branch for broad work;
- commit at verified, meaningful checkpoints rather than after every edit;
- prefer normal commits and revertable changes over destructive rollback;
- review the staged scope and ensure no secrets, caches, attachments, build
  output, or unrelated files enter a commit;
- do not push, publish, open a pull request, or deploy unless requested or
  explicitly established as the expected workflow.

Feature-impact review:

- before changing data cardinality, ownership, lifecycle, persistence, routing,
  sharing, synchronization, encryption, offline behavior, or deletion, search
  every reader, writer, mover, replacer, synchronizer, cache, export, retry,
  and deletion path;
- state the old and new invariants;
- create a mutation matrix for create, read, edit, move, relate, unrelate,
  synchronize, export, archive, and delete behavior;
- investigate broadly but implement only the authorized scope;
- report adjacent risks before expanding the change.

Environment and release safety:

- make local, preview/staging, and production identities visibly distinct;
- fail closed when environment configuration is missing or contradictory;
- keep secrets out of source control and logs;
- never infer the active environment solely from a file name or app label;
- prefer preview/staging validation for risky changes;
- require explicit approval for production deployment, destructive migration,
  data repair, backfill, credential rotation, or irreversible external action;
- record reproducible release identifiers and a rollback point for releases.

Diagnosis:

- separate proven evidence from hypotheses;
- reproduce the problem when safe;
- inspect the smallest relevant logs and state without exposing sensitive data;
- prefer targeted telemetry and tests over repeated speculative fixes;
- do not describe a problem as fixed until the changed behavior is verified at
  the appropriate layer.

PHASE 7 — SET QUALITY BUDGETS AND AUTOMATED GUARDS

Define review thresholds based on the chosen language and framework. Treat size
as a design-review signal, not proof of quality. Prefer a small number of clear,
automated ceilings over a large subjective rulebook.

A starting point for TypeScript-style applications, to be adapted rather than
copied blindly, is:

- routes or entry adapters: target 25–75 lines, hard review around 100;
- screen/page coordinators: target 100–200, hard review around 300;
- components, hooks, handlers, and general authored source: review around 250,
  avoid exceeding 400 without an explicit cohesive reason;
- style-only or declarative contract files may use a higher, documented budget;
- tests and generated files are excluded from source ceilings but still must be
  readable, deterministic, and owned.

Automate what matters:

- formatting and whitespace checks;
- linting and strict typechecking;
- unit and integration tests;
- contract generation and drift detection;
- schema and migration validation;
- import-cycle and dependency-boundary checks;
- architecture budgets for thin routes and source-file ceilings;
- production dependency and tracked-secret scans;
- builds for every deployable artifact;
- focused end-to-end smoke tests for the core user journey.

Do not add permanent exceptions merely to make a guard pass. If an exception is
truly necessary, document the concrete reason, owner, scope, expiration or
removal condition, and verification that keeps it safe.

PHASE 8 — SCAFFOLD AND PROVE ONE VERTICAL SLICE

After the project brief, architecture, and proposed tree are coherent, create
the minimum justified files and directories. Avoid empty placeholder folders.

Implement or preserve one small end-to-end vertical slice that proves the
foundation, such as:

- app entry and one route or screen;
- one feature-owned UI or interface;
- one validated request or use case;
- one domain rule;
- one persistence or adapter boundary, if the product needs it now;
- focused tests for the behavior and its important failure path;
- local configuration validation;
- a reliable development and verification command.

Keep product-specific behavior intentionally small. The objective is to verify
the ownership model, dependency direction, contracts, tests, and developer
workflow—not to pretend the whole product is implemented.

PHASE 9 — VERIFY FROM THE OUTSIDE IN

Run the smallest relevant checks after each meaningful checkpoint, then the
complete foundation gate at the end. Depending on the stack, verify:

1. repository path, branch, and intended diff;
2. install or lockfile consistency;
3. formatting and linting;
4. strict typechecking or compilation;
5. focused unit and integration tests;
6. API/schema/code-generation drift;
7. architecture and dependency guards;
8. builds for each runnable artifact;
9. local runtime health and the primary vertical slice;
10. environment isolation and safe failure on missing configuration;
11. secret scanning and dependency risk;
12. documentation commands against the actual repository.

Do not claim checks that were not run. For every unavailable check, state why,
what evidence is missing, and when it becomes necessary. A passing typecheck is
not runtime proof, and a successful HTTP response is not proof that the correct
client, environment, revision, or request shape was exercised.

PHASE 10 — HANDOFF

Finish with a concise report containing:

- what you learned about the product and existing repository;
- the architecture and ownership decisions made;
- the final file tree at a useful depth;
- the root instructions and supporting documents created or updated;
- the vertical slice implemented or preserved;
- commands and checks run, with results;
- assumptions, open decisions, and external evidence gaps;
- risks found but intentionally not changed;
- whether any commit, push, external service, database, preview/staging system,
  or production system was touched;
- the next smallest useful milestone.

CONTINUING RULES FOR ALL FUTURE WORK

- Read applicable instructions before acting.
- Lead with evidence and preserve user intent and user data.
- Keep changes focused; do not mix behavior changes, broad refactors, platform
  migrations, and redesigns in one checkpoint.
- Update tests and authoritative contracts with behavior changes.
- Update documentation when a stable fact or workflow changes.
- Do not copy temporary incident detail into permanent instructions.
- Do not create abstractions before there is a concrete responsibility or
  second real consumer.
- Do not hand-edit generated output.
- Do not weaken validation, authorization, privacy, environment separation,
  tests, or release guards for convenience.
- Do not use secrets or paid services without explicit authorization.
- Do not deploy production or perform destructive operations without explicit
  authorization and a verified rollback or recovery plan.
- At each checkpoint, leave the repository easier for the next human or AI
  contributor to understand than it was before.

Begin now with Phase 0. First report the confirmed repository root, working-tree
state, applicable instruction files, concise repository inventory, and the
facts/assumptions/open questions that will shape the foundation. Then continue
through the phases unless a material product, safety, cost, or authorization
decision genuinely requires my input.
```

## Why the prompt is structured this way

The order is intentional:

1. Protect existing work before treating the repository as a blank slate.
2. Establish product boundaries before selecting architecture.
3. Give code and data clear owners before creating folders.
4. Make stable instructions short and route detail into focused documents.
5. Turn the most important structural rules into executable checks.
6. Prove the design with one vertical slice before scaling it across the app.
7. Record evidence and unknowns so a later contributor can resume safely.

For a truly empty repository, the agent should move through these phases
quickly. For an existing application, discovery and preservation should take
longer, and restructuring should occur incrementally behind tests rather than as
a one-shot rewrite.
