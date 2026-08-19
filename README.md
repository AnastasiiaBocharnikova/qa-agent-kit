# qa-agent-kit

Agent skills for test design, test-quality review, and QA effort estimation.

Standalone companion package. It does not depend on Dev Doc Harness. Copy `AGENTS.md` (merge if the destination already has one) plus the `.agents/` folder into a product repository.

House rules are taken from existing suites: **fx-ui** (Jest, Cypress, Playwright), **fx-bff** (JUnit, WireMock, Pact, RestAssured smoke, Gatling), **stx-e2e-tests** (Java Selenium Cucumber, local and LambdaTest).

## What it is for

- Design tests for new behavior (techniques, layers, which repo)
- Review PRs against unit / integration / e2e / smoke practice
- Record QA effort when estimating a ticket

The router classifies the open repo first. It does not force Selenium onto a React app or Cypress onto a Java BFF.

## Install

Merge this repo’s `AGENTS.md` into the product `AGENTS.md`, and copy `.agents/skills/qa-agent-kit`, `qa-test-design`, `qa-test-review`, and `qa-effort`.

## Route

Default models (price / quality / speed): Composer 2.5 Fast for the router and `qa-effort`; Grok 4.6 (balanced / medium) for design and review. See `references/model-selection.md`. Do not start QA work on a flagship model.

The router `.agents/skills/qa-agent-kit/SKILL.md` picks **one** skill:

| Request | Skill | Writes |
|---|---|---|
| Cover this with tests | `qa-test-design` | `docs/qa/<slug>/test-cases.md` |
| Are these tests good enough / PR review | `qa-test-review` | `docs/qa/<slug>/test-review.md` |
| How much QA is this | `qa-effort` | `docs/qa/<slug>/qa-estimate.md` |

## Layout

```text
AGENTS.md                            # house rules + route
.agents/skills/qa-agent-kit/         # router, references, templates, roles
.agents/skills/qa-test-design/
.agents/skills/qa-test-review/
.agents/skills/qa-effort/
docs/qa/<slug>/                      # artifacts in the product repo
```

## License

Use and copy in your own repositories unless a later commit adds a different license.
