# Select purchase cases by the changed contract

| Scenario | Initial state | Expected observation |
|---|---|---|
| First buy | Free app owner; known store history | One purchase yields the intended usable entitlement |
| Cancel | Checkout open | Existing work and entitlement remain consistent |
| Pending approval/payment | Payment not completed | No false success; later completion can be recovered |
| Store succeeds, response lost | Transaction exists; delivery uncertain | Retry/recovery does not charge or provision twice |
| Reopen | Fulfilled purchase | Access is reconstructed from the supported authority |
| Restore | Existing purchaser | Same owner regains the correct access without a new charge |
| Renewal | Active subscription | New period updates expiry/allowance according to policy |
| Cancellation | Renewal disabled, period still valid | Current-period access follows the chosen contract |
| Expiry/refund/revocation | Access end or revocation established | App converges to the agreed restricted state |
| Upgrade/downgrade | Existing plan | Correct effective date, capability and displayed offer |
| Account switch | Purchaser A then app account B | No accidental transfer or stale paid UI |
| Trial eligibility | Eligible and previously used store identities | Offer display and purchase match provider eligibility |

For a pricing-layout change, render the relevant offers. For a verification or
subscription-state change, add the affected provider transitions and durable
state checks. For a release candidate, cover the critical purchase/reopen/restore
journey and any invalidated lifecycle evidence.

Store notifications can be duplicated, late or out of order. Select service
contract tests for those mechanics rather than waiting for every live event on
every run. Accelerated sandbox renewal schedules are test behavior, not customer
billing durations. Do not hardcode their timing from an old runbook.
