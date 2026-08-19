# Local, CI, and LambdaTest

Same scenarios; different driver factory / base URL / capabilities.

## Selenium (`seleniumserver`)

| Value | Meaning |
|---|---|
| `local` | Machine Chrome/Firefox. Default while writing a test. `Config.properties`. |
| `remote` | Internal hub (`seleniumserverhost`). |
| `lambdatest` | Cloud grid. Capabilities: `browser`, `browserVersion`, `os`, `osVersion`, `resolution`, `geoLocation`, `idleTimeout`, `buildname`. |

LambdaTest tunnel starts automatically when `seleniumserver=lambdatest`.

- Local: env `LT_USERNAME` and `LT_ACCESS_KEY`.
- Jenkins: LambdaTest plugin credentials. Do **not** enable “Use Local Tunnel” in the plugin (the framework starts the tunnel).

Branch on `lambdatest` only in the driver factory or grid-only utilities (file download: `lambda-file-exists` / `lambda-file-content`). Set `lambda-name` from the scenario name. Always `quit` so grid sessions do not leak.

A failure only on LambdaTest is still a failure (wait, viewport, tunnel) — do not skip the test locally to hide it. STX smoke (`@PreApps`) should be runnable on **both** local and LambdaTest.

## Cypress / Playwright

- Local: `.env` from `.env.local`; `npm run cy:local:int` / `playwright:local`.
- CI: `playwright:ci:smoke`, `cy:ci`; `process.env.CI` enables retries and `forbidOnly`. `BASE_URL` / secrets from CI or config-repo — not committed files.

## API post-deploy

- App must be running (`localhost:8080` or `-DbaseUrl=https://….apps.dev.cengage.io`).
- `mvn test -Ppost-deployment`. Normal `mvn clean install` must not execute smoke/load.
