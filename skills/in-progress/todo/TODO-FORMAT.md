# TODO.md Format

The durable backlog file lives at the repository root as `TODO.md`.

Create `TODO.md` lazily — only when the first task is confirmed.

## Structure

```md
# TODO

Deferred but still relevant follow-up work that should not interrupt the current thread.

## Open

### {Theme or Context}

#### {Short task title}
- **Status**: open
- **Why deferred**: {Why this should not be done now}
- **Relation to current work**: {What discussion, implementation, or idea caused this task}
- **Next step when resumed**: {The first concrete move to restart this work}

## Closed

### {Theme or Context}

#### {Short task title}
- **Status**: done | dropped
- **Why deferred**: {Original reason it was deferred}
- **Relation to current work**: {What discussion, implementation, or idea caused this task}
- **Next step when resumed**: {Keep the last planned next step, or say "None - closed"}
- **Closure note**: {Why it was completed or intentionally dropped}
```

## Rules

- Keep one root `TODO.md`, even in multi-context repositories.
- Group by theme or context only when it improves scanability. If the list is small, a flat `Open` / `Closed` split is enough.
- Keep titles short and action-oriented.
- Keep each field concise. This file is a durable reminder, not a mini-spec.
- Merge obvious duplicates instead of appending near-identical tasks.
- If a task grows clear enough to define acceptance criteria and implementation boundaries, move it to the issue tracker or a formal plan instead of expanding it here.
