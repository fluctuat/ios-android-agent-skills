---
name: boundary-debugging
description: Diagnose ambiguous failures across native UI, identity, backend and providers using discriminating checks and matched evidence.
license: CC0-1.0
---

# Find the last successful boundary

Use when repeated retries or competing explanations have not located a failure.
For an obvious local defect, use one focused reproduction instead of a full
incident process.

## Form a testable distinction

Write the observed symptom without naming the cause. Map the actual path:
input → native state → identity/provider → service authorization → durable effect
→ decoded response → stable UI. Use only boundaries present in the project.

| Observation | Plausible explanations | Useful next observation |
|---|---|---|
| Provider chooser closes; app remains blocked | Cancelled login, missing setup, rejected service call | Auth result and first failing request plus landing state |
| App Check rejects | Attestation/configuration boundary failed | Matched app/build/provider configuration; not a guessed verdict |
| Purchase sheet closes; paid feature locked | Cancel, pending payment, verification or delivery failure | Transaction state then authoritative entitlement |
| Test hangs before first action | Cold runner or device lock | Runner attach timing and identified foreground screen |
| Save times out | No commit, committed but response lost, local decode failure | Durable result for the operation before retry |

Pick the cheapest observation that distinguishes the leading explanations. A
hypothesis should predict evidence; avoid collecting logs with no decision they
could change.

## Match evidence before attributing impact

Correlate environment, build, operation/run ID and UTC interval. Time overlap
alone cannot identify a caller or prove customer impact. Test-account activity
is not automatically a production-user incident. Prefer the owning source and
current state over an old handoff summary.

Measure client, network, server/provider and automation intervals separately.
A local import benchmark is not cloud startup time. A warm replay cannot explain
a failed cold runner. Do not change accounts, capacity or security policy based
on a spinner alone.

## Repair the failed boundary

After a mutation timeout, inspect durable state before retrying. Recover a device
connection at the device boundary rather than redeploying healthy services.
Keep temporary instrumentation narrow and avoid private payloads in logs.

Once repairs are authorized, change the proven cause and verify both the failing
case and its nearest credible regression. A UI error message can be improved
without claiming that it fixes the underlying service rejection.

Return: observed failure, last confirmed successful boundary, confirmed cause or
remaining hypotheses, discriminating evidence, correction and bounded proof.
Mark an unavailable runtime check unverified rather than changing the explanation
to fit what tools happened to be available.
