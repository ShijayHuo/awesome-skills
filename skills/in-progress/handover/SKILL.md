---
name: handover
description: Prepare a handover document for the next session or agent. Use when another agent should continue the work, when the user wants to preserve the current state, or when a converged discussion needs an implementation-ready handoff into coding.
argument-hint: "What will the next session be used for?"
---

Write a handover document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

Include a "suggested skills" section in the document, which suggests skills that the agent should invoke.

If the next session is likely to implement code, include a short section that lists a practical implementation plan the next agent can directly use to land code. Break it into a few concrete batches or steps, keep it concise, and avoid reopening settled decisions unless the code or docs clearly contradict them.

Do not duplicate content already captured in other artifacts (PRDs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
