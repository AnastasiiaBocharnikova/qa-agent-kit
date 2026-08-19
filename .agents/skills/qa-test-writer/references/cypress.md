# Cypress

Load only when writing files under `cypress/` (fx-ui).

- **Integration** (`CYPRESS_TYPE=integration`): `cy.intercept` + `cypress/fixtures/apiMocks`. Pin UI to a known payload (persona `getUsersMe` / `getVisitorMe` / …).
- **E2E** (`CYPRESS_TYPE=e2e`): live `baseUrl`, real BFF. Split specs by persona under `cypress/e2e/regression/<Persona>/`.
- **Smoke:** `cypress/e2e/smoke`. Login helper; seed and delete entitlements/courses with `cy.request`. Intercept only to *wait* on live calls (`cy.intercept(...).as('search')`), not to replace the BFF. If the journey needs a catalog product or existing course key, ask the operator — do not invent it.
- Timeouts and `retries` are already high — do not add `cy.wait(5000)`.
- Credentials from `.env` / `FXUSERPASSWORD_SECRET`. Never commit `.env`.
- Locators: same `data-testid` / `src/testID` as Jest.

Component state without HTTP → [ui-unit.md](ui-unit.md). CI browser smoke in Playwright → [playwright.md](playwright.md).
