# Lead playbook

## Start a wave

1. Read the current scope, acceptance criteria, and prior wave evidence.
   Identify prerequisites and confirm the intended integration workspace.
2. Allocate disjoint write paths, including configuration and generated
   outputs. Record read-only dependencies, checks, and handoff evidence.
3. Check T3 Code capabilities before the first delegation. Start each
   ready worker with `delegate_task` and `mode: "async"`. Include its
   baseline, write scope, acceptance, checks, and project-only credential rule.
4. Record the task IDs and arm one bound `schedule_task`. Use a one-time
   `schedule` with `type: "once"` and a `runAt` timestamp within 15 minutes.
   Set `bindToCurrentThread: true` and record the returned schedule ID.
   Include the active tasks and check-in purpose in the prompt. Follow the
   returned continuation and keep the thread free for feedback.

## Relay contracts and steer workers

1. Assign one owner to publish the API or schema, including its version,
   inputs, outputs, errors, compatibility, and a reference consumers can read.
2. Relay the same contract to all consumers. Let unrelated work continue while
   a dependency is pending. Start the dependent wave when the contract
   and its required implementation evidence are ready.
3. If the user corrects a requirement mid-flight, update the acceptance
   criteria in scope and relay the correction and affected contract version
   through a supported T3 thread operation. If a running worker cannot
   receive it safely, cancel and rebrief that task. Reassign its write scope
   only after cancellation settles. Keep completed work that still applies.

## Run the watchdog

1. Review worker progress, shell approval events, errors, and quota notices
   in `t3_thread_read`. Inspect outstanding questions with
   `t3_pending_request`. Use completion notifications for terminal results.
2. For a stalled shell approval, inspect the reason and identify a permitted
   way to achieve the same check. If a replacement is needed, use
   `task_cancel` and confirm the original worker is terminal before assigning
   its paths again. Have the replacement reconcile partial edits against
   the baseline and preserve valid changes. If the approval is required for
   the task itself, route it to the authorized approver and advance
   independent work.
3. For a rolling quota, record the reset from the provider. Queue work for
   the same model, serialize quota-sensitive assignments, and advance work
   on already-authorized routes. Schedule a bound resume at the known reset
   if quota leaves no active workers. If no reset is known, report that
   blocker. Keep the configured model unless the owner approves a change.
4. On completion, cancel the outstanding check-in with
   `delete_scheduled_task` and advance the wave. After every check-in,
   re-arm within 15 minutes if any worker is still active. Cancel any
   remaining watchdog when idle.

## Verify and package

1. Reconcile worker outputs and make sure the integrated tree contains the
   requested changes and any approved dependent work. Resolve ownership
   conflicts before packaging.
2. As soon as a worker completes, delegate the build and package gate.
   If parallel writers are still active, start the gate immediately after
   the wave settles. Give the gate worker exclusive output paths.
3. Capture the commands and outcomes, the artifact identity, and evidence
   from the actual workflow. Prefer headless checks while the user is
   working. For an authorized launch, verify the visible result from the
   exact built executable or package.
4. If the gate fails, assign the smallest correction to the owning worker
   and repeat the affected checks and packaging. Close the wave only when
   acceptance evidence is recorded. Report Implementation, Verification,
   and Launch separately.
