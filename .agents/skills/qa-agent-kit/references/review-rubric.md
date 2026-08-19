# Test-quality review rubric

Review the **diff of tests** (and missing tests for new behavior). First apply [repo-profiles.md](repo-profiles.md), then this rubric plus the stack file (`ui-frontend.md`, `api-backend.md`, `java-selenium.md`).

## Unit (Jest / JUnit)

- Isolated from live network and browser (mocks / Mockito / WireMock)
- Names the rule; loading/empty/error or 4xx/5xx covered
- UI: uses shared testIDs, not ad-hoc CSS
- Does not drop the coverage gate to land the change

## Integration (Cypress intercept / WireMock)

- Fixtures live in `apiMocks` (or WireMock mappings), not copied JSON in the spec
- Persona/config fixtures match a real role (`getVisitorMe`, …)
- Not used as the only proof for a deploy gate

## Contract (Pact)

- New fields on a downstream call have a pact update
- Broker publish path unchanged unless the ticket is about the broker

## E2E (Cypress live / Selenium `@coreTest`)

- Journey, not a click-through of every control
- Locators: `data-testid` / testID module
- No `Thread.sleep` / `cy.wait(ms)` as sync
- Data setup/teardown via API; no order dependence
- Selenium: page object + tags; `@Step` on pages; Context in stepdefs; Browser helper for windows

## Smoke

- Short and tagged (`smoke`, `@PreApps`, Playwright project `smoke`)
- Runnable locally and on the grid/CI target used in Jenkins
- API smoke: schema + cleanup + tags for optional collaborators
- `@PostApps` / prod: non-invasive (no leftover purchases, no unpaid orders)

## Cross-cutting

| Smell | Severity |
|---|---|
| New behavior with no automated proof | blocker |
| UI e2e used where Jest or API unit would fail first | should-fix |
| Live Cypress e2e where intercept integration was enough | should-fix |
| RestAssured smoke inside the unit module / default Maven build | blocker |
| Created course/entitlement not cleaned up | blocker |
| Order-dependent tests / leaked WebDriver session | blocker |
| Secrets in repo, `.env` committed, LT keys in POM | blocker |
| New absolute XPath instead of `data-testid` | should-fix |
| Scenario-level `if (lambdatest)` without grid-only reason | should-fix |
| `Thread.sleep` / `System.out.println` | should-fix |
| Duplicate assertion at two layers that slows the gate | nit or should-fix |
