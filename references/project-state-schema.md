# Project State Schema

Use this reference whenever the project needs a durable status object that both a nontechnical PM and a future web control panel can understand.

Treat this schema as the canonical source of truth after intake. Markdown boards, chat summaries, and control-panel views should be derived from it.

## Design goals

- show the full task tree, not only the current short TODO list
- show the current phase, current step, blockers, outputs, and next action
- preserve stable project state across multi-turn conversations
- support both PM-readable summaries and frontend parsing
- keep the first version simple enough for consistent maintenance

## Canonical bundle

Use this top-level structure:

```json
{
  "project": {},
  "phases": [],
  "steps": [],
  "artifacts": [],
  "decisions": []
}
```

Minimum first version:

- `project`
- `phases`
- `steps`

Strongly recommended:

- `artifacts`
- `decisions`

## Project fields

Required:

| Field | Type | Notes |
|---|---|---|
| id | string | Stable unique project id |
| title | string | Project name |
| summary | string | One-sentence project summary |
| project_type | enum | See `project_type` |
| current_phase_id | string | Current phase id |
| current_step_id | string | Current active step id if known |
| overall_status | enum | See shared status enum |
| strategy | enum | `doc_first` or `hybrid` |
| total_phase_count | number | Total phases |
| total_step_count | number | Total steps |
| completed_step_count | number | Completed steps |

Recommended:

| Field | Type | Notes |
|---|---|---|
| owner_role | string | Default `nontechnical_pm` |
| requires_user_attention | boolean | Whether the user must act now |
| next_action_summary | string | What should happen next |
| current_risk_summary | string | Main current risk |
| created_at | string | ISO timestamp |
| updated_at | string | ISO timestamp |

`project_type`:

- `web_app`
- `mobile_app`
- `backend_service`
- `web_plus_backend`
- `app_plus_backend`
- `multi_platform`
- `other`

`strategy`:

- `doc_first`
- `hybrid`

## Phase fields

Required:

| Field | Type | Notes |
|---|---|---|
| id | string | Stable phase id |
| project_id | string | Parent project id |
| order | number | Phase order |
| title | string | Phase name |
| goal | string | Why this phase exists |
| status | enum | Shared status enum |
| outputs | string[] | Concrete outputs already produced |
| requires_user_confirmation | boolean | Whether the user must confirm this phase |
| testable | boolean | Whether this phase already has something testable |
| step_count | number | Steps in this phase |
| completed_step_count | number | Done steps in this phase |

Recommended:

| Field | Type | Notes |
|---|---|---|
| summary | string | Short PM-readable summary |
| notes | string | PM-readable notes |
| user_action | enum | See `user_action` |
| acceptance_hint | string | How the PM can judge success |
| depends_on_phase_ids | string[] | Prior phases |
| started_at | string | ISO timestamp |
| finished_at | string | ISO timestamp |

## Step fields

Required:

| Field | Type | Notes |
|---|---|---|
| id | string | Stable step id |
| phase_id | string | Parent phase id |
| order | number | Order within phase |
| title | string | Step name |
| goal | string | Why this step exists |
| status | enum | Shared status enum |
| output | string[] | Concrete outputs from this step |
| requires_user_confirmation | boolean | Whether the user must confirm or respond |
| testable | boolean | Whether the result can be tested now |
| notes | string | PM-readable note |

Strongly recommended:

| Field | Type | Notes |
|---|---|---|
| depends_on | string[] | Prior steps |
| user_action | enum | What the user should do now |
| acceptance_hint | string | Quick PM verification hint |
| progress_summary | string | Progress summary |
| blockers | string[] | Current blockers |
| related_artifact_ids | string[] | Linked artifacts |
| related_decision_ids | string[] | Linked decisions |
| started_at | string | ISO timestamp |
| finished_at | string | ISO timestamp |

`user_action`:

- `none`
- `confirm_ui`
- `confirm_product_rule`
- `choose_technical_path`
- `run_user_test`
- `provide_bug_feedback`
- `review_output`
- `supply_missing_info`

## Artifact fields

Required:

| Field | Type | Notes |
|---|---|---|
| id | string | Stable artifact id |
| title | string | Artifact name |
| artifact_type | enum | See `artifact_type` |
| location | string | Path, URL, page name, or file location |
| summary | string | Short description |

Recommended:

| Field | Type | Notes |
|---|---|---|
| phase_id | string | Related phase |
| step_id | string | Related step |
| created_at | string | ISO timestamp |
| version | string | Version if relevant |

`artifact_type`:

- `document`
- `web_prototype`
- `source_code`
- `test_script`
- `report`
- `design_spec`
- `architecture_doc`
- `task_board`
- `other`

## Decision fields

Required:

| Field | Type | Notes |
|---|---|---|
| id | string | Stable decision id |
| title | string | Decision label |
| context | string | PM-readable context |
| status | enum | `open`, `waiting_user`, or `resolved` |
| recommended_option_id | string | Recommended option if any |

