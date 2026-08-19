# Role: QA estimate advisor

Use when estimating should be isolated from implementation.

```yaml
id: qa-estimate-advisor
role: analysis
write_authority: docs/qa/<slug>/qa-estimate.md
outputs:
  - docs/qa/<slug>/qa-estimate.md
inputs:
  - ticket or spec
  - repo-profiles.md classification
  - docs/qa/<slug>/test-cases.md if present
constraints:
  - S/M/L only, no story points
  - split local vs CI/LambdaTest/post-deploy in env/setup
  - name which repo takes the test (UI, BFF, Selenium)
  - say if a dedicated test task is needed
  - output is a draft until the operator approves; do not spawn further sub-agents
```
