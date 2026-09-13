# Game Development SDD Reference

Use this reference for games and game-like interactive projects where gameplay, world/content design, and technical architecture evolve together.

## Authority chain

The default game-development flow is:

```text
Game Idea / Brainstorm
        ↓
Game Design
        ↓
Requirement
        ↓
System Design (when applicable)
        ↓
Spec
        ↓
Task
        ↓
Implementation
        ↓
Playable / Runtime Evidence
```

This is an authority and projection chain, not a rule that every discussion must produce every artifact.

## Authoring habit

Game development uses an intentionally asymmetric human/Agent workflow.

### Human-led, high-frequency authoring surfaces

**Game Design** and **System Design** are the user's primary working documents.

The user is expected to directly write, rewrite, restructure, and frequently revise these layers. Treat them as active design workspaces rather than frozen approval documents.

When working in these layers:

- preserve the user's terminology, distinctions, uncertainty, and design intent;
- help organize, compare, critique, and make decisions without silently completing unresolved design;
- make material trade-offs visible;
- update the document that actually owns the decision;
- do not prematurely translate every idea into implementation scope.

The Agent may draft or edit these documents when asked, but should behave as a design collaborator/editor rather than as the sole author.

### Agent-led projection surfaces

**Requirement, Spec, and Task** are normally generated and maintained primarily by the Agent from approved upstream material, then reviewed and lightly adjusted by the user.

The expected habit is:

```text
user works directly in Game Design / System Design
        ↓
Agent projects settled decisions into Requirement / Spec / Task
        ↓
user reviews, corrects, or makes small adjustments
```

Do not require the user to manually keep downstream projection documents synchronized after every upstream edit. When an upstream decision changes, identify the affected descendants and update only those projections.

Implementation remains downstream evidence and execution, not a design-authority layer.

## Game Design

Game Design is the upstream creative/design authority.

It may contain:

- core loop and player experience;
- gameplay rules and relationships;
- world/content structure;
- progression/economy/content direction;
- presentation and interaction concepts;
- level/encounter/event design;
- future systems and world variants;
- references and design rationale;
- alternatives, experiments, unresolved questions, and intentionally open content slots.

Game Design may be broader than the current implementation version. Do not delete valid future Design merely because it is outside current scope.

Do not constrain Game Design to accidental legacy implementation unless the limitation is intentionally accepted as part of the design.

If a version decision materially changes what the game is or how a gameplay system should work, update Game Design first rather than hiding the change in Requirement, Spec, or code.

## Requirement

Requirement is an implementation-facing projection of sufficiently settled Game Design, not the place where game design is invented.

Requirement may contain two kinds of content:

### Owned baseline

An **Owned baseline** records already implemented behavior that has been explicitly accepted as consistent with current Game Design and should not be broken accidentally.

Existing code does not become owned merely because it exists.

Recognizing an owned baseline does not require retroactively creating System Design, Spec, or Task for untouched implementation.

### Current development Scope

When starting new work, Requirement selects a current version Scope from Game Design.

A development Scope uses one of two modes:

- **Delivery Scope** — implement sufficiently settled design as a capability intended to remain;
- **Validation Scope** — build the smallest useful playable/observable experiment needed to answer a concrete design question.

A Validation Scope should state:

- the design question or hypothesis;
- the minimum experiment;
- what evidence/play result answers the question;
- what is intentionally provisional or disposable.

Prototype code is evidence for Game Design. It does not become permanent Requirement or architecture merely because the experiment works.

After validation:

1. discard/retire the experiment and update Game Design with the result; or
2. update Game Design, then extract a Delivery Scope for the version worth keeping and hardening.

Requirement should describe what must be preserved, implemented, or validated and the observable completion direction. Do not put module ownership, scene/script boundaries, interfaces, internal data models, factories, or other software architecture into Requirement.

## System Design

System Design is the user's other primary high-frequency design surface.

It owns durable technical/software decisions for current accepted capabilities, including:

- capability/system ownership;
- scene/script/module boundaries;
- dependency direction;
- state/data model;
- runtime lifecycle;
- interfaces/protocols;
- persistence/loading strategy;
- integration boundaries between gameplay layers;
- deterministic/runtime contracts;
- material failure/rollback behavior;
- technical trade-offs worth preserving beyond one Task.

Before changing these boundaries, inspect the affected implementation path end to end.

