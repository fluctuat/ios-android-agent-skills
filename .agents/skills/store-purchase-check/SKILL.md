---
name: store-purchase-check
description: Design or run a bounded Apple or Play purchase test with explicit environments, paired accounts and complete fulfillment evidence.
license: CC0-1.0
---

# Purchase testing that proves the right thing

Use when establishing billing QA or qualifying checkout, restore or lifecycle
behavior. For paywall spacing, use a rendered mock flow instead.

## Resolve the product contract first

Identify the paid action, purchaser, entitlement owner, trial eligibility,
post-cancellation access and expiry behavior. Recover accepted decisions from
source and product records; use `product-decisions` if available for unresolved
choices. Do not silently change those choices to simplify testing.

Write one row before executing:

```text
candidate | app identity | install/signing channel | backend
transaction source | app persona | store tester alias | device/profile
scenario | starting entitlement/history | expected durable result
```

Values come from the actual build/configuration and private registry. A track
name, “debug” label or email address does not establish the other dimensions.

## Choose one proof lane

| Lane | Use it for | It does not prove |
|---|---|---|
| Mock paywall and entitlement states | Loading, pricing layout, cancellation UI | Store configuration or verification |
| Local StoreKit | Deterministic Apple purchase states and transaction handling | App Store-signed acceptance |
| Isolated staging integration | Account binding, persistence, paid-feature behavior | Real billing when the entitlement is synthetic |
| Provider test purchase | Native checkout and actual verifier integration | Exact released binary unless that binary was installed |
| Exact store-delivered candidate | Candidate's checkout, fulfillment, reopen and restore | Every later renewal/refund transition |

Read [setup recipes](references/setup-recipes.md) when configuring a lane, and
[lifecycle cases](references/lifecycle-cases.md) when selecting scenarios.
These are distinct proofs, not a compulsory ladder for every UI edit.

## Follow the whole transaction

1. Establish the intended starting account and store history. Identify any human
   confirmation before opening checkout.
2. Load the actual product/offer and inspect the native test-payment context.
3. Buy once. Observe pending, cancelled or completed state truthfully.
4. Observe server verification and the entitlement bound to the intended owner.
5. Use the paid feature, then close/reopen and verify durable access.
6. Test restore/query recovery separately where the scenario requires it.

Sheet dismissal is not fulfillment. Restore is not a substitute for a first
purchase. If the store succeeded but fulfillment failed, retain recoverable
transaction state and diagnose delivery; do not ask the user to buy again.
Inspect durable outcome after response loss before retrying. For completion,
finishing or acknowledgement, follow the platform's delivery contract: verify
and durably grant before marking fulfillment complete, and recover interrupted
processing. Include this step in the receipt; do not leave completed purchases
unacknowledged merely because UI automation ended.

This test recipe does not authorize a real-money purchase or customer-account
mutation. If the expected test-payment context is absent, stop before confirming
and resolve the lane. A live customer incident needs its own recovery scope.

## Keep daily work fast

Use stable free/paid/expired fixtures for ordinary feature work. Reuse generated
assets and prepared data. Reserve provider tests for changed billing, signing,
verification, catalog or release inputs and unresolved provider failures.
A bounded candidate smoke is a useful starting point; add lifecycle cases based
on what changed, not an arbitrary promise that one purchase proves all billing.

Do not reset purchase history unless the scenario needs it and that reset is
within scope. Preserve an established purchaser for restore coverage.

## Return a useful receipt

Record source/build, lane, aliases, initial state, transaction outcome,
verification outcome, feature/reopen/restore results and remaining gaps. Retain
only sanitized evidence. A failed or human-blocked confirmation stays unverified;
a source fix or local mock pass cannot close it.

Use current [Apple sandbox documentation](https://developer.apple.com/documentation/storekit/testing-in-app-purchases-with-sandbox)
and [Play billing tests](https://developer.android.com/google/play/billing/test)
for account and distribution requirements. Product configuration and secure
confirmation vary; check them before adapting a recipe.
