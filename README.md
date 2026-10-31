# iOS & Android Agent Skills

Practical skills for the decisions and verification work around native apps:
when to ask for payment, how accounts and purchases fit together, how to make
reviewer access dependable, and how to test without spending every task rebuilding.

Each skill gives a decision method, concrete examples and an expected outcome.
Examples use fictional products and personas. They illustrate approaches and
tradeoffs, not measured results or a universal architecture.

## Start with the problem

| You need to… | Skill | What you should get |
|---|---|---|
| Start a project or repair its development setup | [Project bootstrap](.agents/skills/project-bootstrap/SKILL.md) | Explicit environment boundaries, reusable setup commands and a verified first journey |
| Decide purchase timing, trials and ownership | [Product decisions](.agents/skills/product-decisions/SKILL.md) | A decision record with alternatives, consequences and state transitions |
| Choose login and prepare review access | [Identity and review access](.agents/skills/identity-and-review-access/SKILL.md) | A supported identity strategy and tested reviewer journey |
| Stop retyping test credentials | [Test account automation](.agents/skills/test-account-automation/SKILL.md) | A persona registry/helper contract with checked secret handling |
| Set up or qualify purchase testing | [Store purchase check](.agents/skills/store-purchase-check/SKILL.md) | An explicit lane, account pairing and fulfillment evidence |
| Keep new screens consistent | [Reference-led design](.agents/skills/reference-led-design/SKILL.md) | A screen contract grounded in actual components and references |
| Diagnose slowness or compare performance | [Native performance check](.agents/skills/native-performance-check/SKILL.md) | Comparable measurements and a demonstrated or inconclusive result |
| Choose what to test and what to skip | [Validation planning](.agents/skills/validation-planning/SKILL.md) | The smallest sufficient checks and their proof limits |
| Protect a regression | [Behavior TDD](.agents/skills/behavior-tdd/SKILL.md) | A test that detects the actual failure |
| Locate a layered failure | [Boundary debugging](.agents/skills/boundary-debugging/SKILL.md) | A discriminating observation rather than another blind retry |
| Change backend contracts | [Firebase change](.agents/skills/firebase-change/SKILL.md) | Compatibility, concurrency and deployment-scope evidence |
| Verify a screen or interaction | [Native UI check](.agents/skills/native-ui-check/SKILL.md) | Rendered proof with the relevant keyboard/lifecycle state |
| Make UI evidence easy to review | [Visual review evidence](.agents/skills/visual-review-evidence/SKILL.md) | Faithful before/after images, sheets or recordings |
| Audit a product or candidate | [Native Firebase audit](.agents/skills/native-firebase-audit/SKILL.md) | Prioritized findings and a bounded coverage ledger |

## Example requests

- “Bootstrap this native project around a first create/save/reopen journey.
  Inspect what already works, separate local and real-service setup, and identify
  product decisions that block account or purchase configuration.”
- “Before implementing the paywall, compare asking for payment at onboarding,
  first export and a usage limit. Inspect existing decisions first; ask me only
  about unresolved product choices.”
- “Set up a purchase-test plan with fast local state checks and one provider
  qualification path. Keep app login, store account and backend separate.”
- “Design a helper that signs in a test persona without exposing its password
  to the agent or recording it in tool history.”
- “Measure why opening this screen feels slow. Separate app latency from build,
  runner startup and time between automation steps.”

## Use in another project

```text
README.md
AGENTS.md
LICENSE
.agents/skills/<name>/SKILL.md
.agents/skills/<name>/references/   # only where useful
```

Copy the selected skill folder, including its references, to your agent's
supported skill location. `.agents/skills/` is this collection's canonical home;
use your agent's documented discovery mechanism or a symlink where appropriate.
Merge relevant `AGENTS.md` guidance into your project's agreement. Individual
skills work without installing the others; optional cross-references help you
continue when the task crosses boundaries.

These are instructions and examples, not a runnable app or a bundled QA CLI.
Adapt example interfaces to your existing tools. Private account registries,
credentials, actual app identifiers and test artifacts belong in the adopting
project's private environment. Read current linked platform documentation before
live store configuration or submission.

## Complementary skills

[Matt Pocock's skills](https://github.com/mattpocock/skills) are useful companions:
[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)
for exploring decisions,
[TDD](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd)
for behavioral testing, and
[codebase design](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)
for module interfaces. This collection focuses on native product, account, store
and verification decisions. It links to those skills without bundling their text
or adopting their workflow requirements. External skills retain their own terms.

Free to use, copy, modify and share, including commercially, without attribution
or permission. Original material in this collection is dedicated to the public
domain under [CC0 1.0](LICENSE).
