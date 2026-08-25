---
name: qa-test-design
description: >-
  Writes a layered test-case list without implementing tests. Use when the
  operator wants cases only, not TDD or test code. When requested, it can also
  offer to create one consolidated Zephyr Test in Jira and populate its
  structured Test Step, Test Data, and Expected Result fields. For writing
  tests, use qa-agent-kit instead.
disable-model-invocation: true
---

# QA Test Design

Use this skill only for a **case list without implementation**. When writing tests or doing TDD, use the root `qa-agent-kit` skill instead and load one stack file.

Read this skill only when the kit selected test design (no code).

## Model

- capability_tier: `balanced`
- reasoning_effort: `medium`
- resolved_target: Grok 4.6
- Sub-agent: [test-design-analyst.md](../qa-agent-kit/roles/test-design-analyst.md) uses the same envelope. Do not escalate to flagship for case lists.

## Steps

1. Name `<slug>` and the behavior. Read the ticket, spec, or behavior diff.
2. Classify the repo via [repo-profiles.md](../qa-agent-kit/references/repo-profiles.md).
3. List risks: input boundaries, rules, states, personas, auth, money, leftover data.
4. Pick techniques from [test-design.md](../qa-agent-kit/references/test-design.md). Do not apply every technique.
5. Assign layer, surface, stack, suite_tag, and run_target using [test-layers.md](../qa-agent-kit/references/test-layers.md). Load **one** stack file from the write-tests skill table (Jest, Cypress, Playwright, backend unit, Pact, deployment, or Selenium).
6. Write `docs/qa/<slug>/test-cases.md` from [test-cases.md](../qa-agent-kit/assets/templates/test-cases.md).
7. Stop. Do not implement tests unless the operator asked.

## Zephyr workflow

When the operator asks to use Zephyr, or asks to create the test cases in Jira:

1. Prepare the case list first and explicitly offer to create a Zephyr `Test`.
2. By default, consolidate the requested coverage into one Test issue unless
   the operator asks for multiple tests.
3. Create the Jira issue as type `Test`, then open the created issue. Link it to
   the source ticket with the relationship `is a test for` when that relation
   is available.
4. Do not put the test procedure only in Jira Description. Use the Zephyr
   Test Details form. Add one row per meaningful action/assertion and populate:
   - `Test Step`: the action the tester performs;
   - `Test Data`: the value, persona, environment, or input used;
   - `Expected Result`: the observable outcome.
5. Keep the first step concise: normally it should contain only navigation or
   setup. Do not put the entire scenario into the first row.
6. In this Zephyr UI, use the row-level tick action (`Add Steps`, class/action
   `addstep`) to append the next row. The top `Add Step` control may not create
   a row reliably through browser automation.
7. Work one row at a time: fill all three visible fields in the current row,
   click its tick/save action, then append the next row. Do not append several
   blank rows before filling them; this can leave empty rows between valid
   steps and shift data into the wrong row.
8. After saving, verify the row numbers and the text in each column. If a row
   has Test Data or Expected Result but no Test Step, correct that row before
   continuing. Remove accidental empty persisted rows only after confirming the
   exact row and accepting Zephyr's irreversible-delete warning.
9. Ask for confirmation immediately before creating the Jira Test or making
   other external changes. Creating the issue and adding its steps are separate
   external mutations; if the issue was already created with confirmation,
   adding the structured steps is within the same explicitly requested Zephyr
   workflow, but still verify the target issue before editing it.

For a Zephyr request, the local `docs/qa/<slug>/test-cases.md` remains useful as
an audit artifact, but the Jira Test Details rows are the source of truth for
execution.

## Rules

- Prefer unit, then mocked integration, then live e2e. Smoke is a short tagged gate.
- Every live UI e2e case must say why Jest/API/Cypress-int cannot prove it.
- Put tests in the repo that owns the layer (UI vs BFF vs Selenium suite). Do not duplicate the same journey in Cypress and Selenium without a product reason.
- Default run target follows the profile (Jest/JUnit: local+CI; Selenium smoke: local and LambdaTest).
- If a sub-agent would help, use [test-design-analyst.md](../qa-agent-kit/roles/test-design-analyst.md).
