# <PROJECT> wave plan

## Product Vision & Scope

- User and intended outcome — <USER_AND_OUTCOME>
- Core workflow — <STARTING_POINT_TO_SUCCESS>
- In scope — <DELIVERABLES>
- Out of scope — <EXCLUSIONS>
- Latest user acceptance correction — <CORRECTION_OR_NONE>

## Architecture & Boundaries

- Workspace and baseline — <ROOT_AND_REVISION>
- Entry points and responsibilities — <COMPONENTS_AND_ENTRY_POINTS>
- Shared state and side effects — <DATA_AND_SIDE_EFFECTS>
- Protected paths, sessions, and project credentials — <BOUNDARIES>
- Authorized release, spending, and launch actions — <AUTHORIZATIONS_OR_NONE>

## Wave Breakdown

### Wave <N> · <OUTCOME>

- Start condition — <PREREQUISITES_AND_CONTRACT_VERSION>
- Integration order — <ORDER>
- Exit condition — <VERIFIED_RESULT>

| Worker and model | Exclusive file/directory ownership | Read-only dependencies | Deliverable and check |
| --- | --- | --- | --- |
| <WORKER_A_AND_MODEL> | <EXACT_PATHS_A> | <READ_PATHS_A> | <OUTPUT_AND_CHECK_A> |
| <WORKER_B_AND_MODEL> | <EXACT_PATHS_B> | <READ_PATHS_B> | <OUTPUT_AND_CHECK_B> |

Repeat for each wave. Check directory overlap, including nested paths.
Assign shared configuration, generated files, and package outputs to one
writer for each wave.

## Cross-Boundary Contracts

| Contract and version | Publishing owner | Consumers | Interface, errors, and compatibility | Evidence and ready condition |
| --- | --- | --- | --- | --- |
| <CONTRACT_VERSION> | <OWNER> | <CONSUMERS> | <INTERFACE_AND_BEHAVIOR> | <REFERENCE_AND_GATE> |

## Verification & Packaging Gates

- Integrated baseline and expected changes — <REVISION_AND_WORKSPACE>
- Build and package command or equivalent — <COMMAND_AND_OUTPUT_PATH>
- Required checks — <CHECKS>
- Real workflow and expected result — <STEPS_AND_OBSERVATIONS>
- Artifact identity — <PATH_AND_REVISION_OR_DIGEST>
- Launch scope and verification method — <AUTHORIZED_LAUNCH_OR_HEADLESS_CHECK>
- Evidence owner and recording location — <WORKER_AND_EVIDENCE>

Build after each completed implementation worker or immediately after a
settled parallel wave. Resolve failed gates before closing the wave.

## Acceptance Checklist

- [ ] Implementation covers <REQUESTED_BEHAVIOR_AND_LATEST_CORRECTION>.
- [ ] Verification confirms <REAL_WORKFLOW_AND_ARTIFACT> with <EVIDENCE>.
- [ ] Launch status records <AUTHORIZED_LAUNCH_AND_OBSERVATION_OR_NOT_REQUESTED>.
- [ ] Remaining blockers and required decisions are recorded in <STATUS_LOCATION>.
