# Purchase-test setup recipes

Use separate development and release app identities where the project supports
that separation. Development identifiers, backend projects and tester aliases
below are conceptual; discover the adopting project's actual values privately.

## A. Local Apple purchase-state tests

- Put representative product IDs, subscription groups and offers in a local or
  synced StoreKit configuration. Local catalog edits do not publish products.
- Attach the configuration to the test/scheme launch that actually runs the app.
  Installing an app by a different launcher does not establish that attachment.
- Use mock authentication and isolated state for pure UI coverage. If testing
  real staging features with synthetic access, label that authority explicitly
  and keep it isolated from release verification. Do not send locally signed
  receipts to a production verifier and call rejection a store failure.
- Use StoreKit testing controls for deterministic cancellation, interruption and
  lifecycle states. A no-dialog test is local state evidence only.

See [StoreKit configuration setup](https://developer.apple.com/documentation/xcode/setting-up-storekit-testing-in-xcode).

## B. Development-signed Apple sandbox integration

Resolve the development app's own store registration/catalog, signing and real
backend verifier. Disable local StoreKit configuration for the provider test.
Use a dedicated Sandbox Apple Account and the corresponding private app persona.
Follow Apple's current device/account recipe; do not sign out a personal account
as a universal setup step. Verify the transaction source at checkout and at the
server, not from the app's display name.

## C. TestFlight candidate

Test the actual distributed build. Its backend is determined by its compiled and
runtime configuration; TestFlight does not select staging. Apple purchases in
TestFlight use sandbox. Access to explicit sandbox controls and a chosen Sandbox
Apple Account has a separate setup involving Media & Purchases and Developer
settings; follow the current Apple instructions and account for effects on a
personal device. Do not confuse installing via a production Apple Account with
which account is attributed the sandbox transaction.

If the app deliberately uses a production backend for candidate qualification,
that is a live backend test with sandbox store transactions. Record both facts.
Do not weaken transaction verification to make that combination work.

## D. Google Play

Configure the matching package/catalog and a license tester. A test-track invite
and license-tester status are different; being on a test track alone does not
make purchases free. Inspect the selected account in the native purchase dialog
and require the expected test-payment method before confirming a test purchase.

License testers can test matching packages through supported sideload workflows;
use the actual Play-delivered artifact when the claim concerns that candidate.
A separate development package needs its own applicable Play configuration.

Record the Android profile as well as the Google account. A profile's unlocked
storage state is not proof its screen is unlocked or its app is foregrounded.
Do not rotate accounts to recover a stalled automation runner.

## Preflight result

A ready lane has a known app/backend pairing, available product, correct tester,
expected entitlement/history, identified secure-confirmation step and a recovery
path. Missing one is a named setup gap, not permission to switch environments.