Recommended:

| Field | Type | Notes |
|---|---|---|
| related_phase_id | string | Related phase |
| related_step_id | string | Related step |
| options | object[] | Available options |
| user_decision | string | Final choice |
| recommendation_reason | string | Why one option is recommended |
| notes | string | Extra context |

## Shared status enum

Use these exact values for `project`, `phase`, and `step`:

- `not_started`
- `in_progress`
- `waiting_user`
- `ready_for_test`
- `blocked`
- `done`

Use these for decisions:

- `open`
- `waiting_user`
- `resolved`

## Status roll-up guidance

Use this precedence when summarizing the current project state:

1. `blocked` when execution cannot continue without removing a blocker
2. `waiting_user` when the next move depends on user confirmation, choice, testing, or missing information
3. `ready_for_test` when a runnable increment is ready for user verification
4. `in_progress` when active work is underway and no blocker or user gate is higher priority
5. `not_started` when work has not begun yet
6. `done` only when the relevant scope is completed

## Semantic rules

Follow these rules so the schema stays consistent:

1. `goal` must explain purpose, not just action.
2. `output` and `outputs` must be concrete, such as file paths, page names, modules, reports, or scripts.
3. `requires_user_confirmation` should only be `true` when the user must explicitly approve, choose, review, test, or provide missing information.
4. `testable` should only be `true` when a core flow or functional change is complete and the current build is runnable.
5. `notes`, `summary`, and `progress_summary` must use plain product language that a nontechnical PM can understand.

## Continuity rules

Maintain continuity across conversations:

1. initialize at least `project` and early `phases` during intake
2. expand to a full step-level tree no later than master task board generation
3. never renumber existing ids after they have been shared
4. do not remove completed items; keep them and mark them `done`
5. when scope grows, append new ids and recalculate counts
6. keep `current_phase_id` and `current_step_id` pointing to existing records
7. sort `phases` by `order` and `steps` by phase plus `order`
8. update step counts, `requires_user_attention`, `next_action_summary`, and `updated_at` whenever the active position changes
9. derive markdown status boards and daily summaries from this canonical object

## Suggested id patterns

- `proj-001`
- `phase-03`
- `step-03-02`
- `artifact-001`
- `decision-001`

## Example

```json
{
  "project": {
    "id": "proj-001",
    "title": "Class evidence notes app",
    "summary": "Help students capture classroom evidence and turn it into reusable study assets",
    "project_type": "app_plus_backend",
    "current_phase_id": "phase-03",
    "current_step_id": "step-03-02",
    "overall_status": "waiting_user",
    "strategy": "hybrid",
    "total_phase_count": 6,
    "total_step_count": 24,
    "completed_step_count": 9,
    "requires_user_attention": true,
    "next_action_summary": "Confirm whether the homepage and detail-page static prototype look right",
    "current_risk_summary": "Course-mode switching rules are not fully confirmed"
  },
  "phases": [
    {
      "id": "phase-03",
      "project_id": "proj-001",
      "order": 3,
      "title": "Static prototype confirmation",
      "goal": "Use a visual prototype to confirm page structure and the main flow before coding",
      "status": "waiting_user",
      "outputs": [
        "ui_preview.md",
        "web_prototype/index.html",
        "screen_specs.md"
      ],
      "requires_user_confirmation": true,
      "testable": true,
      "step_count": 3,
      "completed_step_count": 2,
      "summary": "Homepage and detail-page prototype are ready for review",
      "notes": "Move into architecture planning only after confirmation",
      "user_action": "confirm_ui",
      "acceptance_hint": "You should be able to open the prototype and judge whether layout, entry points, and navigation match expectations"
    }
  ],
  "steps": [
    {
      "id": "step-03-02",
      "phase_id": "phase-03",
      "order": 2,
      "title": "Create homepage and detail-page static prototype",
      "goal": "Let the user confirm page structure and information hierarchy before implementation",
      "status": "waiting_user",
      "output": [
        "web_prototype/index.html"
      ],
      "requires_user_confirmation": true,
      "testable": true,
      "notes": "The prototype can be opened directly in a browser",
      "depends_on": [
        "step-03-01"
      ],
      "user_action": "confirm_ui",
      "acceptance_hint": "You should be able to move from the homepage to the detail page and confirm that the main flow and layout make sense",
      "progress_summary": "Static pages are complete and waiting for user confirmation",
      "blockers": [],
      "related_artifact_ids": [
        "artifact-001"
      ],
      "related_decision_ids": []
    }
  ],
  "artifacts": [
    {
      "id": "artifact-001",
      "title": "Homepage and detail-page static prototype",
      "artifact_type": "web_prototype",
      "location": "web_prototype/index.html",
      "summary": "Prototype used to confirm UI structure and navigation"
    }
  ],
  "decisions": []
}
```
