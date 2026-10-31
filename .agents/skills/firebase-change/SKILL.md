---
name: firebase-change
description: Change Firebase Functions, Rules and shared configuration while preserving released clients and deployment scope.
license: CC0-1.0
---

# Firebase changes

- Admin SDK operations bypass client Rules. Rules tests therefore cannot prove
  authorization in a privileged Function; exercise that boundary separately.
- Scope idempotency to actor, destination and input. Reusing an operation ID for
  a different request must not silently return the prior request's result.
- Released clients define a compatibility floor independent of current main.
  Freeze their request/decoder fixtures from the released revision; append new
  fixtures instead of rewriting old ones to make a server change pass.
- Shared imports, initialization, configuration and dependency inputs can affect
  Functions outside the edited handler. Determine deployment scope from those
  dependencies rather than commit labels alone. A full deploy can overwrite
  unrelated runtime configuration; preserve it when selecting affected targets.
- Different selectively deployed Functions can legitimately have different
  source revisions. Compare runtime inputs and configuration before treating
  revision differences as deployment drift.
- Backend deployment, client distribution and feature activation are separate
  events. Order compatible changes so intermediate states support released
  clients; activation may require a later adoption or migration gate.
- A successful deploy does not prove activation or a client's visible result.
  Read back the affected runtime/configuration and verify the changed contract.
