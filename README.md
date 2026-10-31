# iOS & Android Agent Skills

Reusable skills and an `AGENTS.md` for coding agents. The guidance captures
recurring mistakes from native app work.

```text
AGENTS.md
.agents/skills/<name>/SKILL.md
```

One copy of each instruction and skill; no sample app, backend, credentials,
runner or required plugin.

## Use in another project

Copy the skills you need into `.agents/skills/`. Merge relevant instructions
from `AGENTS.md` into your project's existing agreement rather than replacing it.
Use your agent's documented skill location; link to the canonical folders where
supported rather than maintaining duplicate copies.

| Skill | Recurring issue |
|---|---|
| `behavior-tdd` | Tests pass without detecting the defect |
| `boundary-debugging` | A failure is attributed to the wrong layer |
| `firebase-change` | Released clients or selective deployment inputs are missed |
| `native-ui-check` | Builds or headless keyboards stand in for rendered UI |
| `reference-led-design` | Native design is judged from uninspected references |
| `store-purchase-check` | Mock, sandbox and release proof are confused |
| `validation-planning` | Checks repeat without strengthening the claim |
| `visual-review-evidence` | Captures are misleading or hard to review |
| `native-firebase-audit` | Release claims exceed the available evidence |

Free to use, copy, modify and share, including commercially, without attribution
or permission. Dedicated to the public domain under [CC0 1.0](LICENSE).
