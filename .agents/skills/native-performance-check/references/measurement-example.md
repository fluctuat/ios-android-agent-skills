# Example: a slow “open settings” check

Illustrative measurements, not results from a real product:

| Interval | Baseline | Candidate |
|---|---:|---:|
| Build/install | 42 s | 42 s |
| Cold automation attachment | 18 s | 18 s |
| Agent/tool round trips between actions | 24 s | 4 s |
| App tap-to-ready median | 310 ms | 305 ms |

A saved replay reduced the workflow by about 20 seconds. It did not establish an
app performance improvement: a 5 ms difference may be ordinary noise. Keep
installation, cold attachment, replay and app latency as separate columns.

For the app interval, suppose a trace shows image decoding on the main thread.
Try decoding/resizing away from that path, then collect comparable runs. Verify
image correctness, cancellation and memory as well as timing. Do not claim success
from a shorter server handler duration if the customer still waits just as long.

A compact result record:

```text
scenario: existing document list → settings ready for input
revision_before / revision_after: recorded commit IDs and dirty state
hardware / OS / build mode: recorded locally
fixture: same synthetic dataset and active account role
cache / process / network: stated separately
runs: count, failures, individual values, median and range
trace: selected local artifact with the suspected cost marked
conclusion: improved / unchanged / regressed / inconclusive; what remains unmeasured
```

Use aliases in shareable evidence. Retain detailed private device/account metadata
only where needed for reproducibility. Avoid adding real user content to traces.

For example, if the predeclared meaningful-change band is ±20 ms, an estimated
5 ms improvement with uncertainty spanning a 25 ms regression through a 35 ms
improvement is inconclusive. An interval wholly within ±20 ms supports unchanged
at that chosen practical tolerance. These numbers are illustrative; choose the
threshold and uncertainty method before inspecting the candidate result.
