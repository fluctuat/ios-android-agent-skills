---
name: native-firebase-audit
description: Audit native and Firebase release claims for gaps between source, runtime and distribution evidence.
license: CC0-1.0
---

# Native and Firebase audit

Focus on claims that routinely survive a superficial review:

- A native screen may still call a stub even when it resembles the other
  platform. Trace the actual service and durable effect before calling parity.
- Successful authentication may stop before account setup or the stable expected
  landing screen. Test cancellation and restoration when they affect that path.
- Late callbacks after an account switch and stale-client writes can invalidate
  an otherwise successful single-account flow. Include them where state is shared.
- An empty or failed fetch must not be mistaken for authoritative empty data.
  Inspect whether recovery overwrites durable state or triggers fresh setup.
- String limits measured as characters, grapheme clusters, UTF-16 units and
  bytes can disagree across native clients and server validation.
- A completed download is distinct from partial readiness. Verify offline
  reopen rather than relying only on a success marker or cached screen.
- Release configuration can differ from debug source. Inspect the candidate's
  packaged inputs for claims about signing, flags or service selection.
- Upload acceptance, tester availability, review submission, approval and public
  visibility are different distribution states; use the relevant readback.
- Store policy findings need the current official rule and applicable exception.
  Optional UX preferences and inaccessible evidence are not confirmed defects.
- Provider request flags do not establish contractual retention guarantees.
  Match the actual data sent and project eligibility to the promised policy.
- Budget alerts are not enforced spending caps. When enforcing a spending
  ceiling, account for concurrent requests, retries and uncertain billing
  outcomes before admitting more work; successful-response totals alone can
  undercount spend.
