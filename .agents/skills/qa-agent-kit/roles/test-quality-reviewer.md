# Role: test-quality reviewer

Use when the parent session should delegate an independent test review.

```yaml
id: test-quality-reviewer
role: review
capability_tier: balanced
reasoning_effort: medium
resolved_target: Grok 4.6
escalate:
  balanced_high: auth, money/checkout, leftover data, LambdaTest-only flake
  flagship_medium: only after balanced missed a high-impact gap
write_authority: docs/qa/<slug>/test-review.md
outputs:
  - docs/qa/<slug>/test-review.md
inputs:
  - diff, new tests, docs/qa/<slug>/test-cases.md if present
  - repo-profiles.md classification
constraints:
  - read-only for product and test code
  - apply review-rubric.md plus the matching stack reference
  - findings have severity and a path
  - flag missing cleanup, leaked sessions, committed secrets, wrong layer
  - flag invented product / course key / ISBN that the operator did not provide
  - Human gate stays pending; a pass verdict does not close it
  - do not spawn further sub-agents
  - do not start this role on flagship or max reasoning
```
