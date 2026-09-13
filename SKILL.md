---
name: sdd-workflow
description: |
  Apply the project's specification-driven development workflow. Use when planning,
  restructuring, reviewing, or executing development work that should flow through
  Requirement, System Design, Spec, Task, and Implementation. Route game projects
  to the game-development reference and ordinary software/product projects to the
  software-development reference. Preserve authority boundaries, avoid speculative
  architecture, and re-project only affected downstream artifacts when upstream
  decisions change.
license: MIT
metadata:
  version: "1.0.0"
---

# SDD Workflow

This skill provides a small common workflow shell and two domain-specific references.

Do not force software development and game development through the same authoring habits. They share projection and authority rules, but the upstream creative/design work is different.

## Select the workflow

Choose one reference before doing substantial SDD work:

- **Game development** — read [`references/game-development.md`](references/game-development.md) when the repository is a game, the user is discussing gameplay/world/content design, or the project already has Game Design artifacts.
- **Software development** — read [`references/software-development.md`](references/software-development.md) for applications, services, libraries, infrastructure, tools, plugins, and other non-game software/product work.

When the project type is obvious from the repository and request, select it directly. Do not ask the user to classify an obviously game or obviously software project.

If a repository intentionally contains both kinds of work, use the reference that governs the capability currently being changed.

## Shared rules

These rules apply to both references.

### Authority is directional

Upstream artifacts define intent and constraints. Downstream artifacts project them into progressively more executable form. Implementation is evidence of current behavior; it does not silently redefine upstream intent.

When a material contradiction appears, repair the earliest authoritative layer that is wrong, then re-project only the descendants that depend on that change.

### Preserve unaffected work

A change does not invalidate the whole documentation tree. Revisit only affected Requirement, System Design, Spec, Task, tests, and implementation surfaces.

Remove stale contradictions from current-state documents instead of accumulating patch-note prose inside them.

### System Design is conditional

Create or update System Design when a capability needs a durable technical decision about ownership, dependency direction, state/data shape, lifecycle, interface/protocol, persistence, runtime integration, or another material architectural boundary.

Do not create architecture merely to complete the document chain. A small change that already fits a settled technical structure may proceed without a new System Design document.

An already implemented technical boundary may be adopted as a current System Design baseline only after it has been explicitly revalidated against current upstream intent and the real implementation. This does not trigger retrospective Spec or Task backfill.

### Discussion is not authority

System Design may contain explicitly labeled `Discussion` sections for future directions, alternatives, scaling concerns, candidate architecture, or unresolved technical questions.

Discussion is retained design context, not an implementation instruction:

- do not project it directly into Spec or Task;
- do not use it to justify speculative abstractions, dependencies, migrations, or compatibility work;
- promote a discussed direction into the normative System Design only after the relevant capability enters current scope, the implementation is re-inspected, and the technical decision is actually settled.

### Spec is an executable projection

Do not backfill Specs for untouched legacy code.

Create or update a Spec when a capability is actually being developed, refactored, or replaced. A Spec should contain the smallest contract an implementation agent needs: observable behavior, capability boundary, relevant ownership, contracts/invariants, allowed/prohibited change surface, failure behavior, and proportionate verification.

Spec must not invent product/gameplay scope or material architecture. If it cannot be written without doing so, return to the earliest missing upstream layer.

### Task is decomposition, not design

Tasks may name concrete files, work order, migration steps, commands, and checks. They may not create hidden requirements or architecture decisions.

### Verification follows impact

Protect meaningful behavior, state transitions, data/contracts, and reproduced regressions. Do not add tests merely for symmetry, test counts, coverage percentage, or platform-matrix size.

### Prefer the smallest durable solution

Reuse existing project mechanisms first, then native platform/language mechanisms, and add new abstractions only for a concrete current consumer. Do not build generalized systems solely because future work might need them.

## Output discipline

Before producing a Requirement, System Design, Spec, or Task, identify which layer the requested decision actually belongs to. If the user is actively designing in an upstream human-owned layer, help edit that layer directly rather than prematurely pushing the discussion downstream.

Use the selected reference for the domain-specific authority chain, authoring roles, scope modes, and artifact expectations.
