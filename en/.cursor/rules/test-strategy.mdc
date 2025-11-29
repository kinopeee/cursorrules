---
alwaysApply: true
---

## Test strategy rules

These rules define the test process that **must** be followed whenever you implement or modify test code. A test task is **not** considered complete unless all of the steps below are satisfied.

---

## 1. Test perspective table (equivalence partitioning / boundary values)

1. Before starting any test work, you **must** first present a “test perspectives table” in Markdown table format.
2. The table must include at least the following columns: `Case ID`, `Input / Precondition`, `Perspective (Equivalence / Boundary)`, `Expected Result`, `Notes`.
3. Rows must comprehensively cover normal, abnormal, and boundary cases. For boundary values, you must include `0 / minimum / maximum / ±1 / empty / NULL` at a minimum.
   Among the boundary candidates (0 / minimum / maximum / ±1 / empty / NULL), you may omit those that are not meaningful for the given specification, as long as you record in `Notes` why they are out of scope.
4. If you later discover missing perspectives, update the table after self‑review and add the necessary cases.
5. Note: For minor adjustments to existing tests (such as tweaking messages or slightly updating expectations) that do not introduce new branches or constraints, creating or updating a test perspectives table is optional.

### Template example

| Case ID | Input / Precondition | Perspective (Equivalence / Boundary) | Expected Result                               | Notes |
|--------|----------------------|---------------------------------------|----------------------------------------------|-------|
| TC-N-01 | Valid input A        | Equivalence – normal                 | Processing succeeds and returns expected value | -     |
| TC-A-01 | NULL                 | Boundary – NULL                      | Validation error (required field)            | -     |
| ...     | ...                  | ...                                   | ...                                          | ...   |

---

## 2. Test code implementation policy

1. Implement **all** cases listed in the table above as automated tests.
2. Ensure you include **at least as many failure cases as success cases** (validation errors, exceptions, external dependency failures, etc.).
3. Your tests must cover the following perspectives:
   - Normal paths (main scenarios)
   - Abnormal paths (validation errors, exception paths)
   - Boundary values (0, minimum, maximum, ±1, empty, NULL)
   - Inputs with invalid types or formats
   - Failures of external dependencies (e.g. API / DB / messaging, when applicable)
   - Exception types and error messages
4. Additionally, aim for 100% branch coverage, and design extra cases yourself as needed to achieve it.
   Treat 100% branch coverage as a target. When it is not reasonably achievable, at minimum cover all high‑impact business branches and primary error paths.
   If any branches remain uncovered, explicitly document the reasons and impact in `Notes` or the PR description.

---

## 3. Given / When / Then comments

Each test case must include the following comment format:

```text
// Given: Preconditions
// When:  Operation to execute
// Then:  Expected result / assertions
```

Place these comments directly above the test code or within the steps so that readers can easily follow the scenario.

---

## 4. Exception and error verification

1. For cases where exceptions occur, explicitly verify both the **exception type** and the **message**.
2. For validation‑related abnormal cases, also verify error codes and field information, if available.
3. When simulating failures of external dependencies, use stubs/mocks and confirm that the expected exceptions, retries, and fallbacks are invoked.

---

## 5. Execution commands and coverage

1. At the end of test implementation, always document the **execution command** and **coverage collection method** at the end of the documentation or PR description.
   - Examples: `npm run test`, `pnpm vitest run --coverage`, `pytest --cov=...`
2. Check branch coverage and statement coverage, aiming for 100% branch coverage as a target (when it is not reasonably achievable, prioritize covering high‑impact business branches and primary error paths).
3. Attach coverage report results (screenshots or summaries) where reasonably possible.

---

## 6. Operational notes

1. Any test changes that do not comply with these rules should be sent back during review.
2. Even when there are no external dependencies, you must still include failure cases by **using mocks to simulate failures**.
3. When new branches or constraints are added to the target specification, update both the test perspective table and the test code at the same time.
4. If there are cases that are difficult to automate, clearly document the reasons and alternative measures, and obtain agreement with the reviewer.
   The alternative measures must at least describe the affected functionality and risks, the manual verification steps, the expected results, and how logs or screenshots will be recorded.
5. In principle, any PR that includes a meaningful change to production code (such as new features, bug fixes, or refactors that may affect behavior) must also include corresponding additions or updates to automated tests.
6. If adding or updating tests is reasonably difficult, clearly document the reasons and the alternative verification steps (such as manual test procedures) in the PR description and obtain agreement from the reviewer.
7. Even for refactors that are not intended to change behavior, confirm that the changed areas are sufficiently covered by existing tests, and add tests when coverage is insufficient.

---

Always adhere to these rules and continuously self‑check for missing perspectives when designing and implementing tests.

