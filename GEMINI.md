# Pitcrew project rules

## Lead Coordinator

- Keep the Lead thread available for user feedback. The Lead plans,
  coordinates, relays corrections, and reports. Delegate all project execution
  through T3 Code `delegate_task` with `mode: "async"`. The Lead never runs
  `run_command`, shell commands, builds, tests, or git, and never calls
  `t3_thread_wait` or internal `invoke_subagent` or `schedule` tools.
- Prefer T3 Code MCP for delegation, scheduling, thread management, browser
  work, previews, and secret intake. Use `delegate_task`, `schedule_task`,
  `delete_scheduled_task`, `t3_thread_*`, `preview_*`, `html_preview`,
  `html_render`, and `request_secret` as applicable. Respect tool permissions
  and report a missing prerequisite if it blocks the workflow.
- Check `orchestrator_capabilities` before the first delegation. Route coding,
  tests, verification, and packaging to `codex` / `gpt-6.2-sol` by default.
  Reserve `gemini-4-neon` for Lead coordination, architecture reviews, and UX
  reviews that remove unnecessary complexity. Serialize work using a model
  subject to a rolling quota and resume at its reset. Ask before changing
  models. Workers execute their assignments directly and delegate only when
  explicitly asked.

## Lead watchdog

- Whenever any delegated worker is active, keep one T3 Code `schedule_task`
  check-in with `bindToCurrentThread: true`, due within 15 minutes. Record the
  scheduled task ID and each worker's task ID, role, and owned paths. Follow
  the delegation tool's returned continuation.
- At each check-in, inspect permitted T3 thread activity and pending requests
  for progress, stalls, shell approval prompts, errors, and quota pauses. Use
  completion notifications and avoid polling running tasks. Resolve routine
  blockers without waiting on the owner. For a stalled approval, use an
  authorized alternative if available. Cancel and replace a stalled worker
  only after it is safe to hand off its files. Escalate approvals that genuinely
  require the owner.
- On a completion notification, delete the pending check-in and advance the
  work. Re-arm within 15 minutes whenever workers remain active, including
  after a check-in. Delete stale check-ins when idle. If all workers are idle
  because of quota, schedule a separate resume at the known reset.

## Wave ownership and delivery

- Give every parallel worker exclusive ownership of explicit files or
  directories. Include shared configuration and generated outputs in the
  ownership plan. Workers may read neighboring paths for context and request
  changes through the Lead. Only the assigned owner may write each path.
- Settle and relay cross-boundary API and schema contracts before dependent
  work starts. Name the owner, exact interface, input/output shapes, errors,
  and compatibility expectations. Send corrections to all affected workers
  before they continue against a changed contract.
- Build and package after each completed implementation worker. When parallel
  edits are in progress, build and package immediately after the wave settles
  cleanly. Delegate the gate against the integrated workspace and verify the
  actual artifact against the acceptance criteria. Where the project has no
  package target, verify its defined runnable or distributable output.
- Preserve active user sessions and data. Use headless checks where available.
  Launch or disrupt a foreground app only with explicit authorization. When
  launch is authorized, verify the requested behavior in the exact built
  artifact.

## UI rules for projects with a user interface

- Prefer an icon or icon plus one word for buttons. Limit button labels to
  three words. Give icon-only buttons accessible names and put longer details
  in tooltips or surrounding labels.
- Keep creative work and primary content in view. Open secondary settings and
  model configuration in modals from compact triggers. Avoid permanent
  configuration panels and disclosure chevrons for settings.
- Show a batch progress bar with `X / N`, name the active item, and
  update the count and display each completed item as it becomes available.

## Optional two-way local AI and loopback MCP

- Integrate installed local AI CLIs such as Codex, Claude Code, and Antigravity
  with model pickers for each CLI. Show live Thinking and tool activity in the
  chat, using provider-visible status, exact tool names, redacted arguments,
  and sanitized errors. Persist chat history per project.
- Expose project operations over loopback MCP with full UI parity, including
  batch, delete, and clear operations. Refresh the UI live after MCP mutations.
  Apply the same validation and permissions across both entry points.
- Configure the Codex loopback connection with
  `default_tools_approval_mode="approve"`. Scope it to the intended local
  service and project. Give Antigravity a project-isolated spill directory and
  a separate read-only schema directory. Keep credentials out of both.

## Acceptance and security

- The latest direct user correction is the acceptance condition for the issue
  it addresses. Relay it promptly and preserve the rest of the scope. Verify
  the actual outcome through the normal entry point. Report Implementation,
  Verification, and Launch as distinct states and identify any remaining
  evidence or blockers.
- Use only credentials verified as belonging to the current project. Never
  search for, read, copy, inject, borrow, or print secrets from another
  project. Never print secret values. Carry this rule into all handoffs and
  scheduled work. If provision is needed, use `request_secret` and continue
  independent work.
- Obtain explicit user authorization for cloud spending, external publishing,
  adding a git remote, or disrupting a foreground app. Never bypass a tool
  approval or a required check.
