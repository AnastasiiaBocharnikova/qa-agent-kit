---
name: qa-agent-kit
description: >-
  Routes QA work to test design, test-quality review, or QA effort estimation.
  Use when covering new behavior with tests, reviewing unit/integration/e2e/smoke
  tests for UI or API (Jest, Cypress, Playwright, JUnit, Pact, RestAssured,
  Java Selenium), or when tests run locally, on CI, or on LambdaTest.
---

# QA Agent Kit

Standalone QA skill router. Not part of Dev Doc Harness.

## Model

- capability_tier: `fast/economy`
- reasoning_effort: `low`
- resolved_target: Composer 2.5 Fast
- See [model-selection.md](references/model-selection.md). Do not keep the session on a flagship model just to route.

## 1. Detect profile

Read [repo-profiles.md](references/repo-profiles.md) and classify the open repo as `ui-frontend`, `api-backend`, `ui-selenium`, or mixed. Follow that profile’s stacks. Do not invent a second framework.

## 2. Route

Pick **one** skill unless the operator asked for more than one:

| Request | Skill | Artifact | Model |
|---|---|---|---|
| New behavior, cover with tests, plan cases | `qa-test-design` | `docs/qa/<slug>/test-cases.md` | balanced / medium · Grok 4.6 |
| PR, diff, test adequacy | `qa-test-review` | `docs/qa/<slug>/test-review.md` | balanced / medium · Grok 4.6 |
| Estimate, ticket sizing, plan split | `qa-effort` | `docs/qa/<slug>/qa-estimate.md` | fast/economy / low · Composer 2.5 Fast |

`<slug>` is a ticket key (`DASH-123`) or a short kebab name. Reuse the folder if it already exists.

Then read that skill’s `SKILL.md`. Do not load the other two skills “just in case”.

## 3. Shared defaults

- Layers: unit → integration (mocked or in-process) → e2e (live) → smoke (short gate). See [test-layers.md](references/test-layers.md).
- UI locators: `data-testid` / shared testID modules.
- Run target: local, CI, LambdaTest (`seleniumserver`), or `both` as the profile allows.
- Write under `docs/qa/<slug>/` using `assets/templates/`.
- Read-only review unless the operator asked to change code.
- Obey house rules in the repo `AGENTS.md` (suite tags, cleanup, no sleep, post-deploy vs unit build).

## Load order for a routed skill

1. This router.
2. [repo-profiles.md](references/repo-profiles.md) if not already classified.
3. The selected skill `SKILL.md`.
4. Only the references that skill names.
5. Repo test layout, existing `docs/qa/<slug>/`, and the current diff or ticket.

## References

- [repo-profiles.md](references/repo-profiles.md)
- [test-design.md](references/test-design.md)
- [test-layers.md](references/test-layers.md)
- [ui-frontend.md](references/ui-frontend.md)
- [api-backend.md](references/api-backend.md)
- [java-selenium.md](references/java-selenium.md)
- [execution-environments.md](references/execution-environments.md)
- [review-rubric.md](references/review-rubric.md)
- [qa-effort.md](references/qa-effort.md)
- [model-selection.md](references/model-selection.md)
