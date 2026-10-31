---
name: behavior-tdd
description: Build a focused regression guard through observable behavior when test-first work or replacement of brittle tests is requested.
license: CC0-1.0
---

# Tests that fail for the right reason

Use for requested test-first implementation, a reproducible regression or a
brittle-test replacement. Do not impose TDD on a prose edit or invent a new
production interface solely to make a private method testable.

## Select the boundary that owns the outcome

Find the existing public interface and its observable result. Name the failure
this test should detect, why current coverage misses it and which dependencies
must be real. Routine selection does not require user approval; an unresolved
product contract does.

| Outcome | Useful boundary | Weak substitute |
|---|---|---|
| Saved draft survives reopen | Repository/service plus supported read path | Searching source for a save call |
| Retry creates one durable resource | Service operation with repeated input | A mock recording two invocations |
| Other account cannot read a record | Authenticated service/Rules operation | Hidden button assertion |
| Keyboard leaves submit reachable | Rendered screen with normal keyboard | View-model boolean test |

## Work one behavior at a time

Create a minimal fixture with independently derived expected values. Run the
case and confirm the intended assertion fails; missing dependencies or an import
error are not a reproduction. Implement the correction, rerun the affected case,
and refactor only while preserving the observable contract. Add another case
for a distinct failure mode, not each private branch.

For a duplicate-save regression, send the same operation through the public
service twice and assert one durable item through the supported read interface.
Then test a genuinely different input where the contract says it differs. Do not
calculate the expected answer by calling the same implementation under test.

## Keep doubles honest

Mock unavailable external systems at their real boundary. Validate meaningful
request contents and error behavior. A mock that accepts every request cannot
protect serialization or authorization. Prefer emulator integration for the
service permissions it can actually exercise; keep provider acceptance in its
provider lane. Reading durable state is valid when it is the result under test,
not an excuse to couple every test to private storage structure.

## Replace fragile coverage without losing its purpose

Record old test → protected behavior → replacement → executed command. Read the
replacement and confirm it is selected and not skipped. When justified, briefly
reintroduce the defect in an isolated owned checkout to see the replacement fail,
then restore it. Never mutate another run's shared inputs for this check.

Keep tests of source/config only when the file itself is the contract, such as a
packaged entitlement or immutable compatibility fixture. Label that narrow claim.

Completion: the relevant failure is observed, the corrected behavior passes, and
the evidence names its limits. For broader TDD techniques see
[Matt Pocock's TDD skill](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd).
Use it as optional reading; follow the adopting project's workflow and approval
rules rather than importing an unrelated process wholesale.
