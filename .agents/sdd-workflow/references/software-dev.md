# Software Development SDD Reference

Use this reference for applications, services, libraries, infrastructure, tools, plugins, automation, and other non-game software/product work.

## Authority chain

The default software-development flow is:

```text
Problem / Product Context
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
Verification / Evidence
```

`Problem / Product Context` may live in user discussion, a product brief, an issue, research notes, or another upstream artifact. It does not need a mandatory document merely to make the chain look complete.

## Working habit

Software development is normally **Requirement-first**.

The user and Agent may collaboratively refine Requirement and System Design. The Agent may draft any layer, but must keep product intent and architectural trade-offs visible for review rather than silently settling material choices inside Spec or code.

Requirement, System Design, Spec, and Task are not equally heavy. Use only the detail required by the actual impact surface.

## Requirement

Requirement defines the accepted implementation-facing scope and observable completion direction.

For an MVP or staged product, distinguish where useful:

- **current must-do** — required for this delivery;
- **can defer** — known but intentionally outside current delivery;
- **future** — plausible later direction, not current scope;
- **needs verification** — assumption requiring research/prototype/evidence;
- **unknown** — unresolved question that must not be silently invented.

Requirement should state behavior, constraints, important exclusions, and acceptance direction. It should not decide module ownership, interfaces, persistence layout, internal data models, factories, service boundaries, or other architecture.

Existing code is implementation evidence. It becomes an owned Requirement baseline only when the behavior is intentionally accepted, not merely because it exists.

## System Design

System Design owns durable software structure when such decisions matter to the current work.

A useful System Design should make the relevant parts of these explicit:

- capability/module ownership;
- data and control flow;
- dependency direction;
- stable versus replaceable boundaries;
- state/data model;
- interfaces and integration points;
- persistence/loading strategy when relevant;
- lifecycle and concurrency/runtime behavior when relevant;
- trust boundaries and failure modes;
- minimum implementation path;
- material trade-offs that would change architecture.

Prefer the smallest architecture that satisfies current Requirement. Do not design the full future system in advance.

### Discussion

Use `Discussion` inside System Design to retain candidate alternatives, scaling directions, possible future integrations, rejected-but-still-relevant options, and unresolved technical questions.

Discussion is not part of the executable authority projected into Spec until it is explicitly settled and promoted into the normative design.

## Spec

Spec translates current Requirement plus any applicable System Design into a local, agent-executable contract.

A Spec should normally answer:

- what behavior must change or remain unchanged;
- which capability/component owns the change;
- what inputs, outputs, state transitions, and invariants matter;
- what callers or integration points are affected;
- what changes are allowed and prohibited;
- how invalid input/failure/rollback should behave;
- what proportionate verification is required.

Do not turn Spec into another architecture document. If a material design decision is still unresolved, return to System Design.

## Task

Task decomposes the approved Spec into executable work.

It may include:

- exact files/modules;
- implementation order;
- schema/migration steps;
- compatibility/removal steps;
- build/test/lint commands;
- rollout or verification sequence.

A Task must not add functionality, compatibility promises, or abstractions that do not exist upstream.

## Validation/prototype work

If an uncertain technical or product question needs a prototype, state the question, minimum experiment, evidence needed, and disposable/provisional parts before implementation.

Do not silently graduate prototype shortcuts into permanent architecture. Once the experiment answers the question, update the earliest authoritative layer and either discard the experiment or convert the accepted result into normal delivery scope.

## Legacy code

Do not backfill complete SDD documentation for untouched legacy code.

When legacy code enters a real change scope:

1. inspect the affected path end to end;
2. identify which existing behavior is intentionally preserved;
3. revalidate any old technical notes against current code and Requirement;
4. create/update System Design only for durable decisions that now matter;
5. write the Spec for the actual change, not for the historical implementation as a whole.

## Review checklist

Before implementation, verify that:

- Requirement contains scope/behavior rather than architecture;
- material architecture is settled in System Design when necessary;
- Discussion has not leaked into executable commitments;
- Spec does not invent scope or architecture;
- Task is only decomposition;
- unaffected behavior/documents remain untouched;
- verification matches the real failure/impact surface.
