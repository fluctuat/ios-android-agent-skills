---
name: store-purchase-check
description: Qualify Apple or Google Play purchases without confusing mocked, sandbox and release evidence.
license: CC0-1.0
---

# Store purchase checks

- Resolve app identity, install/signing channel, backend environment, transaction
  source, app account, store tester and OS profile independently. TestFlight or
  a Play test track does not select a staging backend.
- Local StoreKit proves simulated behavior, not Apple-signed acceptance. Verify
  the intended StoreKit configuration is actually attached to the launched app.
  Use provider-signed test transactions for verification-integration claims.
- For Play, track membership, license testing and the selected device account
  are separate. Confirm the native test-payment context before confirmation.
- First purchase, reopen and restore are distinct checks. Restore cannot replace
  a first-buy test; sheet dismissal does not prove fulfillment.
- Follow the transaction through server acceptance and usable entitlement to
  reopen/recovery. Record which boundary succeeded rather than one broad pass.
- Account history is test input. Reusing a tester can invalidate a fresh-user
  claim. Inspect transaction/server state after an ambiguous timeout before
  attempting another purchase.
