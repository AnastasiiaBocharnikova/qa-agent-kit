---
name: qa-test-design
description: >-
  Applies test-design techniques and writes a layered test-case list for new or
  changed behavior. Use when covering a feature with tests, planning QA for a
  ticket, or choosing Jest, Cypress, Playwright, JUnit, Pact, RestAssured, or
  Java Selenium layers.
disable-model-invocation: true
---

# QA Test Design

Read this skill only when the kit router selected test design.

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- Sub-agent: [test-design-analyst.md](../qa-agent-kit/roles/test-design-analyst.md) uses the same envelope. Do not escalate to flagship for case lists.

## Steps

1. Name `<slug>` and the behavior. Read the ticket, spec, or behavior diff.
2. Classify the repo via [repo-profiles.md](../qa-agent-kit/references/repo-profiles.md) (`ui-frontend`, `api-backend`, `ui-selenium`, or mixed).
3. List risks: input boundaries, rules, states, personas, auth, money, leftover data.
4. Pick techniques from [test-design.md](../qa-agent-kit/references/test-design.md). Do not apply every technique.
5. Assign layer, surface, stack, suite_tag, and run_target using [test-layers.md](../qa-agent-kit/references/test-layers.md). Load only the stack file you need: [ui-frontend.md](../qa-agent-kit/references/ui-frontend.md), [api-backend.md](../qa-agent-kit/references/api-backend.md), [java-selenium.md](../qa-agent-kit/references/java-selenium.md), [execution-environments.md](../qa-agent-kit/references/execution-environments.md).
6. Write `docs/qa/<slug>/test-cases.md` from [test-cases.md](../qa-agent-kit/assets/templates/test-cases.md).
7. Stop. Do not implement tests unless the operator asked.

## Rules

- Prefer unit, then mocked integration, then live e2e. Smoke is a short tagged gate.
- Every live UI e2e case must say why Jest/API/Cypress-int cannot prove it.
- Put tests in the repo that owns the layer (UI vs BFF vs Selenium suite). Do not duplicate the same journey in Cypress and Selenium without a product reason.
- Default run target follows the profile (Jest/JUnit: local+CI; Selenium smoke: local and LambdaTest).
- If a sub-agent would help, use [test-design-analyst.md](../qa-agent-kit/roles/test-design-analyst.md).
