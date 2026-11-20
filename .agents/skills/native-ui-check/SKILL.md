---
name: native-ui-check
description: Verify native layout, focus, keyboard and navigation changes with semantic interaction and rendered completion states.
license: CC0-1.0
---

# Inspect the journey the customer actually uses

Use when a change affects appearance or interaction. A successful build is useful
preparation, not rendered proof.

## Choose a reproducible starting state

Name the screen, role, fixture, build mode and expected action/result. Use a mock
fixture for app-owned layout; use real integration only when the claim involves
it. Reuse the maintained device and hold its resource ownership during manual
interaction as well as scripted steps.

Select the smallest relevant state set: normal success plus the changed loading,
empty, error, cancellation or partial state. Expand size, appearance and text
scaling only where adaptation or evidence calls for it.

## Use semantic actions and state waits

Prefer stable accessibility IDs or roles. Distinguish an identifier from a visible
label; a tool's `label` lookup does not necessarily match an app's accessibility
identifier. Refresh references after navigation, dialogs and scrolling. Wait for
the expected state with a deadline rather than adding long fixed settling delays.

Save repeatable flows with semantic checkpoints. Screenshots are for appearance
and diagnosis, not a reason to spend an agent turn after every known tap.
If hierarchy inspection itself fails, classify an observation failure before
assuming the tap failed. Sensitive input requires identified controls; leave
secure OS confirmation manual if the tool cannot safely identify or operate it.

## Check the states that fake success

- **Keyboard:** open the ordinary keyboard, enter long text, scroll to the end,
  reach primary actions, dismiss and reopen. A headless keyboard does not prove
  normal IME occlusion or focus behavior.
- **Persistence:** activity recreation, process restart and account restoration
  are different tests. Pick the lifecycle boundary behind the claim.
- **Build mode:** a DEBUG-only keep-awake or seed flag does not prove release
  behavior. Verify the actual launch mechanism and installed configuration.
- **Navigation:** try Back or Close on an untouched editor and after an unsaved
  edit. Check the destination in each case. If the user can cancel a discard,
  verify the typed value survives. After a discard or interrupted save, reopen the record to check what persisted.

Example: for a Save button hidden by the keyboard, reproduce with a long draft,
fix the inset/focus layout, then save and reopen. A screenshot of the empty editor
with its keyboard closed does not cover the defect.

Return selected captures with the source/build and state, observed interactions,
completion state and any unverified boundary. Use `visual-review-evidence` if
available for a larger contact sheet or recording; it is not required for one
clear screenshot. Restore only settings changed by this run and close only owned
sessions. Do not create another device to avoid a busy shared one.

Keep credentials and authenticated session material out of saved flows and
shared captures. Use secret references resolved by a checked helper, not literal
passwords embedded in a replay; otherwise leave secure entry manual.
