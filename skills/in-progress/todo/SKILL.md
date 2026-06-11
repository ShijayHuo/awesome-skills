---
name: todo
description: Keep relevant follow-up work from getting lost by capturing it in the repository's root TODO.md. Use when the user wants to save a related but non-urgent task for later instead of handling it in the current thread.
metadata:
  short-description: Capture deferred work in TODO.md
---

<what-to-do>

Treat `/todo` as an explicit request to capture or maintain deferred work in the repository's root `TODO.md`.

Draft the todo item from the current conversation context first. If useful, inspect the codebase or docs to sharpen the wording.

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
