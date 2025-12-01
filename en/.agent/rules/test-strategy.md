---
trigger: model_decision
description: Applied when implementing or modifying test code. Rules for creating test perspective tables (equivalence partitioning/boundary values), Given/When/Then format, and coverage targets
---

# Test Strategy Rules

These rules define the testing process that must be followed when implementing or modifying test code. A test task is not considered complete unless all of the following steps are satisfied.

---

## 1. Test Perspective Table (Equivalence Partitioning / Boundary Values)

1. Before starting any test work, you must first present a "test perspectives table" in Markdown format.
2. The table must include at least the following columns: `Case ID`, `Input / Precondition`, `Perspective (Equivalence / Boundary)`, `Expected Result`, `Notes`.
3. Rows must cover normal cases, error cases, and boundary value cases. For boundary values, include at minimum `0 / minimum / maximum / ±1 / empty / NULL`.
   Boundary value candidates (0 / minimum / maximum / ±1 / empty / NULL) that have no meaning in the specification may be omitted with the reason stated in `Notes`.
4. If you notice missing perspectives later, update the table after self-review and add necessary cases.
5. Note that for minor modifications to existing tests (message adjustments, minor expected value corrections, etc.) where no new branches or constraints are added, creating/updating the test perspective table is optional.

### Template Example

| Case ID | Input / Precondition | Perspective (Equivalence / Boundary) | Expected Result                               | Notes |
|--------|----------------------|---------------------------------------|----------------------------------------------|-------|
| TC-N-01 | Valid input A        | Equivalence – normal                 | Processing succeeds and returns expected value | -     |
| TC-A-01 | NULL                 | Boundary – NULL                      | Validation error (required field)            | -     |
| ...     | ...                  | ...                                   | ...                                          | ...   |

---

## 2. Test Code Implementation Policy

1. Implement **all** cases listed in the above table as automated tests.
2. **Always include failure cases equal to or more than normal cases** (validation errors, exceptions, external dependency failures, etc.).
3. Cover the following perspectives in tests:
   - Normal cases (main scenarios)
   - Error cases (validation errors, exception paths)
   - Boundary values (0, minimum, maximum, ±1, empty, NULL)
   - Invalid type/format inputs
   - External dependency failures (API / DB / messaging, etc. when applicable)
   - Exception types and error messages
4. Furthermore, aim for 100% branch coverage and design additional cases yourself as needed.
   100% branch coverage is a target; if not reasonably achievable, at minimum cover branches with high business impact and main error paths.
   If there are uncovered branches, state the reason and impact in `Notes` or the PR body.

---

## 3. Given / When / Then Comments

Each test case must have the following comment format.

```text
// Given: Preconditions
// When:  Operation to execute
// Then:  Expected result/verification
```

Write comments directly above the test code or within steps to keep the scenario traceable for readers.

---

## 4. Exception/Error Verification

1. For cases where exceptions occur, explicitly verify the exception **type** and **message**.
2. For validation error cases, also verify error codes and field information if available.
3. When simulating external dependency failures, use stubs/mocks to verify that expected exceptions/retries/fallbacks are called.

---

## 5. Execution Commands and Coverage

1. At the end of test implementation, always document the **execution command** and **coverage acquisition method** at the end of documentation or PR body.
   - Examples: `npm run test`, `pnpm vitest run --coverage`, `pytest --cov=...`
2. Check branch coverage and statement coverage, aiming for 100% branch coverage (if not reasonably achievable, prioritize branches with high business impact and main error paths).
3. Attach coverage report verification results (screenshots or summaries) where possible.

---

## 6. Operational Notes

1. Test diffs that do not conform to this rule will be rejected in review.
2. Even when there are no external dependencies, **use mocks to simulate failures** for failure cases.
3. When new branches or constraints are added to the test target specification, update the test perspective table and test code simultaneously.
4. If there are cases that are difficult to automate, clearly state the reason and alternative means, and reach agreement with reviewers.
   Alternative means should include at minimum: target functionality and risks, manual verification procedures, expected results, and how to save logs or screenshots.
5. As a rule, PRs containing meaningful changes to production code (feature additions, bug fixes, refactoring that may affect behavior) must always include corresponding automated test additions or updates.
6. If adding/updating tests is reasonably difficult, clearly state the reason and alternative verification procedures (manual test procedures, etc.) in the PR body and reach agreement with reviewers.
7. Even for refactoring not intended to change behavior, verify that the changed areas are sufficiently covered by existing tests, and add tests if insufficient.

---

Follow this rule and always self-check for missing perspectives before designing and implementing tests.
