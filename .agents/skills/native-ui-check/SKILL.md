---
name: native-ui-check
description: Verify native layout, keyboard and navigation changes on rendered iOS or Android screens.
license: CC0-1.0
---

# Native UI checks

- Compilation cannot verify layout. Inspect the affected rendered screen and
  completion state rather than treating launch or install as UI success.
- A headless test keyboard does not prove ordinary IME layout. For editor or
  sign-in changes, open the normal keyboard and inspect focused fields, bottom
  actions, scrolling and dismissal.
- Refresh semantic references after navigation, dialogs or scrolling. A stale
  accessibility node can address a previous screen; coordinate-only targets
  are unsuitable for passwords or secure confirmation.
- Activity recreation, process restart and account restoration exercise
  different persistence boundaries. Choose the one the change actually claims.
- Debug-only launch flags cannot prove release behavior. Use the relevant build
  configuration when the claim depends on those flags or OS integration.
