---
name: key-decision-vetting
description: Focused grilling session that pressure-tests the highest-impact design decisions against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, ADRs) inline. Use when the user wants a finite review of key decisions rather than an exhaustive interrogation of every branch.
metadata:
  short-description: Finite review of key design decisions
---

<what-to-do>

Interview me relentlessly about this plan until we reach a shared understanding. Walk down the important branches of the design tree, resolving dependencies between decisions one-by-one. Focus on the most important questions and disagreements first, and do not try to cover every possible branch. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase or docs, explore them instead.

Stop as soon as you judge that the original goal of the discussion has been met, we have reached a shared understanding, and no important questions remain. At that point, give your conclusion.

If you have asked 30 questions in this session, stop and ask whether I want to continue with another round of grilling before asking any more.

</what-to-do>

<supporting-info>

## Positioning

Prefer this skill over [../grill-with-docs/SKILL.md](../grill-with-docs/SKILL.md) when the user needs a bounded, high-signal review of the most consequential decisions instead of a full traversal of every branch in the design tree.

## Domain awareness

During codebase exploration, also look for existing documentation.

### File structure

Most repos have a single context:

```text
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```text
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

Create files lazily. Only create a `CONTEXT.md` when the first term is resolved. Only create `docs/adr/` when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. Example: "Your glossary defines `cancellation` as X, but you seem to mean Y. Which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. Example: "You're saying `account`. Do you mean Customer or User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent edge cases that force the user to be precise about boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it clearly. Example: "The code cancels whole Orders, but you just said partial cancellation is possible. Which is right?"

### Update `CONTEXT.md` inline

When a term is resolved, update `CONTEXT.md` immediately instead of batching changes for later. Use the format in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

`CONTEXT.md` should remain a glossary. Keep implementation detail, solution shape, and technical trade-offs out of it.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. Hard to reverse: changing course later would be meaningfully expensive
2. Surprising without context: a future reader would reasonably ask "Why did they do it this way?"
3. The result of a real trade-off: genuine alternatives existed and one was chosen for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).

### Do not reopen settled questions lightly

Once a principle is settled, capture it and move on. Reopen it only if new evidence creates a real contradiction with the code, docs, or another decision.

</supporting-info>