Prefer existing project mechanisms, then engine/language-native mechanisms, then the smallest new boundary required by current scope.

Do not create generalized architecture merely because future Game Design may contain more worlds, modes, content, or rule variants. Future replaceability is a design direction; a current abstraction requires a concrete current consumer.

### Existing architecture baseline

An already implemented technical boundary may be promoted into current System Design after explicit revalidation against:

1. current Game Design;
2. current Requirement/Owned baseline;
3. actual implementation behavior.

This is useful when converting a prototype/legacy project into an SDD-ready project. It does not trigger retroactive Specs or Tasks.

### Discussion

System Design may deliberately retain future technical thinking under an explicit `Discussion` heading.

Use Discussion for:

- candidate future architecture;
- alternatives and trade-offs not yet selected;
- scaling concerns;
- migration possibilities;
- future engine/ECS/data-oriented options;
- unresolved integration questions;
- technical consequences of possible future Game Design.

Discussion is **not current architecture authority**.

Do not project Discussion directly into Spec/Task and do not implement abstractions merely because a Discussion records them.

When a discussed direction becomes relevant:

```text
Game Design / Requirement selects the capability
        ↓
re-inspect current implementation
        ↓
resolve the technical choice with the user
        ↓
promote the settled conclusion out of Discussion
        ↓
Spec
```

This lets Game Design and System Design remain useful long-lived thinking spaces without turning every future idea into current engineering scope.

## Spec

Spec is normally Agent-authored from current Requirement plus applicable normative System Design.

It should be locally executable and limited to the capability actually being developed/refactored/replaced.

A Spec should contain only what the implementation agent needs, such as:

- observable behavior;
- capability boundary and relevant owner;
- inputs/outputs and state transitions;
- contracts/invariants;
- allowed/prohibited change surface;
- failure/rollback behavior;
- compatibility requirements that are truly in scope;
- proportionate automated/manual/playable verification.

Do not backfill Specs for untouched legacy code.

Do not copy Game Design brainstorming or System Design Discussion into Spec. If implementation needs an unresolved gameplay or architecture choice, go back upstream.

## Task

Task is normally Agent-authored from Requirement + applicable System Design + Spec.

It may contain exact scenes/scripts/files, implementation order, migrations, cleanup steps, tests, editor/headless commands, and manual play checks.

Task is not allowed to decide gameplay or architecture.

## Playable validation versus software verification

Game development has two distinct evidence types.

### Software correctness

Use automated/runtime checks for independently meaningful technical failures: contracts, state transitions, persistence, deterministic behavior, regressions, lifecycle, and integration boundaries.

### Design evidence

Validation Scope may require qualitative play evidence rather than only software tests. The goal is first to ensure the prototype reliably exposes the intended design question, then evaluate the play result.

Do not confuse “the prototype runs correctly” with “the game design hypothesis is good.”

## Legacy/prototype conversion

When turning an existing prototype into an SDD-ready project:

1. establish current Game Design authority before treating old behavior as permanent;
2. identify which existing behavior aligns with that Design and claim only that behavior as Requirement Owned baseline;
3. reject accidental/obsolete implementation behavior from Requirement even if it currently works;
4. revalidate durable technical boundaries worth preserving into System Design;
5. keep future technical reasoning as Discussion when still useful;
6. do not backfill Specs/Tasks for untouched old code;
7. use the first real new/refactor capability to verify that the full chain works in practice.

## Suggested repository layout

A useful default layout is:

```text
docs/
├─ design/
│  ├─ README.md
│  └─ ... game-design documents
├─ requirements.md
├─ system-design/
│  ├─ README.md
│  └─ <capability>.md
└─ specs/
   ├─ README.md
   └─ <capability>.md
```

Task can remain in the active issue/PR unless a durable task document is specifically useful.

The layout is a convention, not authority by itself. Existing repository conventions may be retained when their roles are equally clear.

## Review checklist

Before implementation, verify that:

- gameplay/content decisions live in Game Design;
- current version scope is projected into Requirement rather than invented there;
- material architecture is either already settled or resolved in System Design;
- System Design Discussion is visibly non-authoritative;
- Spec contains no new gameplay or architecture decisions;
- Task only decomposes approved work;
- implementation does not become upstream authority by accident;
- only affected descendants are re-projected after upstream changes;
- validation evidence and software correctness evidence are not conflated.
