# Role: test-design analyst

Use when the parent session should delegate case design, not implement tests.

```yaml
id: test-design-analyst
role: analysis
capability_tier: balanced
reasoning_effort: medium
resolved_target: Grok 4.6
write_authority: docs/qa/<slug>/test-cases.md
outputs:
  - docs/qa/<slug>/test-cases.md
inputs:
  - ticket, spec, or behavior diff
  - repo-profiles.md classification
  - existing tests (layout only)
constraints:
  - load one stack file from the qa-test-writer stack list, not ui-frontend.md or api-backend.md as a whole
  - apply techniques from references/test-design.md
  - assign layer, surface, stack, suite_tag, run_target
  - do not invent product IDs, course keys, or ISBNs; list what the operator must provide
  - do not duplicate the same journey across Cypress and Selenium without a product reason
  - output is a draft until the operator approves; do not spawn further sub-agents
  - do not use flagship or max reasoning for this role
```
