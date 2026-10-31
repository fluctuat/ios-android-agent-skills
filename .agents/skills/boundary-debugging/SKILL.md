---
name: boundary-debugging
description: Separate UI, identity, backend and provider failures when a symptom has several plausible causes.
license: CC0-1.0
---

# Boundary debugging

- Separate provider sign-in, authenticated session, attestation, application
  authority, data access and final UI state. Success at one boundary does not
  prove the next; a spinner is insufficient reason to change backend policy.
  An App Check rejection alone does not identify the attestation verdict.
- Correlate observations by environment, build, operation ID and time window.
  Nearby timestamps alone do not establish caller identity or customer impact.
- A mutation timeout leaves its outcome unknown. Inspect durable state before
  retrying; repeating the request may repeat the side effect.
- Measure build/install, cold runner startup, replay, network/service and human
  confirmation separately. A cold automation connection can dominate a short
  flow without indicating app latency.
- Keep recovery at the failed boundary. An automation/device startup failure
  does not justify redeploying an already healthy backend or resetting accounts.
