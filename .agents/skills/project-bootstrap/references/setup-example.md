# Example: a drawing app's first usable setup

Everything here is fictional. Names illustrate configuration relationships, not
accounts to create or measured results. Adapt the recipe to the existing project;
do not create this directory layout or these environments merely to match it.

## Decisions that unblock the first slice

Suppose the owner has chosen guest drawing, local save and a paid high-resolution
export. The price and whether access is one-time or recurring remain undecided.

Proceed with create/save/reopen and an export boundary that preserves the draft.
Keep paid states synthetic for UI work. Defer store product registration and
recurring-trial configuration until the payment model is chosen. If login is
required before purchase, explain the extra interruption in the export flow and
resolve account ownership before implementing transaction binding.

The alternative, requiring signup and payment before drawing, simplifies some
ownership paths but prevents users from experiencing the drawing tools first.
That tradeoff belongs to the product decision, not to the bootstrap script.

## One setup map, with source owners

| Concern | Example choice | Where to confirm it |
|---|---|---|
| iOS local launch | `SketchLocal` scheme, `org.example.sketch.dev` | Scheme's build configuration and resolved build settings |
| Android local launch | `localDebug`, `org.example.sketch.dev` | Variant's resolved application ID and service configuration |
| Local data | Isolated draft store and explicit fake service adapter | Actual dependency wiring for these launches |
| Development integration | Separate scheme/variant using the intended staging backend | Resolved client configuration and a safe request observed at that backend |
| Purchase UI | Synthetic states; local StoreKit configuration for Apple where implemented | Test/scheme attachment and transaction source during that launch |
| Provider qualification | Not configured yet | Missing catalog and agreed payment model; no implied purchase permission |
| Design | Semantic `surface`, `onSurface`, `primary`, `error` roles | Owning token source and native runtime consumers |
| Test accounts | Private aliases `fresh-drafter` and later `returning-purchaser` | Private registry's environment, expected state and secret reference |

Use the project's real names in its private recipe. Do not put its environment
map or account registry into the reusable skill collection.

## Turn that map into a working local recipe

1. Read the repository's toolchain pins, wrapper help and available schemes or
   variants. Record the exact existing local build and focused-test invocations.
   If no wrapper exists, use the project's native build tool before adding one;
   a wrapper earns its place by enforcing repeated environment/selector choices.
2. Select the local launch and verify its resolved app identity and service
   adapter. Give its draft store a separate namespace from integration fixtures.
   Remove or deliberately reject missing integration configuration; do not let a
   local launch silently inherit a release backend.
3. Seed a small drawing through the same persistence interface the app reads.
   Verify a real save/reopen assertion in the owning logic tests. An in-memory
   mock that returns the seed unchanged does not test persistence.
4. Run the app on the project's reusable test device. Create and rename a draft
   using the normal keyboard, save, terminate/relaunch without clearing data,
   then reopen and edit. Confirm the draft and name survived. A process restart
   differs from reinstalling or clearing application data.
5. Render the same editor's empty, saved and save-failed states through controlled
   fixtures. Check the primary action while the keyboard is visible. Use the
   real theme roles; keep native controls rather than forcing identical chrome.

The saved recipe should identify its command's purpose and preconditions:

| Operation to record | Preconditions | Acceptance |
|---|---|---|
| Focused draft-store tests | Fixture storage isolated | Actual persistence assertions run; zero selection fails |
| Local app launch | Known device and local configuration | Correct app and data fixture appear |
| Draft journey | Editable fixture, normal keyboard | Create/save/reopen/edit completes within bounded waits |
| Integration sign-in, when enabled | Private persona and verified secret-safe input | Intended backend and stable signed-in landing screen |

Replace the operation names with commands discovered and run in that project.
This example deliberately ships no `qa` executable or purported wrapper command.

## Add real integration only when the first slice needs it

For cloud sync, configure the intended non-production auth and data services,
including actual callback/signing requirements. Confirm that the selected launch
reaches them before creating fixtures. Exercise owner read/write and another
user's denied access using the client identity path, not only an administrator.
Prove sync through a fresh server-backed read under the intended client identity,
such as on a second client without the first client's cache. Relaunch alone can
show cached data and does not prove cloud persistence or synchronization.

When implementing the agreed email/password route, qualify signup, verification,
failed login, password reset and session restoration through the real supported
flow. A successful login alone leaves recovery untested. For local drafts joining
an account, verify the agreed adoption behavior preserves work and does not expose
it after switching accounts. Where offline sync is supported, check reconnect and
the chosen conflict behavior. Include sign-out and account deletion when those
flows are in scope; do not silently add new account features to a local-only task.

For payments, establish the chosen store product and test-account pairing, then
use the provider-specific setup instructions. Keep transaction source and backend
destination as separate fields. Prepare cancellation, pending and restore states
before treating a first purchase as a reusable qualification recipe.

## Example handoff shape

These are illustrative outcomes, not evidence of a run:

- **Verified:** local draft journey on both platforms; include actual build,
  commands, test results and selected rendered evidence in the real handoff.
- **Configured:** development login wired; secret-input transport check still
  pending, so no real credentials have been passed through that helper.
- **Blocked:** store catalog awaits payment-model decision; local editor and
  synthetic paywall work can continue independently.
- **Not performed:** device performance profiling. Future metric: tap a saved
  drawing to editable canvas, measured separately from runner startup.

Maintain this in the existing project setup record or concise handoff. Avoid
creating a new dated report for every successful launch.
