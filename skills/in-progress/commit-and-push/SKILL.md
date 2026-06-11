---
name: commit-and-push
description: Safely commit and publish local code changes.
---

# Commit And Push

Commit and publish the intended local changes without sweeping in unrelated work.

## Scope

This skill covers branch creation, staging, commit, push, and optional pull request creation. If no issue or docs exist, do not block the publish flow.

## Context To Gather

Before committing, gather delivery context in this order:

1. Issue
   - Prefer a user-provided issue number or URL.
   - Otherwise, if GitHub context is available, inspect the current branch PR with `gh pr view --json number,title,closingIssuesReferences,url`.
   - If no clear issue is available, continue without one.
2. Docs / specs
   - Prefer user-specified paths first.
   - Otherwise inspect the smallest relevant set of files under `docs/` and `specs/` needed to understand scope.
   - If no relevant docs exist, continue without them.
   - Use docs/specs for factual context only.

## Branch Naming

- If already on a non-default branch and its name clearly matches the work, keep it.
- If on `main`, `master`, or another default branch, create a new branch.
- When creating a new branch, use the authenticated GitHub login as the namespace unless the user explicitly asks for another naming pattern.
- Prefer `{github-login}/#{issue-number}-{feature}` when an issue is known.
- Otherwise prefer `{github-login}/{feature-summary}`.
- Use lowercase kebab-case.
- `huoshijie/#25-agent-outline-events`
- `octocat/import-docx-nested-lists`

## Workflow

1. Inspect scope with `git status -sb` and the relevant diff.
2. If the worktree is mixed, stage only the intended files. Do not default to `git add -A`.
3. Resolve branch strategy using the naming rules above.
   - If this path depends on `gh`, check `gh auth status` before the first `gh` command.
   - If creating a new branch requires the authenticated GitHub login namespace and `gh` is unauthenticated, ask the user to run `gh auth login` and retry this step.
4. Review the staged file list before committing. If scope is ambiguous, ask which files belong in the commit.
5. Run the most relevant checks for the touched area when practical.
6. Write the commit message using the format below.
7. If an issue or docs/specs were found, mention them in the commit body only after verifying that the references are relevant and safe to include.
8. Respect the user's requested publication scope.
   - If the user asked only for a local commit, stop after the commit.
   - Push only when the user explicitly asked to push, publish, ship, or otherwise create/update a remote branch.
   - Create a PR only when the user explicitly asked for one, asked to publish/ship, or confirmed that opening a PR is desired.
9. If a push is required:
   - Prefer `git push -u origin HEAD` or `git push -u origin $(git branch --show-current)` when the branch has no upstream yet.
   - Otherwise use a normal `git push` on the tracked remote.
   - Before pushing, inspect the staged names and diff for accidental secrets. If the repo has an existing secret scan command or hook, run it. Otherwise do a manual check and stop on suspicion.
10. If a PR is required:
   - If this path depends on `gh`, check `gh auth status` before the first `gh` command. If unauthenticated, ask the user to run `gh auth login` and retry this step.
   - Prefer `gh pr view` to detect an existing PR before creating a new one.
   - Prefer a draft PR by default unless the user explicitly asks for a ready-for-review PR.
   - Infer the base branch from the repository default branch unless the user specifies another target.
   - Prefer `gh pr create` / `gh pr view` for PR discovery and creation.
11. Report back branch name, commit hash, validation, publication actions taken, and any linked issue/docs used.

## Commit Format

Use Angular Git Commit Guidelines.

```text
type(scope): subject

<optional body>

Docs: docs/path.md, specs/feature.md
Close #123
```

- Prefer lowercase `type`, `scope`, and `subject`.
- Keep `subject` imperative and behavior-focused.
- Omit `scope` only when there is no clear bounded area.
- Omit optional lines when they do not apply.

Examples:

```text
feat(user): add user login API

Close #45
```

```text
fix(payment): resolve timeout error during checkout
```

## Safety

- Do not rewrite user history unless explicitly requested.
- Do not rename an already-pushed branch without asking.
- Do not read, infer, expose, or stage local credential material or authentication stores. If GitHub authentication is required, ask the user to run `gh auth login` themselves.
