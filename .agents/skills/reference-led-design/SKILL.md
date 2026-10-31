---
name: reference-led-design
description: Design or refine native screens using the product’s actual design system, selected references and rendered state coverage.
license: CC0-1.0
---

# Design from a system, not a screenshot

Use for a new screen, substantial redesign or design-system drift. For a small
layout bug, inspect the current component and fix the affected state directly.

## Establish which system governs this surface

Trace the screen to its theme, token source, native primitives and shared
components. A similarly named file elsewhere in the repo may belong to a retired
surface. If theme code is generated, change its source and regenerate rather
than patching output. Record intentional platform differences before calling
one platform wrong.

Inspect a small set of relevant existing screens. Ask for user-selected Apple,
Material or reference-library examples when direction is missing. Study the
actual flow, not a remembered image. If access is unavailable, mark the reference
uninspected and continue with the product's own examples.

## Make a small screen contract

Define primary task, hierarchy, navigation, density, typography, semantic color,
spacing, elevation and component variants. Describe loading, empty, error,
partial, success and disabled states where they matter. Include keyboard/focus,
large text and accessibility behavior rather than reviewing only the ideal image.

| Shared intent | iOS expression | Android expression |
|---|---|---|
| Destructive action | Appropriate native destructive role/menu | Material destructive treatment and native menu behavior |
| Primary action | Existing button style and placement convention | Existing Material button and container convention |
| Content grouping | Product's list/section pattern | Product's card/list pattern |
| Semantic color | Theme role, including appearance variants | Color-scheme role, including appearance variants |

Do not force identical chrome to obtain pixel parity. Share meaning and brand
choices; preserve platform navigation, keyboard, hit targets and system behavior.

## Prove drift before creating another component

A useful finding connects a design decision to its runtime consumer and visible
consequence. Repeated code or different numeric values alone do not prove drift.

Example: two edit screens use the same documented primary-save component, but
one overrides its container color with a literal that fails in dark appearance.
Fix the override or missing semantic token at its owner. Do not introduce a new
“universal button” to fix one screen unless multiple consumers need that contract.

If no existing component expresses the necessary state, propose a bounded variant
with its intended consumers and behavior. Record accepted exceptions so the next
agent does not “fix” them back. Treat optional redesign as a proposal.

## Verify and hand off

Render the changed journey with normal keyboard behavior and relevant appearance
or text-size variants. Use paired captures for visible changes and a short
recording for motion. Label generated concepts separately from runtime evidence.

Return the governing source/component, selected pattern and reason, states
covered, actual captures and any intentional differences. Update the existing
design record only when a reusable decision changed. Keep implementation details
out of the product's user-facing flow.

For platform decisions consult the current [Apple HIG](https://developer.apple.com/design/human-interface-guidelines/)
and [Material guidance](https://m3.material.io/). A reference app's choice is not
a platform requirement. For substantial component-interface questions,
[Matt Pocock's codebase-design skill](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)
is an optional complement, not a dependency.
