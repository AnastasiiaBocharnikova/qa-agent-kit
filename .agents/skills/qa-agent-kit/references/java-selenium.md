# Java + Selenium (Cucumber)

Applies to **ui-selenium** repos (stx-e2e-tests, same family as cs-admin-e2e-tests). Shared library: `selenium-core`. Layout: `pages`, `stepdef`, `steps`, `features`, `utils/ui/driver`.

## Structure

- **Pages** own locators and user actions. `@FindBy` on `data-testid` (or `aria-label` as fallback). Custom `Element` + `waitFor()` condition — never `Thread.sleep`.
- **`@Step`** belongs on the page (when the method is more than one action), not on the stepdef.
- **Stepdefs** glue Gherkin to pages. Pass data with `Context.set/get` (user/course helpers). Do not call `WebDriverFactory.getDriver()` from pages/stepdefs (legacy; do not add new calls).
- **Browser** class owns tabs, windows, `switchTo`, navigation.
- **YAML** per tier: `QA_TestData.yml`, `PROD_TestData.yml`, … Gherkin `{key}` resolves via the parameter transformer. Keep new keys in the right tier file.
- Feature files under `src/test/resources/features`. **These Cucumber tags are stx-e2e-tests only** (not fx-ui / fx-bff):
  - `@PreApps` — smoke / most-used happy paths
  - `@coreTest` — regression
  - `@PostApps` — production, non-invasive
  - feature tags (`@StxInternational`, `@StxOrders`, …)
  - `@ignoreDev` / `@ignoreStage` only with a comment/ticket

## Assertions and logs

- Critical checks: hard asserts.
- Style, color, non-blocking copy: `softAssertThat()`; `SoftAssertions.assertAll()` in `@After`.
- `@Slf4j` / `log.info` — no `System.out.println`.
- Failed scenario: screenshot attached; then `WebDriverFactory.quit()`.

## Code style

- camelCase for methods, variables, locator names.
- Meaningful names; delete dead code.
- Plugins via POM only — no checked-in drivers/jars.
- Parallel: Cucumber `forkCount` / `cucumber.execution.parallel`; tests must not depend on run order.

## Run

```text
mvn clean verify -Dtags=@PreApps -Dbrowser=chrome -Dtier=qa -Dseleniumserver=local
mvn clean verify -Dtags=@PreApps -Dbrowser=chrome -Dtier=qa -Dseleniumserver=lambdatest -DforkCount=5 -Dbuildname=STX_QA_Critical
```

`seleniumserver=local | remote | lambdatest`. Tunnel and credentials: [execution-environments.md](execution-environments.md).

## Mapping to layers

Most Selenium tests are **e2e** (`@coreTest`). `@PreApps` is **smoke**. `@PostApps` is **prod smoke**. Do not use Selenium to assert JSON contracts.
