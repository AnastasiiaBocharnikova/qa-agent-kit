# Backend unit — JUnit, Mockito, WireMock

Load only when writing tests under `impl/src/test` or `app/src/test` (fx-bff). These run in `mvn clean install`.

- Colocate `*Test.java` with the code.
- Endpoint tests mock services (`@ExtendWith(MockitoExtension.class)`). Assert status, mapping, and 4xx/5xx, not only the happy path.
- Mapper/strategy/service tests cover branching (PDM vs hybrid vs OLR, region, empty lists).
- Downstream HTTP: WireMock mappings (`WireMockExtension`, JSON/XML loaders). Do not call real Adonis/Gopher/OLR.
- Do not put RestAssured smoke in this module.

New downstream field shape → [contract-pact.md](contract-pact.md). Running-app smoke → [deployment.md](deployment.md).
