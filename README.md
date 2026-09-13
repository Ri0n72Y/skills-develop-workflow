# SDD Development Workflow Skill

This repository packages `sdd-workflow` under `.agents/sdd-workflow/`.

```text
.agents/
└─ sdd-workflow/
   ├─ SKILL.md
   └─ references/
      ├─ game-dev.md
      └─ software-dev.md
```

`SKILL.md` is the only entry point. It first decides whether the current capability follows the game-development or software-development workflow, then loads the matching reference.

## Game development

Game development is design-led:

```text
Game Idea / Brainstorm
→ Game Design
→ Requirement
→ System Design
→ Spec
→ Task
→ Implementation
```

`Game Design` and `System Design` are human-led, high-frequency working surfaces. `Requirement`, `Spec`, and `Task` are normally Agent-projected downstream artifacts that the user reviews and adjusts.

See `.agents/sdd-workflow/references/game-dev.md`.

## Software development

Software development is normally Requirement-first:

```text
Problem / Product Context
→ Requirement
→ System Design (when applicable)
→ Spec
→ Task
→ Implementation
→ Verification / Evidence
```

Requirement and System Design may be collaboratively refined; Spec and Task remain executable downstream projections.

See `.agents/sdd-workflow/references/software-dev.md`.

Both modes share the same core rules around directional authority, non-authoritative `Discussion`, no speculative architecture, no retrospective Spec backfill for untouched legacy code, and re-projecting only affected downstream artifacts.
