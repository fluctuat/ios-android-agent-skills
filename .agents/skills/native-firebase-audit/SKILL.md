---
name: native-firebase-audit
description: Audit native and Firebase journeys for gaps between intended behavior, source, runtime and release evidence.
license: CC0-1.0
---

# Audit vertical journeys, not a collection of green indicators

Use for a substantial product or release audit. An ordinary screen fix needs its
focused check, not this whole review. Audit produces findings; repair work depends
on the user's requested scope.

## Build the smallest useful map

Identify requested revision/dirty changes, intended journeys, supported clients,
roles, backend environments and the release candidate if relevant. Existing
product decisions constrain the audit; optional redesign is not a defect.

For each critical journey follow:
`entry → action → authorization → durable effect → visible result → retry/reopen`.
Select representative failure paths where the contract has meaningful risk.

## Look for false completeness

| Area | Easy claim | Stronger check |
|---|---|---|
| Platform parity | Screens look alike | Same fixture produces the intended service and persisted effects |
| Login | Provider authenticated | Setup/restoration reaches stable expected landing |
| Shared state | One save passed | Late fetch, stale device and account switch preserve the intended owner/state |
| Downloads | Success marker displayed | Required assets reopen without network; partial readiness remains distinct |
| Purchases | Checkout dismissed | Verification, binding, useful paid action and recovery all observed |
| Release | Debug checks passed | Packaged configuration and exact candidate match the claim |
| Distribution | Upload accepted | Correct audience can access the intended build |

Check string limits across characters, graphemes, UTF-16 units and bytes when
clients share a validation contract. Inspect whether failed fetches are treated
as authoritative empty state and can erase or reinitialize data.

## Inspect cost and privacy as implemented contracts

Trace the actual categories of data sent to a provider and their retention
promises. A request flag alone does not establish contractual retention. If a
spending ceiling is promised, account for concurrency, retries and uncertain
billing outcomes before admitting more work. Budget alerts alone do not enforce
that ceiling. Avoid inventing disclosure answers or changing budgets in an audit.

## Turn observations into findings

Each finding needs trigger, user impact, exact source/runtime evidence,
confidence, smallest correction and a check that could detect the failure.
A confirmed source defect can be reported without runtime reproduction; label
that limit. Missing access is an unverified check, not proof of a vulnerability.
Store-policy findings require current official requirements and exception analysis.

Keep a short coverage ledger: verified, issue found, not applicable with reason,
or unverified with the missing observation. Do not turn one unavailable environment
into dozens of speculative defects, or promise readiness because it found none.

For example: “After switching accounts while a fetch is in flight, the prior
account's response can replace the current screen state; callback ownership is
not checked. Add an account-generation fence and a delayed-response test.” Use
actual source evidence when applying this pattern; the example is hypothetical.

Prioritize data loss, access/ownership, charged-without-access and blocked core
journeys over cosmetic differences. End with findings and the smallest remaining
checks in dependency order. Use the relevant focused skills when installed; this
skill does not require installing another collection or running every lane.
