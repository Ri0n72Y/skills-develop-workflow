# SDD Development Workflow Skill

A reusable `sdd-workflow` skill with separate references for software development and game development.

## Structure

```text
SKILL.md
references/
├─ software-development.md
└─ game-development.md
```

`SKILL.md` contains only the shared SDD rules and routing logic. It selects one domain reference before substantial workflow work.

## Software development

Default flow:

```text
Problem / Product Context
→ Requirement
→ System Design (when applicable)
→ Spec
→ Task
→ Implementation
→ Verification / Evidence
```

Software work is normally Requirement-first. Requirement and System Design may be collaboratively drafted and reviewed; Spec and Task remain downstream executable projections.

See [`references/software-development.md`](references/software-development.md).

## Game development

Default flow:

```text
Game Idea / Brainstorm
→ Game Design
→ Requirement
→ System Design (when applicable)
→ Spec
→ Task
→ Implementation
→ Playable / Runtime Evidence
```

Game development intentionally uses a different authoring habit:

- **Game Design** and **System Design** are human-led, high-frequency working surfaces. The user directly writes and repeatedly revises them, with the Agent acting as collaborator/editor.
- **Requirement**, **Spec**, and **Task** are normally Agent-maintained projections of settled upstream decisions, with the user reviewing and making targeted adjustments.
- upstream edits should re-project only affected descendants; the user should not need to manually synchronize every downstream artifact.
- `Discussion` sections inside System Design may preserve future architecture and alternatives, but are non-authoritative until explicitly promoted into normative design for a current scope.

See [`references/game-development.md`](references/game-development.md).

## Shared principles

Both workflows keep the same core constraints:

- implementation is evidence, not upstream authority;
- repair contradictions at the earliest wrong authoritative layer;
- do not backfill Specs for untouched legacy code;
- System Design is created only when material technical structure needs durable authority, or when an existing boundary is explicitly revalidated as a baseline;
- Spec does not invent scope or architecture;
- Task decomposes work but does not design it;
- preserve unaffected artifacts and behavior;
- prefer the smallest durable solution and avoid speculative abstractions.
