---
name: project-bootstrap
description: Establish or repair a native iOS/Android project's development setup, environment boundaries and first verified journeys before feature work scales up.
license: CC0-1.0
---

# Bootstrap a project agents can actually work in

Use when starting a native project or making an existing one reliably buildable,
testable and reviewable. For an ordinary feature or broken test, use the existing
setup rather than reopening these decisions. The outcome is a working first
journey and a reusable recipe, not a scaffold with every integration enabled.

## Recover decisions before creating infrastructure

On an existing project, inspect the actual app targets, schemes/flavors, backend
configuration, test entrypoints and accepted product decisions. Distinguish
working, partially implemented and planned setup. A README command or a named
staging scheme is a hypothesis until its destination and behavior are checked.

Resolve the decisions that change foundations before provisioning their
dependencies:

| Decision | Why it affects setup |
|---|---|
| First useful result and purchase boundary | Determines which journey must work without a purchase and which fixtures need paid access |
| One-time unlock, subscription or consumable | Changes catalog shape, ownership and recovery tests; a subscription trial is not a generic free-use timer |
| Guest use and first required login | Determines local persistence, migration/linking and the first recoverable account boundary |
| Who owns paid access | Determines how app identity, purchase restoration and account switching interact |
| Trial start, eligibility and expiry | Determines distinct personas and what state a reset must preserve |

Recover facts from the project; ask the owner only about unresolved product
choices, explaining the setup consequence. An accepted choice stays authoritative.
For example, local draft creation can proceed while export pricing is undecided;
a paid-access ownership model cannot be silently invented to unblock a verifier.
Use `product-decisions` if available for the detailed comparison.

## Make the environment boundaries explicit

Create or update one compact setup map in the project's existing documentation
when documentation is in scope. Otherwise return it in the handoff. Record the
actual source of each value, not a second manually maintained configuration:

- iOS target/scheme/configuration and bundle identity; Android module/variant and
  application identity. Separate development identities are useful for installing
  beside release apps, but require their own applicable provider registrations.
- Backend destination and how the selected build resolves it. Trace aliases and
  runtime overrides as well as checked-in configuration.
- Authentication mode, transaction source and entitlement authority. These are
  independent: a local payment simulation does not authorize a real backend.
- Signing, provider callbacks and device attestation requirements for each real
  integration lane. Keep signing material and debug credentials outside the map.
- Toolchain versions from manifests/lockfiles, maintained build roots, existing
  device aliases and the commands that select focused tests.

Prefer three **proof levels**, not three mandatory cloud projects:

| Level | Configure | Establishes |
|---|---|---|
| Local deterministic | Isolated fixtures, local persistence and mocks/emulators where supported; explicit network behavior | App-owned states, navigation and logic |
| Development integration | Intended non-production app/backend pairing, real auth and relevant service configuration | Real account, authorization and persistence boundaries |
| Provider or candidate qualification | Matching store catalog/tester/signing and the actual artifact required by the claim | Provider behavior or that candidate's integration |

