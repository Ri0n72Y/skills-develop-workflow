---
name: sdd-workflow
description: |
  Apply the repository's specification-driven development workflow. Route the work
  to either the software-development or game-development process before creating or
  updating Requirement, System Design, Spec, Task, or Implementation. Preserve
  authority boundaries, keep Discussion non-authoritative, and re-project only the
  downstream artifacts affected by an upstream change.
license: MIT
metadata:
  version: "1.1.0"
---

# SDD Workflow

This file is the entry point for SDD work.

Software development and game development share some authority rules, but they use different working habits and must not be forced through one identical process.

## 1. Select the development mode first

Before substantial SDD work, determine which development mode governs the capability being changed.

### Game development

Use [`references/game-dev.md`](references/game-dev.md) when:

- the repository is primarily a game or interactive game project;
- the request concerns gameplay, world/content design, progression, encounters, levels, presentation, game systems, or engine-side architecture for those systems;
- the repository already treats Game Design as an upstream authority.

Game development is **design-led**. In this mode, Game Design and System Design are normally the user's primary high-frequency working surfaces, while Requirement, Spec, and Task are mostly Agent-projected artifacts that the user reviews and adjusts.

### Software development

Use [`references/software-dev.md`](references/software-dev.md) when:

- the repository is an application, service, library, infrastructure project, plugin, automation tool, developer tool, or other non-game software/product;
- the work is primarily product/behavior/technical delivery rather than game-design iteration.

Software development is normally **Requirement-first**. Requirement and System Design may be collaboratively refined, while Spec and Task remain downstream executable projections.

### Mixed repositories

If a repository intentionally contains both game and ordinary software work, select the reference that governs the capability currently being changed.

Do not ask the user to classify an obviously game or obviously software task.

## 2. Shared authority rules

These rules apply in both modes.

### Authority is directional

Upstream artifacts define intent and constraints. Downstream artifacts project them into progressively more executable form.

Implementation is evidence of current behavior. It does not silently redefine upstream intent.

When a material contradiction appears:

1. identify the earliest authoritative layer that is wrong or stale;
2. repair that layer first;
3. re-project only the descendants that depend on the changed decision;
4. preserve unaffected artifacts and behavior.

### System Design is conditional

Create or update System Design when a capability needs a durable technical decision about ownership, dependency direction, state/data shape, lifecycle, interface/protocol, persistence, runtime integration, or another material architectural boundary.

Do not create architecture merely to complete the document chain.

An already implemented technical boundary may be adopted as a current System Design baseline only after explicit revalidation against the current upstream intent and actual implementation. This does not trigger retrospective Spec or Task backfill.

### Discussion is not executable authority

System Design may contain explicitly labeled `Discussion` sections for future directions, alternatives, scaling concerns, candidate architecture, migrations, or unresolved technical questions.

Discussion preserves technical reasoning but is not an implementation instruction:

- do not project it directly into Spec or Task;
- do not use it to justify speculative abstractions, dependencies, migrations, or compatibility work;
- when a discussed direction becomes current, re-inspect the implementation and current scope, settle the decision, then promote the accepted conclusion into the normative System Design before projecting a Spec.

### Spec is an executable projection

Do not backfill Specs for untouched legacy code.

Create or update a Spec only when a capability is actually being developed, refactored, or replaced.

Spec must not invent product/gameplay scope or material architecture. If it cannot be written without doing so, return to the earliest missing upstream layer.

### Task is decomposition, not design

Task may name concrete files, work order, migrations, commands, and checks. It may not create hidden requirements, gameplay decisions, compatibility promises, or architecture.

### Verification follows impact

Protect meaningful observable behavior, state transitions, data/contracts, lifecycle boundaries, deterministic behavior, and reproduced regressions.

Do not add verification merely for symmetry, test counts, coverage percentage, or platform-matrix size.

### Prefer the smallest durable solution

Reuse existing project mechanisms first, then native platform/engine/language mechanisms, then add the smallest new boundary required by current scope.

Do not build generalized systems solely because future work might need them.

## 3. Editing discipline

Before creating or editing Requirement, System Design, Spec, or Task, identify which layer actually owns the decision.

If the user is actively designing in a human-led upstream layer, help edit that layer directly instead of prematurely pushing the discussion downstream.

Use the selected reference for the domain-specific authority chain, authoring roles, scope modes, artifact expectations, and review checklist.
