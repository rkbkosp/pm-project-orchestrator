# Output Templates

## Intake artifact

| Field | Content |
|---|---|
| Project name | |
| Input type | idea / existing doc / mixed |
| Inferred project type | |
| Maturity level | rough / partial / mature |
| Recommended starting stage | |
| Missing information | |
| Key risks or ambiguity | |

## Product blueprint

# Product Blueprint

## Product definition
[One sentence]

## Target users
[Who this is for]

## Core scenarios
- Scenario 1
- Scenario 2

## Value proposition
[Why users would use it]

## Primary flow
1. Step 1
2. Step 2
3. Step 3

## MVP scope
- In scope
- In scope

## Non-goals
- Not now
- Not now

## Open questions
- Question
- Question

Use this markdown view as the human-readable companion to the canonical JSON state in `references/project-state-schema.md`.

## Project control panel summary

| Field | Content |
|---|---|
| Project | |
| Current phase | |
| Current step | |
| Overall status | |
| Total phases | |
| Total substeps | |
| Completed substeps | |
| Needs user attention | |
| Next action | |
| Current risk | |

## Master task board

| Phase ID | Step ID | Phase | Substep | Goal | Output | Dependency | Status | User action | Needs user confirmation | Testable after step | Blockers |
|---|---|---|---|---|---|---|---|---|---|---|---|

## Artifact registry

| Artifact ID | Artifact | Type | Location | Related phase | Related step | Summary |
|---|---|---|---|---|---|---|

## Decision log

| Decision ID | Decision | Status | Related phase/step | Recommendation | What the user needs to decide |
|---|---|---|---|---|---|

## Machine-readable state artifact

- Prefer `project_state.json`
- Follow `references/project-state-schema.md`
- Keep `project`, `phases`, and `steps` populated even when `artifacts` or `decisions` are empty

## Build-round scope note

| This round includes | This round excludes | What user can verify after build | User action needed now |
|---|---|---|---|

## User test case

| Test ID | Goal | Preconditions | Actions | Expected result | If it fails, report |
|---|---|---|---|---|---|

## Bug feedback template

| Field | What the user should provide |
|---|---|
| What you did | The exact steps you took |
| What you expected | What should have happened |
| What actually happened | What you saw instead |
| Reproducible? | Always / sometimes / once |
| Visible error text | Exact words if any |
| Evidence | Screenshot, recording, or console output |

## Delivery summary

| Area | Status | Notes |
|---|---|---|
| Source code | | |
| Documentation | | |
| Architecture coverage | | |
| Core flows | | |
| Known issues | | |
| Recommended next iteration | | |
