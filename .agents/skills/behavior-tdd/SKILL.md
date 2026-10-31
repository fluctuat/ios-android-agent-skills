---
name: behavior-tdd
description: Guard regressions through observable behavior when test-first work or replacement of brittle tests is requested.
license: CC0-1.0
---

# Behavior TDD

- A source-string assertion, copied implementation or mock that accepts every
  payload can pass while the behavior is broken. Assert outcomes through the
  existing public boundary; derive expected values independently.
- A red run caused by imports, tooling or setup does not reproduce the defect.
  Confirm the intended behavioral assertion fails before treating it as a guard.
- Before replacing a brittle test, identify the regression it protected. Keep
  that coverage in the replacement rather than deleting the only guard.
