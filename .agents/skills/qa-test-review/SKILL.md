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

Read this skill only when the kit router or `qa-orchestrator` selected test-quality review.

This output is a **briefing** for the operator. A `pass` verdict does not close the human gate.

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- Escalate to balanced/high only for auth, money/checkout, leftover-data, or LambdaTest-only flake. Flagship/medium only after balanced missed a high-impact gap.
- Role: [test-quality-reviewer.md](../qa-test-writer/roles/test-quality-reviewer.md) — same envelope as this skill. Orchestrator spawn only.

## Steps

1. Name `<slug>`. Inspect the diff, new tests, and test layout.
2. Classify the repo via [repo-profiles.md](../qa-test-writer/references/repo-profiles.md).
3. Review against [review-rubric.md](../qa-test-writer/references/review-rubric.md) and **one** stack file from the qa-test-writer stack list (Jest, Cypress, Playwright, backend unit, Pact, deployment, Selenium, or local/LambdaTest).
4. Write `docs/qa/<slug>/test-review.md` from [test-review.md](../qa-test-writer/assets/templates/test-review.md). Set `Human gate: pending`.
5. Do not change product or test code unless the operator asked. Do not treat this review as final.

## Findings

Use severity: **blocker**, **should-fix**, **nit**. Each finding needs a file or test name, what is wrong, and what “good” looks like.

## Rules

- Missing tests for new behavior is a finding, not a pass.
- Wrong layer (UI e2e for a mapper; RestAssured in the unit build) is should-fix or blocker.
- Missing cleanup, leaked driver, or committed secrets is blocker.
- Draft until operator approval. This skill cannot close the human gate. The parent orchestrator owns Task spawn.
