---
name: qa-test-review
description: >-
  Reviews unit, integration, e2e, and smoke tests for UI and API, including
  Jest, Cypress, Playwright, JUnit, Pact, RestAssured, Java Selenium, and
  local vs LambdaTest. Use when reviewing a PR or asking whether coverage is
  good enough.
disable-model-invocation: true
---

# QA Test Review

Read this skill only when the kit router selected test-quality review.

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- Escalate to balanced/high only for auth, money/checkout, leftover-data, or LambdaTest-only flake. Flagship/medium only after balanced missed a high-impact gap.
- Sub-agent: [test-quality-reviewer.md](../qa-agent-kit/roles/test-quality-reviewer.md) — same envelope as this skill.

## Steps

1. Name `<slug>`. Inspect the diff, new tests, and test layout.
2. Classify the repo via [repo-profiles.md](../qa-agent-kit/references/repo-profiles.md).
3. Review against [review-rubric.md](../qa-agent-kit/references/review-rubric.md) and the matching stack file: [ui-frontend.md](../qa-agent-kit/references/ui-frontend.md), [api-backend.md](../qa-agent-kit/references/api-backend.md), [java-selenium.md](../qa-agent-kit/references/java-selenium.md), [execution-environments.md](../qa-agent-kit/references/execution-environments.md).
4. Write `docs/qa/<slug>/test-review.md` from [test-review.md](../qa-agent-kit/assets/templates/test-review.md).
5. Do not change product or test code unless the operator asked.

## Findings

Use severity: **blocker**, **should-fix**, **nit**. Each finding needs a file or test name, what is wrong, and what “good” looks like.

## Rules

- Missing tests for new behavior is a finding, not a pass.
- Wrong layer (UI e2e for a mapper; RestAssured in the unit build) is should-fix or blocker.
- Missing cleanup, leaked driver, or committed secrets is blocker.
- If a sub-agent would help, use [test-quality-reviewer.md](../qa-agent-kit/roles/test-quality-reviewer.md).
