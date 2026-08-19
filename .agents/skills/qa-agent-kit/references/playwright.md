# Playwright

Load only when writing files under `playwright/` (fx-ui smoke).

- `playwright/smoke` + `auth.setup.ts` writing `storageState`.
- `test.use({ storageState })`. Seed/cleanup with `request.put/delete` on `/api/entitlements` and `/api/courses`.
- `getByTestId` aligned with `src/testID`.
- CI: `retries: 2`, `forbidOnly`, `workers: 1`. Local: `npm run playwright:local`.
- Secrets from env / config-repo, not committed files.

Persona regression in Cypress → [cypress.md](cypress.md). Component tests → [ui-unit.md](ui-unit.md).
