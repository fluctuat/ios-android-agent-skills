---
name: native-performance-check
description: Measure and diagnose native startup, interaction, rendering or memory regressions with comparable runs and explicit proof limits.
license: CC0-1.0
---

# Measure the user journey, then locate the cost

Use for a reported slowdown, a performance-sensitive change or a deliberate
performance review. A routine text/layout edit does not require profiling.

## Define the measurement before optimizing

Name the user-visible interval and its start/end markers: launch to usable home,
tap to editor ready, scroll frame delivery, or memory after repeated open/close.
Choose a representative fixture size, device class, build configuration and
network/cache state. A screen merely appearing is different from being usable.

Record cold process, warm process and cached data separately. State whether the
backend is cold or warm too. Install, compilation, test-runner attachment,
semantic lookup and human confirmation are not app response time.

## Pick the instrument for the suspected cost

| Symptom | Start with | Why |
|---|---|---|
| Slow launch or navigation | Timestamped boundary events and a startup trace | Separates initialization, data loading and UI work |
| Scrolling or animation hitch | Frame timing plus a CPU/render trace | Average response time can hide missed frames |
| Increasing memory | Repeated fixed journey, memory graph/allocation evidence | A single high-water reading does not establish a leak |
| Slow remote action | Client interval and correlated service timing | Distinguishes network, cold service, provider and UI delay |
| Slow automated test | Harness startup/replay timing | Prevents optimizing the app for a runner problem |

On iOS use the relevant Xcode/Instruments or XCTest performance facilities; on
Android use Macrobenchmark/Perfetto for whole journeys and focused benchmarks
for isolated computation. For Android startup/frame cases, select
`StartupTimingMetric`/`FrameTimingMetric` and record startup and compilation mode;
a fully compiled pilot is not automatically representative of a fresh install.
Use release-like/profileable settings appropriate to the tool. Debug logging
and instrumentation can change the result.

## Compare like with like

Run a small pilot to establish noise and confirm that markers mean the same
thing on both revisions. Then measure baseline and candidate on the same device,
fixture, build mode and cache/network conditions. Interleave runs when device
heating or service drift could bias a before/after batch. Keep failed runs and
failure rate visible; do not silently discard timeouts.

Before the comparison, declare the metric, direction of improvement, minimum
practically important change, fixed run budget and analysis method. Derive the
budget from pilot variability and the required precision. For a percentile claim,
state the estimator and uncertainty method; if you cannot support its precision,
report descriptive measurements instead of claiming a tail improvement.

Report count, median and spread with raw selected measurements. A five-run pilot
cannot support a credible tail-latency claim. Use four verdicts: **improved** or
**regressed** when the estimated change and its uncertainty clear the chosen
meaningful-change boundary; **unchanged** when they fit within the predeclared
no-meaningful-change band; **inconclusive** when precision or conditions prevent
either conclusion. Lack of statistical evidence is not proof of equivalence.
Simulator timings can guide relative investigation but cannot certify phone
latency, battery or memory. Avoid running indefinitely to obtain a desired result.

## Optimize the proven bottleneck

Examples: repeated decoding on the UI thread, an effect launching duplicate
requests, an oversized image decoded for a thumbnail, or a cold service call.
Choose one intervention, predict which interval should improve, then remeasure
that interval and the full journey. A delayed spinner can remove flicker without
making the operation faster; report the UX change separately.

Use [the worked measurement](references/measurement-example.md) to distinguish
runner savings from app savings. Stop after the requested improvement is supported
and nearby behavior remains correct. Do not add permanent profiling to every test.

Deliver: scenario and markers, baseline/candidate conditions, measurements,
identified cost, change, resulting user-visible effect and remaining limits.
References: [Apple performance tools](https://developer.apple.com/documentation/xcode/improving-your-app-s-performance)
and [Android Macrobenchmark](https://developer.android.com/topic/performance/benchmarking/macrobenchmark-overview).
