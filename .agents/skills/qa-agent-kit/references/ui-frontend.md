# UI frontend (Jest, Cypress, Playwright)

Applies to **ui-frontend** repos (fx-ui). Details: [repo-profiles.md](repo-profiles.md).

## Unit — Jest + Testing Library

- Colocate `src/**/__tests__/*.test.ts(x)` with the component.
- Render with the repo’s `Wrapper`. Mock API modules and context hooks; do not hit the network.
- Select with shared ids: `getByTestId(testID.courseItem(...))` from `src/testID/`. Add a testID in product code if a new control has none.
- Cover loading, empty, error, and the action (click → handler/analytics), not a snapshot of the whole page.
- Keep the coverage gate (fx-ui: 85% branches/functions/lines/statements). Do not lower it to land a feature.
- Husky: lint + unit on staged files. Do not `--no-verify`.

## Cypress

- **Integration** (`CYPRESS_TYPE=integration`): `cy.intercept` + `cypress/fixtures/apiMocks`. Use this to pin UI to a known payload (persona `getUsersMe` / `getVisitorMe` / …).
- **E2E** (`CYPRESS_TYPE=e2e`): live `baseUrl`. Split specs by persona under `cypress/e2e/regression/<Persona>/`.
- **Smoke:** `cypress/e2e/smoke`. Login helper; seed and delete entitlements/courses with `cy.request`; intercept only to *wait* on live calls (`cy.intercept(...).as('search')`), not to replace the BFF.
- Timeouts and `retries` are already high for this app — do not add `cy.wait(5000)`.
- Credentials from `.env` / `FXUSERPASSWORD_SECRET`. Never commit `.env`.

## Playwright

- `playwright/smoke` + `auth.setup.ts` writing `storageState`.
- `test.use({ storageState })`. Seed/cleanup with `request.put/delete` on `/api/entitlements` and `/api/courses`.
- `getByTestId` aligned with the same testID module.
- CI: `retries: 2`, `forbidOnly`, `workers: 1` (as in fx-ui). Local: `playwright:local`.

## When to choose which

Jest (component) → Cypress integration (page + mock) → Cypress/Playwright smoke (live) → Cypress e2e regression (persona × feature). Stop at the first layer that proves the risk.
