---
name: validation-planning
description: Plan bounded proof for cross-platform changes or release validation without repeating unchanged checks.
license: CC0-1.0
---

# Validation planning

| Claim | Minimum useful evidence |
|---|---|
| Pure state/logic change | Focused observable behavior test |
| Layout, keyboard or navigation | Affected rendered native journey |
| Service authorization or persistence | Relevant service/emulator contract |
| Provider signature, attestation or hardware | Matching signed/provider/device lane |
| Shipped configuration | Exact candidate artifact and relevant readback |

- Reuse evidence only while its source inputs, configuration, fixtures and
  environment still support the claim. A new chat alone does not invalidate it.
- Unknown selectors, zero executed tests and required skipped cases are not
  passing coverage. Check the runner's actual selections and results.
- Batch affected checks into a maintained build. Broaden after they pass only
  for a relevant failure, changed input or unresolved claim.
- For platform parity compare the same role, fixture and persisted effect.
  Matching screen counts or paired screenshots cannot establish service parity.
