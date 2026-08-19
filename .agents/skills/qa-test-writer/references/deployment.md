# Deployment tests — smoke, regression, load

Load only when writing `deployment-tests/` (fx-bff). Compiled in a normal build; **executed** only with `-Ppost-deployment` against a running app (`baseUrl`, default `http://localhost:8080/api`).

## Smoke / regression (RestAssured)

- `given(authorized()).when().get(...).then().spec(validateSchema(...))` — status **and** JSON schema.
- Config via `-D` / config-repo (ISBNs, context ids, tokens). No hardcoded stage passwords.
- Cleanup: `CourseCleanupExtension` (or try/finally) for every created course/entitlement.
- `@Tag` optional collaborators (`pdm`, `olr`, `crp`, `adonis`, `companionSites`) so CI can exclude a down service.
- Await readiness with Awaitility, not sleep.

## Load (Gatling)

- `deployment-tests/load`, `simulationClass`, `maxUsers`, `rampSeconds`, `sustainedLoadSeconds`.
- Not a substitute for functional smoke.

## Smells

- Smoke with no schema check; leftover courses; RestAssured inside `impl` unit tests.

Unit/WireMock → [backend-unit.md](backend-unit.md). Pact → [contract-pact.md](contract-pact.md).
