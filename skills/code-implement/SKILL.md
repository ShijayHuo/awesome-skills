---
name: code-implement
description: Implement code changes through a direct-by-default workflow with explicit Planning, Implementation, Refactor, and Done stages.  Use when adding a feature, modifying working code, refactoring implementation logic, or carrying a plan into code.
---

# Code Implement

Default to this skill for implementation work. When the Planning stage marks part of the work as test-first, run the red-green-refactor sub-loop inline (see [tdd.md](tdd.md)).

## Positioning

`code-implement` is a **Self-Contained Orchestrator Skill** (see `CONTEXT.md`): it does not hand off to `/tdd` or `/clean-code` at runtime. Instead it inlines the minimal sub-loop rules — the **Embedded TDD Core** and **Embedded Clean Code Core** — and decides internally which branch to take.

- Prefer this skill when the task is to make code changes.
- If the code is broken or the task is to investigate a defect, prefer `/diagnose`.

## Philosophy

### Principle 1: Direct, Honest Implementation

This principle follows the **Implementation-First Priority** order from `CONTEXT.md`: shortest working implementation → reject speculative defensive code → apply the **Embedded Clean Code Core** → apply the **Embedded TDD Core** only when behavior and risk justify tests.

1. Implement the change in the most direct honest way.
2. Reject speculative defensive code and compatibility paths.
3. Apply the embedded Clean Code core to keep the result readable and restrained.
4. Use the embedded TDD core only when behavior and risk justify tests.

### Principle 2: Boundary Validation, Internal Trust

- Start from the nearest existing abstraction instead of building a new one first.
- Prefer straightforward data flow over protective wrappers and speculative extension points.
- Use `try/catch` only to recover, translate an external failure, or add necessary context.
- Do not add compatibility branches, legacy adapters, or fallback values unless the current task explicitly requires supporting more than one live behavior or data shape.

Boundary checklist — guards go here:

- ✅ **External input boundaries**: user input, API request bodies, external service responses
- ✅ **Persistence boundaries**: database reads/writes, file I/O
- ✅ **Cross-process boundaries**: network calls, message queues
- ✅ **Concurrency boundaries**: data shared across threads

Not boundaries — do not re-validate here:

- ❌ Internal function parameters on trusted internal call chains
- ❌ Domain entities constructed only internally

Do not repeat null checks, fallbacks, optional chaining, or validation deep inside trusted internal call chains.

Stay on the default path for work like:

- CRUD and thin handlers
- simple query assembly
- DTO or field mapping
- pass-through orchestration
- small helpers with no independent decision-making

### Principle 3: Reject Defensive Programming

- Boundary validation is good; internal paranoia is not.
- Do not widen types to optional or nullable unless the value is genuinely optional at that boundary.
- Do not add `??`, `||`, empty objects, empty arrays, or fake defaults just to keep the code running when missing data should fail fast.
- Do not preserve old call patterns or dead branches "just in case" unless the task explicitly requires backward compatibility.
- Fail clearly when a trusted invariant is broken instead of silently masking it.

### Principle 4: Clean Code, Proportionate Refactoring

- Use clear, intention-revealing names.
- Keep each function or class focused, but do not split tiny helpers for style alone.
- Remove duplication when it actively makes the current change harder to understand or modify.
- Keep levels of abstraction reasonably aligned inside a block of code.
- Refactor only as much as the current change needs.

Do not:

- chase tiny functions as a goal
- perform broad cleanup unrelated to the current change
- introduce abstractions only because they look cleaner
- treat every helper as needing its own test

### Principle 5: Proportionate Testing, No Ceremony

This is the **Complexity Escalation Rule** from `CONTEXT.md` applied to testing: stay on direct implementation by default, and escalate to the test-first sub-loop only when an explicit signal is hit.

**Default**: implement directly, do not write tests by default. Test-first is an opt-in applied only where it earns its place.

Frontend / backend strategy:

- **Backend** (data persistence, business rules, external I/O, auth, cross-process communication): test-first for complex business logic and branching behavior.
- **Frontend** (UI rendering, interaction, local state): skip tests by default.
- **Frontend complex-logic exception**: form validation rules, state machines, reusable pure-function utilities → test even though they live on the frontend.
- **Shared utility functions**: pure string/formatting helpers → skip; helpers that encode business rules or decisions → test.

Decision rule: **"Is this code making a decision? Would a wrong decision cause real loss?"** Yes → test. No → skip. Frontend/backend is just a fast approximation of this judgment.

Lean on tests when one or more of these are true:

- the change adds or changes branching behavior or business rules
- a bug fix needs a regression guard
- a state change or side effect could silently regress
- an external integration or serialization boundary needs behavioral confidence

Prefer:

- test-first when reproducing a bug or clarifying non-trivial behavior
- broader behavior tests when they naturally cover trivial glue code
- test scope proportional to the amount of real decision-making

Do not:

- write standalone tests for one-line wrappers, trivial mappers, getters, setters, or pure pass-through code
- split code only to make tiny pieces easier to unit-test
- force red-green-refactor on trivial edits with no meaningful behavior
- treat test count or coverage growth as the goal

## Workflow

### 1. Planning

When exploring the codebase, read the project's `CONTEXT.md` (domain glossary) and relevant ADRs so that names and interface vocabulary align with the project's language.

Before writing any code:

- [ ] Read `CONTEXT.md` (domain terms) and relevant ADRs; align naming with the project's language
- [ ] Identify code type: frontend / backend / boundary code
- [ ] Confirm interface changes needed (with user)
- [ ] Decide which parts need test-first, which may get post-hoc tests, which get no tests
- [ ] List implementation steps (not test steps)
- [ ] Get user approval on the plan

Ask: "What should the public interface look like? Which parts carry real decisions and need tests?"

### 2. Direct Implementation

Implement incrementally — one behavior or one part at a time, not the whole feature at once.

- [ ] Start from the nearest existing abstraction; do not build a new one first
- [ ] Implement in the most direct, honest way
- [ ] No speculative defensive code or compatibility paths
- [ ] Guards only at real boundaries (see Principle 2 checklist)
- [ ] No repeated null checks inside trusted internal call chains

If Planning marked part of the work as test-first, run that part through the red-green-refactor sub-loop described in [tdd.md](tdd.md).

### 3. Clean Code Refactor

After behavior is implemented, look for refactor candidates. Detailed rules in [refactoring.md](refactoring.md).

- [ ] If tests exist → run them after each refactor step
- [ ] If no tests → manually verify key behavior is unchanged after each step
- [ ] Refactor only code directly touched by the current change
- [ ] Extract duplication, deepen modules, keep abstractions justified by this change
- [ ] Never add new features while refactoring

### 4. Done Criteria

- [ ] Domain terms and ADRs respected; naming matches project language
- [ ] The chosen path is the lightest one that still fits the real complexity
- [ ] Defensive code exists at boundaries, not everywhere
- [ ] Abstractions are justified by the current change, not imagined future reuse
- [ ] Frontend/backend test decisions executed correctly
- [ ] Refactoring scoped to the current change; behavior verified
- [ ] Tests are proportional to behavior, decision-making, and risk
