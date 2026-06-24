# Red-Green-Refactor Sub-Loop

Technical rules for the test-first sub-loop invoked from the Planning stage. This is a tool reference, not a philosophy - see Principle 5 of [SKILL.md](SKILL.md) for when to apply it.

## Vertical Slices, Not Horizontal

**DO NOT write all tests first, then all implementation.** That is "horizontal slicing" - treating RED as "write all tests" and GREEN as "write all code."

It produces bad tests:

- Tests written in bulk test _imagined_ behavior, not _actual_ behavior
- You end up testing the _shape_ of things (data structures, signatures) rather than user-facing behavior
- Tests become insensitive to real changes - they pass when behavior breaks, fail when behavior is fine
- You outrun your headlights, committing to test structure before understanding the implementation

**Correct approach**: vertical slices via tracer bullets. One test -> one implementation -> repeat. Each test responds to what you learned from the previous cycle.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED->GREEN: test1->impl1
  RED->GREEN: test2->impl2
  RED->GREEN: test3->impl3
  ...
```

## The Loop

1. **Tracer bullet** - write ONE test that confirms ONE thing about the system:

   ```
   RED:   Write test for first behavior -> test fails
   GREEN: Write minimal code to pass -> test passes
   ```

   This proves the path works end-to-end.

2. **Incremental loop** - for each remaining behavior:

   ```
   RED:   Write next test -> fails
   GREEN: Minimal code to pass -> passes
   ```

Rules:

- One test at a time
- Only enough code to pass the current test
- Don't anticipate future tests
- Keep tests focused on observable behavior

3. **Refactor** - after all tests pass (see [refactoring.md](refactoring.md)).

**Never refactor while RED.** Get to GREEN first.

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
```
