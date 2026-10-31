---
name: identity-and-review-access
description: Choose login methods and prepare repeatable reviewer access for account-based native apps without weakening normal authentication.
license: CC0-1.0
---

# Identity that works for customers, tests and reviewers

Use when planning login, diagnosing repeated account-entry friction, or preparing
store-review access. Treat convenience, account recovery and privacy as separate
tradeoffs. Test credentials must use an intended supported entry path.

## Decide what requires an account

Find the first action that needs cloud ownership, durable recovery or a paid
entitlement. Avoid adding login to an offline preview merely because the backend
uses authentication. Conversely, a guest purchase needs an explicit recovery
and account-linking design; a local receipt flag is not enough.

| Method | Advantage | Operational cost |
|---|---|---|
| Email and password | Stable, cross-platform account; repeatable native automation; credentials can be supplied privately to reviewers | Password reset, verification, abuse protection and support |
| Email link or one-time code | Removes password management from the user's journey | Mailbox access, expiry and link routing can interrupt automation and review |
| Platform/social sign-in | Familiar consent and account selection | Provider state, cancellation, linked identities and OS prompts vary |
| Enterprise SSO | Fits an organization's identity policy | Reviewer/test access must work with the actual tenant policy |
| Guest/local use | Fast value demonstration with little account friction | Recovery and migration become necessary when cloud ownership begins |

For a consumer app already using managed password auth, retaining a visible email
route often makes both cross-platform QA and reviewer access much easier. It is
not a universal requirement. Do not bolt on a second identity system solely for
review when a stable supported route already exists. Email/password does not
by itself satisfy every platform requirement concerning social login.

## Keep identities distinct

An app account, a provider identity, a store purchaser and a device profile are
separate. An email/password account with a familiar email domain is not
necessarily a Google identity. An email alias is not a new store account.

Make account linking explicit. Inspect how provider changes, private relay
addresses, reinstall, sign-out and account deletion affect the app account and
its purchases. Preserve the established owner rather than merging accounts just
to get a test unstuck.

## Prepare one dependable review route

Use a dedicated account with synthetic data, the required normal role and a
stable entitlement where the review contract permits it. Keep it available for
the review window. Document whether access needs a code, an invitation, another
role or hardware. Do not invent an authentication bypass or disable security.
If a normal route needs interactive verification, provide the store's supported
access instructions or resolve the review approach before submission.

Test on the exact candidate where possible:
`fresh launch → chosen sign-in method → setup/consent → stable landing → core feature`.
Also test restoration from a prior session; it is a different path.

Example reviewer instructions, with credentials supplied only in private portal
fields: “Choose Sign in, then Email. Use the supplied account. Open the sample
project and export a preview. The account already has access to the demonstrated
feature.” Specify actual product labels when applying this template. Never put
reviewer credentials in a public README or an ordinary release-notes field.

## Diagnose the boundary before replacing the account

Provider completion → app session → attestation → application access → loaded
state. A successful password check does not prove native landing. Capture a
safe error classification and correlate the failing request to the build and
environment. Do not rotate a working account because a later request failed.

When review repeatedly fails, compare the exact submitted instructions/build and
reviewer-required setup with a fresh native reproduction. Use available customer
sign-in telemetry to determine whether the problem is broader; absence of such
telemetry is a gap, not proof of reviewer error. Fix incorrect instructions or a
broken supported route first. If the only route inherently depends on interactive
provider setup the reviewer cannot complete, propose a supported alternative as
a product change. Before adding email/password, specify existing-account linking,
collision handling, recovery and rollback so customers do not acquire duplicate
accounts or lose paid access.

Deliver a compact identity decision, the tested reviewer path, required private
portal fields and any unresolved access dependency. For reusable secret-backed
sign-in helpers, use `test-account-automation` if available.

## Current platform requirements

Consult [Apple's review guidelines](https://developer.apple.com/app-store/review/guidelines/)
for reviewer access, login services and applicable exceptions, and
[Google's app-access guidance](https://support.google.com/googleplay/android-developer/answer/9859455)
for Play review instructions. These are policy sources, not evidence that a
particular account can reach your app. Recheck them at submission time.
