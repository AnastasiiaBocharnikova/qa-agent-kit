# Test-design techniques

Pick the smallest set that matches the change. Name the technique on each case.

| Technique | Use when | Typical layer here |
|---|---|---|
| Equivalence partitioning | Distinct classes of input or ISBN/user type | unit, API, Cypress intercept variants |
| Boundary value analysis | Ranges, dates, amounts, course dates | unit, API |
| Decision table | Combined rules (role × entitlement × region) | unit or Cypress integration with persona fixtures (`getVisitorMe`, `getRestrictedMe`, …) |
| State transition | Course/section/entitlement lifecycle | API smoke with create→update→delete; UI only for the visible transition |
| Pairwise | Many independent filters (search facets) | API search tests first; one UI check for the control |
| Error guessing | Past bugs, env-only failures (`@ignoreDev`) | any; prefer unit/API |
| Persona / role | Product has auth, visitor, TA, restricted, EMEA | Cypress persona folders; YAML user types in Selenium |
| Use case / happy path | One proof the feature works | one smoke (Playwright/Cypress `smoke`, or STX `@PreApps`), not five UI copies |

## Product-specific cues

- **fx-ui:** If it is render/state/analytics, write Jest ([ui-unit.md](ui-unit.md)). If it is a page with HTTP, prefer Cypress integration ([cypress.md](cypress.md)). If it is login, library, create course — extend smoke ([playwright.md](playwright.md) or Cypress smoke) and add cleanup.
- **fx-bff:** Endpoint/mapper/strategy → [backend-unit.md](backend-unit.md). Downstream HTTP → WireMock in that file. Cross-service shape → [contract-pact.md](contract-pact.md). “Does QA/stage still work?” → [deployment.md](deployment.md).
- **stx-e2e:** New student journey → [java-selenium.md](java-selenium.md). Happy path also `@PreApps`. Production `@PostApps` and keep it non-invasive.

Do not add a Selenium scenario that only re-checks an API contract. Do not add Cypress e2e that only re-checks a Jest assertion.
