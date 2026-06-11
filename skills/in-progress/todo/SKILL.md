---
name: todo
description: Manage deferred follow-up work through a single /todo entrypoint backed by the repository's root TODO.md. Use when the user wants to record something for later, review existing TODOs, continue the current item, promote it to an issue, or close it.
argument-hint: "Optional: leave blank to auto-detect, or say what you want: add a task, review TODOs, continue this item, promote it to an issue, or close it"
metadata:
  short-description: Single-entry TODO workflow
---

<what-to-do>

Treat `/todo` as a single entrypoint for working with deferred follow-up items in the repository's root `TODO.md`.

Infer the user's intent from the slash-command arguments, current file, cursor context, and recent conversation before asking questions.

Internally support these modes:

- `capture` — add a new deferred item
- `review` — inspect current `Open` items and suggest what to do next
- `resume` — continue or re-scope the current item
- `promote` — move a mature item into an issue, plan, or other formal tracker
- `close` — mark an item as `done` or `dropped`

Use natural-language intent in any language. Reply in the user's language. If no language is clear, default to English.

When the user leaves `/todo` blank, auto-detect the mode:

1. If the current discussion just surfaced a deferred-but-relevant task, prefer `capture`.
2. If the user is focused on a specific entry in `TODO.md`, prefer `resume`, `promote`, or `close` based on context.
3. If the user is looking at `TODO.md` without a specific item, prefer `review`.

If the intent is still unclear, do not guess. Show a short numbered menu in the user's language:

1. Add a new follow-up task
2. Review current TODOs
3. Continue the current item
4. Promote the current item to an issue
5. Close the current item

Allow the user to reply with either a number or natural language.

For `capture`, draft the todo item from the current conversation context first. If useful, inspect the codebase or docs to sharpen the wording.

Before writing anything, show the drafted task to the user and ask for confirmation or correction. Only update `TODO.md` after the user confirms.

Use the format in [TODO-FORMAT.md](./TODO-FORMAT.md).

If `TODO.md` does not exist, create it lazily when the first task is confirmed.

If `TODO.md` already exists, preserve its structure, merge obvious duplicates, and place the task under the most suitable theme or context heading.

Support lightweight maintenance only: add tasks, refine wording, regroup items, move items between `Open` and `Closed`, and mark items as `done` or `dropped`.

Do not let `TODO.md` become a second issue tracker. If a task already has a clear scope, acceptance criteria, and implementation boundary, recommend [../../to-issues/SKILL.md](../../to-issues/SKILL.md) instead of keeping it here.

</what-to-do>

<supporting-info>

## Positioning

Use this skill for work that is relevant enough to preserve, but not mature enough or urgent enough to interrupt the current thread.

This skill is a lightweight backlog workflow, not a project-management system.

Prefer [../../to-issues/SKILL.md](../../to-issues/SKILL.md) for ready-to-implement work.

Prefer [../../handoff/SKILL.md](../../handoff/SKILL.md) for session transfer context rather than durable backlog items.

## File location

The durable backlog file is always the repository root `TODO.md`.

Even in multi-context repositories, keep a single root file and group entries inside it by theme or context when needed.

## Entry rules

Each task must include:

- `Title`
- `Why deferred`
- `Relation to current work`
- `Next step when resumed`
- `Status`

Only add extra fields when they are already known and genuinely useful.

## Lifecycle rules

Keep the file split into `Open` and `Closed`.

Use `open` for active backlog items.

Use `done` or `dropped` for closed items. Add a short closure note when it would help future readers avoid reopening the same discussion.

## Confirmation flow

1. Draft the task from the current context.
2. Ask the user to confirm or correct the draft.
3. Write or update `TODO.md` only after confirmation.

</supporting-info>
