---
name: product-decisions
description: Resolve purchase timing, trials, account requirements and entitlement ownership before building or changing a paid native journey.
license: CC0-1.0
---

# Decide the product contract before building

Use this when a feature changes who pays, what they receive or when they must
identify themselves. An existing accepted decision is an input, not an invitation
to redesign the business. For a layout-only change, skip this skill.

## Recover answers before asking questions

Inspect accepted decisions, onboarding, paywalls, product catalog and entitlement
code. Separate **implemented**, **intended** and **undecided** behavior. Do not ask
the owner for facts that the repository already establishes. Do ask about a
material unresolved tradeoff, with a recommendation and its cost. Continue work
that does not depend on that answer; do not invent agreement from silence.

Resolve these dependencies in order:

1. **Value and payer:** What useful result can someone experience first? Is the
   person using the feature also able and authorized to purchase it?
2. **Purchase boundary:** Is payment needed to enter, create, export, collaborate,
   or consume a scarce service? What happens to work already in progress?
3. **Payment model:** Is this a durable one-time unlock, a recurring subscription
   or a consumable allowance? What continuing value justifies renewal? A store
   subscription trial is not a generic trial mechanism for every product type.
4. **Ownership:** Does payment belong to an app account, a device, a team, or a
   sponsored resource? Who keeps access when the purchaser leaves?
5. **Identity timing:** Which action first needs recoverable account ownership?
   Can a guest preview or work locally before that point?
6. **Trial and expiry:** What starts the allowance, what ends it, and what remains
   accessible afterwards? Is cancellation different from expiry?

Use [the decision examples](references/decision-examples.md) when the purchase
boundary or trial model is unresolved. The examples are fictional, not defaults.

## Compare the options that actually fit

| Choice | Useful when | Cost to account for |
|---|---|---|
| Upfront paywall | Value is already understood; serving any user is expensive | Users cannot validate the promise first |
| Pay after a useful free result | The result demonstrates value | Define the free allowance and preserve completed work |
| Pay at export or collaboration | Creation is cheap and sharing is valuable | Disclose the boundary early; avoid trapping hours of work |
| Limited free tier | Ongoing light use has low marginal cost | Quotas, account switching and support need clear rules |
| Time-limited access without auto-renewal | Users need several sessions to evaluate | Users must explicitly return to purchase |
| Store subscription introductory trial | Recurring value needs a real evaluation period | Store eligibility, recurring terms and conversion need careful handling |

A trial is not automatically a better offer. Ask whether the user can reach the
valuable result within it, whether usage creates meaningful cost, and whether the
payer will be present. Do not choose a duration just because competitors use it.
A store trial and an app-managed free allowance have different eligibility and
billing behavior. Use the store's eligibility and localized offer data rather
than inferring eligibility from a newly created app account.

## Resolve the state changes, not just the paywall

Write expected behavior for free, eligible-for-trial, trial-active, paid, pending,
cancelled-but-still-active, expired and verification-unavailable states. Include
an existing customer who signs in on another device. A network failure is not an
expiry event. An account deletion request is not subscription cancellation.

For example, an export subscription may stop new premium exports on expiry while
leaving existing documents editable. That is a proposed policy to approve, not a
universal requirement. Make recovery and data access deliberate.

## Leave a decision that can drive implementation

Update the project's existing decision record. If none exists, present the
compact decision in chat or create one record in the project's established docs
location when durable documentation is in scope; do not invent a documentation
hierarchy. An explicit owner choice is authoritative. When asked to review it,
explain a material downside and an alternative; if the owner retains the choice,
implement within that contract rather than reopening it indefinitely.

Record:

- Chosen purchase boundary, payer and owner; rejected alternative and why.
- Free/trial/paid/expired behavior, including saved work and offline access.
- Account requirement and restore/account-switch behavior.
- One representative journey and the metric that would challenge the choice.
- Unresolved decisions and which implementation work depends on them.

Example success measures: first useful result reached, purchase completion,
paid feature actually used, refund/support contacts, and cost per activated user.
Do not optimize trial starts alone while ignoring successful use and cost.

For login choices continue with `identity-and-review-access` if installed; for
verification evidence use `store-purchase-check`. Neither is required to produce
this decision record. For a deeper general product interview, consider
[Matt Pocock's grilling skill](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling).

For offer eligibility and presentation, consult current
[Apple subscription guidance](https://developer.apple.com/app-store/subscriptions/)
and [Play subscription guidance](https://developer.android.com/google/play/billing/subscriptions).
Treat a store's available offer as input to the product decision, not a reason
to silently change the user's agreed purchase experience.
