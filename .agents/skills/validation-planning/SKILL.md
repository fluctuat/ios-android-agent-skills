---
name: validation-planning
description: Choose the smallest sufficient validation for native, backend or release changes and avoid unnecessary builds, devices and repeated checks.
license: CC0-1.0
---

# Spend test effort where it changes confidence

Use for a cross-area change, release validation or a request to reduce testing
cost. For an obvious small fix, apply the relevant row and proceed; do not create
a planning ceremony.

## Identify the claim and invalidated evidence

Name the changed behavior, affected roles/platforms and the consequence of a
regression. Inspect existing test selection and recent evidence. Reuse a result
only if its source inputs, configuration, fixtures and environment still support
this claim. A new chat does not invalidate a result; changed runtime configuration
can invalidate it even at the same source revision.

| Change | Start here | Escalate when |
|---|---|---|
| Internal docs or copy with no layout/contract effect | Diff, links, metadata where applicable | The copy changes a legal/product contract or layout |
| Pure state transformation | Focused unit behavior test | Persistence or another process participates |
| Layout, loading, focus or navigation | Affected rendered screen/flow | Adaptation, OS behavior or a failure needs another device |
| Auth, permissions, sync or shared schema | Relevant service/emulator contract and affected client boundary | Actual provider, attestation or live configuration is the uncertainty |
| Purchase UI states | Mock/local store state tests | Catalog, verifier, signed transaction or candidate changed |
| Performance | Bounded measurement of the changed interval | Pilot evidence identifies a regression or hardware-specific issue |
| Store candidate | Inspect packaged inputs plus critical candidate smoke | Changed lifecycle/signing inputs invalidate additional proof |

## Decide when not to add or run a test

Before adding one, state the observable invariant, credible failure and missing
coverage. If an existing test already catches that failure at the same boundary,
change or reuse it. Do not add a source-string assertion just because it is easy.
A config-file assertion can be valid when that file itself is the contract.

Examples:

- Rename a README heading: no app build.
- Move a Save button above the keyboard: render with the normal keyboard;
  unrelated billing tests add little confidence.
- Change retry ownership in a service: test response loss and duplicate delivery;
  a happy-path unit test is insufficient.
- Change only a mock fixture label: do not buy a real provider transaction.

## Make the execution cheap

Use existing selectors and batch related tests into one build. Fail on an unknown
selector or zero executed required tests. Reuse named devices, prepared datasets,
valid signed-in sessions and maintained caches. A busy device requires ownership
coordination, not another permanent emulator.

Save a repeatable semantic flow when it will be run again. Batch known actions
with state checkpoints rather than making an agent turn for every tap. Keep
bounded state waits; long fixed sleeps hide both fast paths and real failures.
Track build/install, runner attachment, replay and human time separately.

## Stop based on evidence

After affected checks pass, expand for a new change, relevant failure, explicit
wider request or unresolved claim. Do not rerun a successful backend deployment
to recover a device connection. If a required lane is unavailable, finish useful
independent checks and state the precise missing proof.

Return a small ledger, not a test-count trophy:

```text
claim | selected check | revision/environment | result | limit
keyboard leaves Save usable | rendered editor with ordinary IME | ... | ... | ...
retry grants once | service response-loss test | ... | ... | ...
```

Include passed, failed and unavailable checks. “Built”, “installed”, “rendered”,
“service verified” and “store accepted” are different results.

Keep credentials and authenticated session material out of saved flows and
shared captures. Use secret references resolved by a checked helper, not literal
passwords embedded in a replay; otherwise leave secure entry manual.
