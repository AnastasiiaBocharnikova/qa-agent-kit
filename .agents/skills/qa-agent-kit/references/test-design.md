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
| Use case / happy path | One proof the feature works | one smoke (`@PreApps` or Playwright smoke), not five UI copies |

## Product-specific cues

- **fx-ui:** If it is render/state/analytics, write Jest. If it is a page with HTTP, prefer Cypress integration + fixture. If it is login, library, create course — extend smoke and add cleanup.
- **fx-bff:** Endpoint/mapper/strategy → JUnit. Downstream HTTP → WireMock. Cross-service shape → Pact. “Does QA/stage still work?” → RestAssured smoke + schema, with `@Tag` if a collaborator may be down.
- **stx-e2e:** New student journey → feature file + page object + `@coreTest`. If it is the main happy path, also `@PreApps`. If it must run in production, `@PostApps` and keep it non-invasive (no leftover purchases).

Do not add a Selenium scenario that only re-checks an API contract. Do not add Cypress e2e that only re-checks a Jest assertion.
