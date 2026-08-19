---
name: qa-estimate
description: >-
  Estimates QA effort for a ticket: test design, automation, exploratory,
  regression, and environment setup including local, CI, LambdaTest, and
  post-deploy API smoke. Use when sizing a ticket or splitting a plan.
disable-model-invocation: true
---

# QA Estimate

Read this skill only when the kit router or `qa-orchestrator` selected estimation. Outputs are **drafts** until the operator approves.

## Model

- capability_tier: `fast/economy`
- reasoning_effort: `low`
- resolved_target: Composer 2.5 Fast
- Role: [qa-estimate-advisor.md](../qa-test-writer/roles/qa-estimate-advisor.md) uses the same envelope. Do not use Grok/flagship for an S/M/L table.

## Steps

1. Name `<slug>` and the change. Reuse `test-cases.md` in the same folder if it exists.
2. Classify the repo (or repos) via [repo-profiles.md](../qa-test-writer/references/repo-profiles.md).
3. Score the buckets in [qa-estimate.md](../qa-test-writer/references/qa-estimate.md): design, automation, exploratory, regression, env/setup.
4. Call out LambdaTest / CI / post-deploy cost separately from local unit runs.
5. Name which repo takes the work (UI, BFF, Selenium suite) to avoid duplicates.
6. Write `docs/qa/<slug>/qa-estimate.md` from [qa-estimate.md](../qa-test-writer/assets/templates/qa-estimate.md). Mark it draft.

## Rules

- Use S / M / L plus a one-line reason. Do not invent story points.
- Env/setup is not free when LambdaTest tunnel, Cypress `.env`, or config-repo values are required.
- Draft until operator approval. The parent orchestrator owns Task spawn.
