# Repo profiles

Classify the open repository before designing or reviewing tests.

## ui-frontend (example: fx-ui)

**Signals:** `package.json` scripts `test` (Jest), `cy:local:int` / `cy:run:e2e`, `playwright:local` / `playwright:ci:smoke`; `src/**/*.test.tsx`; `cypress/`; `playwright/`; `src/testID/`.

| Layer | How it looks here |
|---|---|
| unit | Jest + Testing Library, colocated `__tests__`, mocked hooks/API, `getByTestId` from `@fx-ui/testID/*`. Coverage gate ~85%. Husky runs lint + unit on commit. |
| integration | `CYPRESS_TYPE=integration` — Cypress with `cy.intercept` fixtures under `cypress/fixtures/apiMocks`. |
| e2e | `CYPRESS_TYPE=e2e` — live app (`baseUrl`), real BFF. Suites split by **persona**: AuthUser, NonAuthUser, TeacherAssistant, Restricted, Visitor, Suspended, EMEA, NonUs. |
| smoke | `cypress/e2e/smoke/*` and `playwright/smoke/*`. Auth via API token → `storageState`. Seed/cleanup entitlements and courses with `cy.request` / Playwright `request`. CI: retries on, `forbidOnly`. |

Do not add Selenium here. Load one file from the root skill table: [ui-unit.md](ui-unit.md), [cypress.md](cypress.md), or [playwright.md](playwright.md).

## api-backend (example: fx-bff)

**Signals:** parent POM; `impl/src/test`; `app/src/test` with WireMock; `contract-tests` (Pact); `deployment-tests/smoke|regression|load`.

| Layer | How it looks here |
|---|---|
| unit | JUnit 5 + Mockito on endpoints/services/mappers. Default `mvn clean install`. |
| integration | WireMock mappings for downstream HTTP; Spring/app tests that are still in the normal build if present. |
| contract | Pact consumer tests; publish to pact-broker (`-Plocal-pact`). |
| smoke / regression | RestAssured against a **running** instance. **Not** run in a normal build — activate `post-deployment`. Assert status + JSON schema. `@Tag` for optional collaborators (`pdm`, `olr`, `crp`, `adonis`). Cleanup extension for created courses. Config from system properties / config-repo. |
| load | Gatling `simulationClass`, `maxUsers` / ramp / sustained. Also post-deployment only. |

Do not put RestAssured smoke into the unit module. Load one file: [backend-unit.md](backend-unit.md), [contract-pact.md](contract-pact.md), or [deployment.md](deployment.md).

## ui-selenium (example: stx-e2e-tests)

**Signals:** Cucumber `src/test/resources/features`; page objects; `Config.properties` `seleniumserver`; dependency `selenium-core`. Suite tags `@PreApps` / `@PostApps` / `@coreTest` belong to **this repo only**.

| Layer | How it looks here |
|---|---|
| smoke | `@PreApps` — most-used happy paths. |
| prod smoke | `@PostApps` — production, minimal, non-invasive. |
| regression | `@coreTest` — main functionality. Feature-level tags (`@StxInternational`, `@StxOrders`, …). |
| env skip | `@ignoreDev` `@ignoreStage` with a reason. |
| run | `mvn clean verify -Dtags=@PreApps -Dbrowser=chrome -Dtier=qa -Dseleniumserver=local\|lambdatest -DforkCount=5`. YAML data per tier. Parallel Cucumber. Screenshot on fail; quit driver in `@After`. |

Follow [java-selenium.md](java-selenium.md) and [execution-environments.md](execution-environments.md).

## Mixed / monorepo

If UI and BFF are separate repos (fx-ui + fx-bff), design cases per repo. A UI smoke that hits `/api/*` still belongs in the UI repo; contract and schema smoke belong in the BFF. Selenium e2e is a third repo — do not duplicate the same journey in Cypress and Selenium without a reason (usually different products: instructor center vs student STX).
