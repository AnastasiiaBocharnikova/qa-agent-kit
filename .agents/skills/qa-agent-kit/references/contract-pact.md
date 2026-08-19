# Pact contracts

Load only when writing `contract-tests` (fx-bff consumer tests).

- Consumer tests against the downstream provider shape. Publish with `-Plocal-pact` / broker flags.
- New BFF-to-downstream fields belong here, not only in RestAssured smoke.
- Local broker: pact-broker-docker; do not commit broker credentials.

In-process Mockito/WireMock → [backend-unit.md](backend-unit.md). Live QA/stage API → [deployment.md](deployment.md).
