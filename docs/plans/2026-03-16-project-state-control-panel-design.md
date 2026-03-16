# Project State Control Panel Design

## Context

The skill already orchestrates complex product delivery for nontechnical PMs, but its task-board guidance is still too loose for a frontend control panel. The next revision needs one durable structure that survives multi-turn conversations and can answer:

- how many total phases and steps exist
- which phase and step are active
- what is blocked
- what has already been produced
- whether the user needs to intervene now

## Approaches considered

### Option 1: markdown-only boards

This is easy for humans to read, but weak for automation. A frontend page would need brittle parsing rules, and the structure could drift between turns.

### Option 2: JSON-only state

This is strongest for machines, but too opaque for nontechnical PMs if the assistant only speaks in raw objects.

### Option 3: canonical JSON plus markdown views

This is the recommended approach. Keep one machine-readable `project_state.json` as the source of truth, then derive `master_task_board.md`, progress summaries, and daily status views from it.

## Chosen design

Adopt a five-entity schema:

- `project`
- `phase`
- `step`
- `artifact`
- `decision`

Require `project`, `phase`, and `step` in the first version. Make `artifact` and `decision` strongly recommended so outputs and open choices remain traceable.

Unify project, phase, and step status enums around:

- `not_started`
- `in_progress`
- `waiting_user`
- `ready_for_test`
- `blocked`
- `done`

Keep user-facing prose PM-readable while the stored enums remain stable.

## Implementation plan

1. Update `SKILL.md` so the skill explicitly maintains canonical project state across turns.
2. Add `references/project-state-schema.md` as the durable field contract and example bundle.
3. Update output templates and daily status guidance to derive from the schema.
4. Regenerate `agents/openai.yaml` so the UI metadata reflects the new control-panel capability.
