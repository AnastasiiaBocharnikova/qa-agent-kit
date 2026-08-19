---
name: qa-agent-kit
description: >-
  Writes automated tests, including TDD. Use whenever adding or changing tests
  in Jest, Cypress, Playwright, JUnit, Pact, RestAssured, Gatling, or Java
  Selenium. Load this skill first; then load only the one stack file it names.
---

# Write tests

Load this skill **every time tests are written**. Under TDD that is every red–green–refactor cycle.

Do not load Cypress, JUnit, deployment, or Selenium files until this file says to. Do not load review or effort skills while writing tests.

Generated tests are not final without human review. Do not commit, push, or mark merge-ready until the operator says so.

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- See [model-selection.md](references/model-selection.md) only if escalating.

## Foundation (stay here)

1. **Lowest layer that can fail for the right reason.** Unit first. Mocked integration next. Live e2e only if a lower layer cannot prove it. Smoke is a short tagged gate, not a copy of regression.
2. **TDD:** failing test at that layer → minimal code → refactor. Do not write production code without a failing test unless the operator said otherwise.
3. **Locators:** shared `data-testid` / testID modules. No new absolute XPath. No `Thread.sleep` / `cy.wait(ms)`.
4. **Data:** seed and delete via API. Screenshot on UI failure; quit WebDriver. No secrets in git.
5. **Tags:** use the repo’s own suite names. fx-ui: Cypress persona folders and Playwright/Cypress `smoke`. fx-bff: JUnit `@Tag`, post-deploy modules. **stx-e2e-tests only:** `@PreApps` (smoke), `@coreTest` (regression), `@PostApps` (prod, non-invasive). Do not copy STX tags into other repos.
6. **One repo, one stack.** Do not add Selenium to a Jest/Cypress app or Cypress to a Java BFF. Do not duplicate the same journey in two e2e tools.

## Where to look (load **one** file)

Match the file you are about to edit, then stop.

| You are writing… | Load only |
|---|---|
| Jest / RTL (`*.test.ts(x)`) | [ui-unit.md](references/ui-unit.md) |
| Cypress (`cypress/`, `CYPRESS_TYPE`) | [cypress.md](references/cypress.md) |
| Playwright (`playwright/`) | [playwright.md](references/playwright.md) |
| JUnit / Mockito / WireMock in `impl` or `app` tests | [backend-unit.md](references/backend-unit.md) |
| Pact (`contract-tests`) | [contract-pact.md](references/contract-pact.md) |
| Post-deploy smoke / regression / load (`deployment-tests`) | [deployment.md](references/deployment.md) |
| Java Selenium / Cucumber | [java-selenium.md](references/java-selenium.md) |
| `local` vs LambdaTest vs CI wiring | [execution-environments.md](references/execution-environments.md) |
| Technique choice (EP, BVA, personas) — optional | [test-design.md](references/test-design.md) |

Unsure which row? Skim [repo-profiles.md](references/repo-profiles.md), then return to this table.

## Not this skill

| Activity | Skill | Model |
|---|---|---|
| Mixed / “QA this ticket” / write-then-review | `qa-orchestrator` | Composer 2.5 Fast |
| PR / “are these tests enough” | `qa-test-review` | Grok 4.6 |
| Ticket estimate only | `qa-effort` | Composer 2.5 Fast |
| Case list, no implementation | `qa-test-design` | Grok 4.6 |
