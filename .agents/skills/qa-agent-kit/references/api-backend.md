# API backend (JUnit, WireMock, Pact, RestAssured, Gatling)

Applies to **api-backend** repos (fx-bff). Details: [repo-profiles.md](repo-profiles.md).

## Unit — JUnit 5 + Mockito

- Tests live next to code (`impl/src/test/.../*Test.java`).
- Endpoint tests mock services (`@ExtendWith(MockitoExtension.class)`); assert status, body mapping, and error codes (404/409/500), not only the happy path.
- Mapper/strategy/service tests cover branching (PDM vs hybrid vs OLR, region, empty lists).

## WireMock

- Downstream HTTP: mappings in the app test module (`WireMockExtension`, JSON/XML loaders).
- Do not call real Adonis/Gopher/OLR from unit tests.

## Pact

- Consumer tests in `contract-tests`. Publish with `-Plocal-pact` / broker flags.
- New BFF-to-downstream fields belong in a pact update, not only in a RestAssured smoke.

## Post-deployment smoke and regression

- Modules under `deployment-tests/`. Compiled in a normal build; **executed** only with `-Ppost-deployment` against a running app (`baseUrl`, default `http://localhost:8080/api`).
- RestAssured: `given(authorized()).when().get(...).then().spec(validateSchema(...))`.
- Config via `-D` / config-repo (ISBNs, context ids, tokens). No hardcoded stage passwords.
- **Cleanup:** `CourseCleanupExtension` (or equivalent) for every created course/entitlement. Use try/finally for demo products.
- **`@Tag`:** `pdm`, `olr`, `crp`, `adonis`, `companionSites` so CI can exclude a down collaborator.
- Await long-running readiness with Awaitility, not sleep.

## Load

- `deployment-tests/load`, Gatling `simulationClass`, `maxUsers`, `rampSeconds`, `sustainedLoadSeconds`.
- Not a substitute for functional smoke.

## Review smells

- Smoke test with no schema check
- Created course left behind
- RestAssured test inside `impl` unit suite
- Hitting real downstream from Mockito tests
