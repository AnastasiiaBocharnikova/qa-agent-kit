# QA effort

Estimate in S / M / L with a reason. Not story points.

| Bucket | S | M | L |
|---|---|---|---|
| Design | Few cases, one technique | Several rules, personas, or states | Combinations across UI+API+e2e repos |
| Automation | Extend existing Jest/JUnit/spec | New page object, Cypress persona, Pact, or schema | New framework, grid matrix, or flaky UI area |
| Exploratory | One pass of the happy path | Edge + adjacent persona | Cross-product (UI + BFF + Selenium) |
| Regression | Existing suite/tags enough | Extra `@PreApps`/smoke or a Cypress folder | Core auth, money, checkout, shared dashboard |
| Env / setup | Local unit only | LambdaTest or post-deploy already wired | New tunnel, credentials, browser matrix, new `baseUrl` |

Always split **local** vs **LambdaTest/CI** when UI automation is in scope: grid slots, tunnel, Cypress/Playwright CI retries, flake.

Post-deploy API smoke/load needs a running app and config-repo values — count that as env/setup, not as “free because RestAssured exists”.

## Output questions

1. Dedicated test task vs fold into implementation?
2. Smallest proof before merge (usually unit + schema or Jest; smoke if user-visible path)?
3. What waits for follow-up (extra personas, extra browsers, load)?
4. Which repo takes the test (fx-ui vs fx-bff vs stx-e2e) so work is not duplicated?
