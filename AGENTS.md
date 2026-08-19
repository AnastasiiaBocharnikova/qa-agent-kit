# QA Agent Kit

For test design, test-quality review, or QA effort estimation, use `.agents/skills/qa-agent-kit/SKILL.md` as the router. Load only the skill the router selects.

This kit is standalone. It does not require Dev Doc Harness. Write artifacts under `docs/qa/<ticket-or-slug>/`.

## Route

Do not run all three QA skills on every request. Do not start QA work on a flagship or max-reasoning model.

| Request | Skill | Default model (tier / effort) | Current Cursor mapping |
|---|---|---|---|
| New behavior, cover with tests, ticket planning | `qa-test-design` | balanced / medium | Grok 4.6 |
| PR, diff, “are these tests good enough” | `qa-test-review` | balanced / medium | Grok 4.6 |
| Ticket estimate, plan split, “how much QA” | `qa-effort` | fast/economy / low | Composer 2.5 Fast |
| Classify repo and pick the skill | router `qa-agent-kit` | fast/economy / low | Composer 2.5 Fast |

Escalate a **review** to balanced/high only for auth, money/checkout, leftover data, or LambdaTest-only flake. Use flagship/medium only after balanced missed a high-impact gap. Full table: `.agents/skills/qa-agent-kit/references/model-selection.md`.

## Detect the repo profile first

Inspect the repository before choosing stack or layers. Use the matching profile in `.agents/skills/qa-agent-kit/references/repo-profiles.md`.

| Signals | Profile | Default stacks |
|---|---|---|
| `package.json` with Jest and Cypress and/or Playwright | **ui-frontend** (fx-ui style) | Jest+RTL unit; Cypress integration (API mocked) vs Cypress e2e (live); Playwright and/or Cypress smoke |
| Maven modules `impl` + `deployment-tests` (smoke/regression/load) and/or `contract-tests` | **api-backend** (fx-bff style) | JUnit+Mockito unit; WireMock for HTTP collaborators; Pact contracts; RestAssured smoke/regression **post-deploy**; Gatling load |
| Cucumber `*.feature`, Page Objects, `seleniumserver`, `selenium-core` | **ui-selenium** (stx-e2e style) | Java + Selenium + Cucumber; local / remote / LambdaTest |

Do not force Java+Selenium onto a React UI repo, or Cypress onto a Java BFF. Follow the repo that is open.

## House rules (from existing suites)

These override generic textbook advice when they conflict.

1. **Lowest layer that can fail for the right reason.** UI unit (Jest/RTL) or API unit (JUnit) first. Cypress *integration* with intercepts for UI+mocked API. Live e2e only for journeys the lower layers cannot prove. Smoke is a short gate, not a copy of regression.
2. **Suite tags, not one pile of tests.**
   - UI Selenium: `@PreApps` smoke/happy path; `@coreTest` regression; `@PostApps` production, non-invasive only.
   - UI frontend: Jest on every commit; Cypress integration vs e2e via `CYPRESS_TYPE`; Playwright/Cypress `smoke` on CI; role folders (auth, visitor, TA, restricted, …).
   - API: unit in `mvn clean install`; smoke/regression/load only with `post-deployment` against a running app; Pact separately.
3. **Shared `data-testid` / testID modules** are the locator source of truth. Selenium page objects and Cypress/Playwright tests must use the same ids the product ships (`getByTestId`, `@FindBy` on `data-testid`). Do not add brittle absolute XPath for new work.
4. **No `Thread.sleep`.** Wait for a condition (`element.waitFor()`, Cypress default timeouts, Playwright expect timeout).
5. **Create and delete test data via API** in UI smoke/e2e (entitlements, courses). Register cleanup (`after` / `CourseCleanupExtension`). Do not leave courses in the environment.
6. **API smoke asserts status + JSON schema** (RestAssured `validateSchema`), not only “200”. Tag optional dependencies (`pdm`, `olr`, `crp`) so a missing collaborator does not fail the whole gate.
7. **Environment-agnostic scenarios.** `seleniumserver=local|remote|lambdatest` and Cypress/Playwright `BASE_URL` stay in config/driver factory. Secrets: `LT_USERNAME` / `LT_ACCESS_KEY`, `.env`, config-repo — never commit keys. Cypress intercepts belong in integration tests, not as a substitute for smoke against a real BFF.
8. **Personas.** UI regression covers auth vs anonymous vs restricted/TA/visitor/region where the product has those experiences. Selenium YAML is **per tier** (`QA_TestData.yml`, `PROD_TestData.yml`, …). Use `@ignoreDev` / `@ignoreStage` only with a recorded reason.
9. **Soft asserts** only for non-critical UI (copy, color). Critical path uses hard asserts. Screenshot on UI failure; always `quit` the WebDriver.
10. **Page objects / helpers own actions.** Cucumber `@Step` on the page, not the stepdef. Browser tab/window actions only in the Browser helper. Stepdefs pass data via Context. No `System.out`; use the logger.

## Artifacts

```text
docs/qa/<ticket-or-slug>/
  test-cases.md
  test-review.md
  qa-estimate.md
```
