---
name: visual-review-evidence
description: Make reviewable contact sheets, before-and-after captures and short recordings from actual native journeys.
license: CC0-1.0
---

# Evidence a reviewer can compare

Use for multiple changed screens, a visual handoff or an explicit image/video
request. One clear screenshot can be enough for a small change.

## Choose the format for the claim

| Claim | Useful presentation | Missing proof |
|---|---|---|
| Layout changed | Same-state before/after pair | Persistence or server authorization |
| Several screens are consistent | Labeled contact sheet | Interaction between states |
| Keyboard or navigation behaves correctly | Short actual recording | Every accessibility or provider path |
| Design direction is proposed | Labeled concept/reference board | Runtime implementation |

Match fixture, platform, role, appearance and relevant viewport before comparing.
Name intentional differences instead of presenting them as regressions. A new
image should not be compared with an old capture from a different state.

## Keep the evidence faithful

Use synthetic content. Inspect the entire frame for account details, notifications
and background UI. Arrange contact sheets with readable state labels, preserved
aspect ratios and available full-size originals. Avoid cropping out the keyboard,
error, system inset or loading state that matters to the claim.

For video, capture the actual action through its completion. Keep an original
when trimming a review copy and label edits. Accelerated/spliced footage cannot
support latency claims; a frame strip does not establish responsiveness.

Example labels: “Before — editor, keyboard open, long draft” and “After — same
fixture, Save visible”. Include source/build in the accompanying note rather than
obscuring the screen with a large technical overlay.

## Finish with an observation

Return usable images/video and a short verdict: what changed, what was observed,
what still fails, and what these artifacts cannot establish. A file existing is
not proof that its labels are readable or its capture is the right screen.
Keep selected evidence rather than every intermediate image or copied workspace.
Sharing private captures or creating store marketing material is a separate
purpose from a local engineering review.
