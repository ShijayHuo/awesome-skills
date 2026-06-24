# Refactoring

Refactoring rules for code-implement, exercising the **Embedded Clean Code Core** (`CONTEXT.md`): the small set of readability and restraint rules kept inline in a Self-Contained Orchestrator Skill. Covers both the test-protected case and the no-test case — code-implement does not always have tests, so the discipline adapts.

## 1. Refactoring Prerequisites

- **If tests exist** → run them; they are your safety net.
- **If no tests** → manually verify the key behavior is unchanged, and keep the refactor scope smaller than you would with tests. No safety net means smaller steps.

## 2. Scope Discipline

Refactor only code directly touched by the current change. Do not perform broad cleanup unrelated to the change. "I was already in this file" is not a justification.

## 3. Allowed Refactors

- Renaming (variables, functions, types)
- Extracting or inlining functions
- Removing duplication that actively makes the current change harder to understand or modify
- Deepening modules — moving complexity behind a simple interface, within the current change

## 4. Forbidden Refactors

- Changing data flow
- Cross-layer abstraction adjustments
- Introducing new abstractions "because they look cleaner"
- Any refactor whose real motivation is imagined future reuse

## 5. Pace

- Each step small and continuous.
- With tests → run tests after each step.
- Without tests → manually verify after each step.
- Stop and re-verify the moment a step feels non-trivial.

## 6. Never

- Add new features while refactoring.
- Refactor while RED (if you entered the test-first sub-loop from [tdd.md](tdd.md)).
