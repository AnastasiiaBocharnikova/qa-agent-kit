# Test layers and surfaces

Prefer the lowest layer that can fail for the right reason.

## Layers

| Layer | Proves | House mapping |
|---|---|---|
| unit | One component, function, endpoint, or mapper in isolation | Jest+RTL (`*.test.tsx`); JUnit+Mockito (`*Test.java`) |
| integration | UI page with mocked HTTP, or service with WireMock | Cypress `CYPRESS_TYPE=integration` + `cy.intercept`; WireMock in `app/src/test` |
| contract | Consumer/provider pact | Pact module; publish to broker |
| e2e | Live UI against a real BFF/app | Cypress `CYPRESS_TYPE=e2e`; Selenium `@coreTest` |
| smoke | Short deploy/prod gate | Playwright/Cypress `smoke`; Selenium `@PreApps`; RestAssured `deployment-tests/smoke`; prod `@PostApps` (non-invasive) |
| load | Capacity of a running API | `deployment-tests/load` (Gatling), post-deploy only |

Unit and in-build integration run on every commit / `mvn clean install` / Husky. Smoke, live e2e, regression Selenium, and load do **not** belong in that default build unless the repo already wired them that way.

## Surfaces

- **API** — HTTP status, JSON schema, auth headers, redirects, idempotency, cleanup of created resources.
- **UI** — What the user sees. Locators from shared testIDs. Personas (auth, anonymous, TA, restricted, region).
- **CLI** — Commands and exit codes (rare in these suites).

## Fields every case should carry

- `layer`: unit | integration | contract | e2e | smoke | load
- `surface`: ui | api | cli
- `stack`: jest-rtl | cypress-int | cypress-e2e | playwright | junit-mockito | wiremock | pact | rest-assured | java-selenium | gatling
- `suite_tag`: e.g. `@PreApps`, `@coreTest`, `@PostApps`, `smoke`, persona folder
- `run_target`: local | ci | lambdatest | both
