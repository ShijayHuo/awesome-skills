---
name: handover
description: Prepare a handover document for the next session or agent. Use when another agent should continue the work, when the user wants to preserve the current state, or when a converged discussion needs an implementation-ready handoff into coding.
---

# Handover

Treat `/handover` as the unified entrypoint for session transfer.

Write a handover document summarising the current conversation for the next agent. Save it to the temporary directory of the user's OS, not the current workspace.

Keep the repository read-only. Do not modify `TODO.md`, `CONTEXT.md`, ADRs, specs, or any other durable project file while using this skill.

## Workflow

1. Determine the target mode.
2. Gather only the context needed for that mode.
3. Write the handover document.
4. Reply with the saved path, the chosen mode, a short summary, and any prompt the next session can reuse.

## Mode Selection

Respect an explicit user request for `general` or `implementation` mode when the request is clear.

Otherwise, route automatically.

Default to `general` mode.

Switch to `implementation` mode only when all of these are true:

- the next session goal is clear
- the main scope and implementation path are largely settled
- there is no hard blocker
- the obvious next step is code changes, usually with `/code-implement`

Use a conservative threshold. If the conversation is close to implementation but not clearly ready, stay in `general` mode.

Prefer `implementation` mode after `/key-decision-vetting` only when the discussion has actually converged.

## Blockers

Treat these as hard blockers:

- unresolved public interfaces or contracts
- unresolved data shapes or persistence choices
- unresolved ownership or boundary decisions
- any open decision that would materially change the implementation path

Treat these as soft blockers:

- local naming choices
- copy or wording details
- minor sequencing decisions
- low-risk implementation details that do not change the main path

If `implementation` mode was explicitly requested but a hard blocker remains, do not fake an implementation handover. Explain the blocker and direct the user back to the relevant design discussion, usually `/key-decision-vetting`.

## Common Rules

Use the current conversation as the primary source.

If the user passed arguments, treat them as either:

- a narrowed focus for the handover, or
- a mode hint, when the wording clearly asks for `general` or `implementation`

Inspect the codebase or docs only when that helps sharpen names, likely edit targets, boundaries, or test entry points. Keep this inspection lightweight. Do not turn it into a fresh design pass.

Do not duplicate content already captured in PRDs, plans, ADRs, issues, commits, or diffs. Reference those artifacts by path or URL instead.

Redact sensitive information such as keys, passwords, and personal data.

Always separate what is already settled from what remains open.

Unless code or documentation contradicts the current conversation, tell the next agent not to reopen settled decisions.

## General Mode

Use `general` mode for ordinary session transfer and for conversations that are not yet ready to enter coding.

Keep this mode broadly compatible with the existing `/handoff` behavior.

Write these sections:

1. `Next session focus`
2. `Settled context`
3. `Open questions / blockers`
4. `Suggested skills`

If the conversation is close to implementation but did not qualify for `implementation` mode, add a short `Implementation readiness` section that says:

- why this handover stayed in `general` mode
- what is still missing before `implementation` mode would be appropriate

## Implementation Mode

Use `implementation` mode only when the conversation is ready to hand off into coding.

Use the same core structure as `general` mode, then add:

1. `Concrete change list`
2. `Interfaces and boundaries`
3. `Test strategy`
4. `Likely starting point`
5. `Suggested /code-implement prompt`

For `Concrete change list`:

- turn settled decisions into specific implementation actions
- prefer direct verbs such as `add`, `remove`, `rename`, `split`, `move`, `wire`, `test`, and `verify`
- name likely files, modules, or symbols when lightweight repo inspection can identify them

For `Interfaces and boundaries`:

- capture the public contract the next agent must preserve or introduce
- capture persistence, external-service, or cross-process boundaries
- capture the key invariants that must remain true

For `Test strategy`:

- say what should be tested first
- say what can be verified manually
- say what does not need tests yet

For `Likely starting point`:

- suggest the first slice or first file to inspect
- do not expand this into a full implementation plan

For `Suggested /code-implement prompt`:

- tell the next agent to read the handover document first
- name the implementation goal
- call out the highest-risk decision or boundary
- point to any `CONTEXT.md`, ADRs, specs, or issue files that matter

## Output

After saving the document, reply with:

- the saved path
- the selected mode
- a one- or two-sentence summary of what the next agent can start with
- the `Suggested /code-implement prompt` inline when the mode is `implementation`