A Firebase emulator setup must explicitly route every exercised service; an
unconfigured service can still reach a live endpoint. Resolve the destination for
each writing app and tool; a seed tool can differ from the app. Stop on a mismatch
before writing. Seed/reset only the environment and fixture scope authorized for
the task, including on shared staging. For fully local Firebase work, prefer a demo
project where supported: it has no live Firebase resources to fall through to.
Keep the app and emulator project IDs consistent for cross-service tests. See
[Firebase's emulator connection guidance](https://firebase.google.com/docs/emulator-suite/connect_rtdb).
Missing development configuration should stop
that operation rather than fall back to production. Mock auth and disabled sync
are capabilities to implement deliberately, not assumed launch flags.

TestFlight does not select a staging backend. A Play test-track invitation does
not establish license-tester status or free purchases. For provider setup, use
current [Apple sandbox guidance](https://developer.apple.com/documentation/storekit/testing-in-app-purchases-with-sandbox)
and [Play billing test guidance](https://developer.android.com/google/play/billing/test),
and, if installed, `store-purchase-check`.
An unavailable provider account is a named gap; it need not block offline work.

## Establish the smallest repeatable development loop

Reuse the repository's wrappers and pinned toolchain before introducing new
scripts. Discover what they actually select: build-only, unit, service, UI or
device. Do not label a default suite “focused” because its command is short.

For any runner used as evidence, confirm that the intended tests actually ran.
Treat unknown or empty selections as failed evidence even if the command exits
zero. When runner changes are in scope, make those conditions fail explicitly.
Batch compatible selections into one build invocation. Keep
build/install time, app execution time and automation waits separately visible;
otherwise a faster runner can be mistaken for a faster app.

Keep these capabilities separable so a small change remains cheap:

- Pure state tests without installing the app or starting a device.
- Service checks with isolated fixtures, including an allowed operation and its
  denied counterpart. Admin SDK success does not prove client access rules.
- A rendered journey on a reusable named test device with bounded waits and
  stable accessibility identifiers. Success is the expected screen, not merely
  a successful tap or launch command.

Use repository-relative paths in reusable recipes and private local overrides
for machine-specific destinations. Reuse maintained build/device resources;
bootstrap is not a reason to duplicate caches or install every available plugin.

## Prepare identity and payment fixtures deliberately

Choose a supported login route that serves the product and can be exercised
reliably. Email/password can simplify cross-platform review and automation, but
adds verification, reset, abuse protection and support work. A supported social
or passwordless route can be appropriate; prove the reviewer can complete it.
Do not add password login solely because an automation tool struggles with an
existing route. Use `identity-and-review-access` for the tradeoffs if available.

Keep app persona, store tester and device profile distinct. Start with the
personas needed by the first journey: for example, a fresh free user and an
established purchaser for restore. Do not reset the purchaser to obtain a clean
onboarding screenshot or assume reinstalling resets server/store history.

Maintain aliases, intended state and secret references in a private registry.
A sign-in helper should resolve secrets internally and return a safe outcome;
prove its input transport does not persist credential values before supplying
real credentials. A masked console alone is insufficient. Keep required OS
confirmation as an attended step. `test-account-automation` provides the fuller
helper contract when available.

For paid apps, prepare local purchase-state coverage separately from provider
qualification. Identify catalog, launch configuration, tester pairing and backend
verification for the chosen lane. Keep synthetic entitlement authority isolated
from release paths. The first provider journey should eventually cover purchase,
durable fulfillment, actual paid use, relaunch and restore; having a paywall or a
successful store dialog is not that proof. Run only the authorized lane: a setup
request is not permission for real-money purchases or production data resets.

## Give the first screen a design and performance baseline

Apply this section when bootstrap includes UI work or establishing that baseline.
For a request limited to making existing commands repeatable, reuse the existing
UI and report any unperformed design/performance work without expanding scope.

Locate the real token/theme source and its consumers before generating more UI.
If none exists, establish a small set of semantic color, typography, spacing and
component roles for the first journey. Share meaning across platforms while
preserving native navigation and input behavior. Generated theme files need a
known source and regeneration command, not independent manual edits.

Render one representative screen in its empty, populated and relevant error
states. Include the normal keyboard for input flows and a relevant large-text
or dark-appearance check. A headless capture with no keyboard cannot establish
that Save remains reachable during editing. Reuse the resulting components
before designing a second version elsewhere.

Make later performance comparisons possible: name a user-visible start/end
event, such as opening a saved document until it is editable. Record build type,
device, data size and cold/warm state for any initial observation. A simulator
smoke is not a phone performance baseline. If performance work is in scope,
use a repeatable measurement and a decision threshold; otherwise report that
profiling remains unperformed. `native-performance-check` covers that work.

## Finish with one proved journey and explicit gaps

Choose a first slice that exercises real user value, such as create a draft,
save, terminate/reopen and continue editing. Add the real signed-in/backend path
when it is in scope; a mock success cannot stand in for it. Verify recovery or
denial at the boundary the slice actually crosses.

Report each required capability as **configured**, **verified**, **blocked** or
**not performed**, with the command/artifact and its limit. “Configured” means
implemented but not yet demonstrated. “Blocked” names the missing input and which
work it prevents. “Not performed” covers unchecked or out-of-scope work; it makes
no claim about readiness.
Do not report an unrun command as successful setup. For documentation-only
bootstrap work, check structure and references; do not build the apps.

Use [the fictional setup example](references/setup-example.md) when writing an
adopting project's recipe. It illustrates concrete setup choices, acceptance
checks and a handoff without providing a starter app or executable QA tooling.
