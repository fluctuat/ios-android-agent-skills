---
name: firebase-change
description: Change Firebase Functions, Rules and shared contracts while preserving authorization, concurrent state and released-client compatibility.
license: CC0-1.0
---

# Change the service without abandoning installed clients

Use for a backend, Rules or shared-client contract change. A native-only style
change does not need this workflow.

## Define the contract at risk

Trace caller, request/decoder, identity/authorization, transaction or storage
effect, response and visible client state. Identify supported released builds,
not only current main. Freeze compatibility fixtures from those released inputs;
append new fixtures instead of rewriting old ones to hide a server regression.

For example, adding an optional response field may preserve an older decoder;
requiring a new request field can reject every installed old client. Test the
actual old payload and decoder, including omitted and unknown fields.

## Select the failure cases the change creates

- **Authorization:** owner and another account, relevant guest/revoked state,
  client Rules and privileged server path. Admin operations bypass client Rules;
  a green Rules suite does not prove Function authorization.
- **Concurrency:** stale cached value versus new remote value, initial fetch
  racing with an edit, and callbacks completing after an account switch.
- **Retry:** committed operation with a lost response; operation identity scoped
  to actor, destination and input. A reused ID with different input must follow
  an explicit conflict policy rather than return an unrelated result.
- **Deletion:** in-flight work must not recreate deleted state or remove data
  owned by another user.

Choose relevant cases, not a mandatory matrix for every handler. Test durable
results and denial behavior through supported interfaces. Use local emulators
for the contracts they cover before moving to an authorized live lane.

## Plan a compatible intermediate state

Example migration: accept old and new request shapes → verify old-client fixtures
→ distribute clients using the new shape → wait for the agreed support gate →
retire the old shape. Deployment and feature activation may have different gates.
Do not remove a server export because the newest UI no longer calls it.

For shared state, make merge/version behavior explicit. A new device's defaults
are not an authoritative remote snapshot. Test fetch/edit ordering rather than
assuming last-write-wins is harmless.

## Determine the real deployment scope

Follow shared imports, module initialization, generated inputs, dependencies and
runtime configuration. One edited file can affect several Functions; a full deploy
can overwrite unrelated configuration. Different selectively deployed revisions
can be valid, while equal source labels do not prove equal runtime settings.

For an authorized deployment, one owner holds its inputs from preflight through
readback. Record selected targets, intended configuration, rollback and the
compatible client set. After an ambiguous timeout inspect remote state before
retrying. Do not broaden targets because a guarded runner is unavailable.

Return: changed contract, supported-client evidence, local behavior checks,
authorized runtime readback if performed, and any pending activation step.
Source implementation alone is not deployment or client adoption.
