# qa-agent-kit

Agent skills for **writing tests** (TDD), plus optional review and QA effort.

Standalone companion package. It does not depend on Dev Doc Harness. Copy `AGENTS.md` (merge if the destination already has one) plus the `.agents/` folder into a product repository.

House rules come from **fx-ui**, **fx-bff**, and **stx-e2e-tests**.

## Progressive disclosure

1. Always load `.agents/skills/qa-agent-kit/SKILL.md` when writing tests (TDD: every cycle). That file is the shared foundation.
2. Load **only one** stack file it names: Jest, Cypress, Playwright, backend unit, Pact, deployment, or Selenium.
3. Do not load review or effort skills while writing tests.

## Other skills

| Request | Skill | Model |
|---|---|---|
| Writing tests / TDD | `qa-agent-kit` | Grok 4.6 |
| Case list only | `qa-test-design` | Grok 4.6 |
| PR review | `qa-test-review` | Grok 4.6 |
| Estimate | `qa-effort` | Composer 2.5 Fast |

## Install

Merge this repo’s `AGENTS.md` into the product `AGENTS.md`, and copy `.agents/skills/qa-agent-kit`, `qa-test-design`, `qa-test-review`, and `qa-effort`.

## Layout

```text
AGENTS.md                            # when to load the root
.agents/skills/qa-agent-kit/SKILL.md # write-tests foundation + index
.agents/skills/qa-agent-kit/references/  # one file per stack
.agents/skills/qa-test-design/
.agents/skills/qa-test-review/
.agents/skills/qa-effort/
docs/qa/<slug>/                      # optional artifacts
```

## License

Use and copy in your own repositories unless a later commit adds a different license.
