---
name: qa-test-design
description: >-
  Writes a layered test-case list without implementing tests. Use when the
  operator wants cases only, not TDD or test code. For writing tests, use
  qa-test-writer instead.
disable-model-invocation: true
---

# QA Test Design

Use this skill only for a **case list without implementation**. When writing tests or doing TDD, use the root `qa-test-writer` skill instead and load one stack file.

Read this skill only when the kit selected test design (no code), or when `qa-orchestrator` dispatched this specialist. Outputs are **drafts** until the operator approves. Do not spawn sub-agents; the parent orchestrator decides.

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- Role: [test-design-analyst.md](../qa-test-writer/roles/test-design-analyst.md) uses the same envelope. Do not escalate to flagship for case lists.

## Steps

1. Name `<slug>` and the behavior. Read the ticket, spec, or behavior diff.
2. Classify the repo via [repo-profiles.md](../qa-test-writer/references/repo-profiles.md).
3. List risks: input boundaries, rules, states, personas, auth, money, leftover data.
4. Pick techniques from [test-design.md](../qa-test-writer/references/test-design.md). Do not apply every technique.
5. Assign layer, surface, stack, suite_tag, and run_target using [test-layers.md](../qa-test-writer/references/test-layers.md). Load **one** stack file from the qa-test-writer stack list (Jest, Cypress, Playwright, backend unit, Pact, deployment, or Selenium).
6. Write `docs/qa/<slug>/test-cases.md` from [test-cases.md](../qa-test-writer/assets/templates/test-cases.md). Mark it draft. List any product, course key, ISBN, or catalog value the operator must provide. Leave those cells empty rather than inventing them.
7. Stop. Do not implement tests unless the operator asked. Wait for operator approval before treating the list as final. If required test data is missing, ask for it in the same stop.

## Rules

- Prefer unit, then mocked integration, then live e2e. Smoke is a short tagged gate.
- Every live UI e2e case must say why Jest/API/Cypress-int cannot prove it.
- Put tests in the repo that owns the layer (UI vs BFF vs Selenium suite). Do not duplicate the same journey in Cypress and Selenium without a product reason.
- Default run target follows the profile (Jest/JUnit: local+CI; Selenium smoke: local and LambdaTest).
- Do not invent product IDs, course keys, or ISBNs. Ask the operator for the correct value.
- Draft until operator approval. The parent orchestrator owns Task spawn.
