# QA Agent Kit

When **writing tests** (TDD: every cycle), load `.agents/skills/qa-agent-kit/SKILL.md` first. It has the shared foundation. Then load **only one** stack file named there (Cypress, Jest, backend unit, deployment, Selenium, …). Do not preload the rest.

This kit is standalone. It does not require Dev Doc Harness. Optional artifacts: `docs/qa/<ticket-or-slug>/`.

## Route

| Request | Skill | Default model (tier / effort) | Current Cursor mapping |
|---|---|---|---|
| Writing tests / TDD | `qa-agent-kit` (this root) | balanced / medium | Grok 4.6 |
| Case list only, no implementation | `qa-test-design` | balanced / medium | Grok 4.6 |
| PR, “are these tests good enough” | `qa-test-review` | balanced / medium | Grok 4.6 |
| Ticket estimate, plan split | `qa-effort` | fast/economy / low | Composer 2.5 Fast |

Do not start QA work on a flagship or max-reasoning model. Escalate a **review** to balanced/high only for auth, money/checkout, leftover data, or LambdaTest-only flake. Full table: `.agents/skills/qa-agent-kit/references/model-selection.md`.

## Detect stack, then load one file

The root skill’s “Where to look” table is authoritative. Profile cheat sheet: `.agents/skills/qa-agent-kit/references/repo-profiles.md`.

Do not force Java+Selenium onto a React UI repo, or Cypress onto a Java BFF.

## House rules (from existing suites)

These sit in the root skill so they load every time tests are written:

1. Lowest layer first (unit → mocked integration → live e2e → short smoke).
2. Suite tags from **that repo**: Cypress persona folders / Playwright `smoke`; JUnit `@Tag`; post-deploy not in `mvn clean install`. `@PreApps` / `@coreTest` / `@PostApps` exist only in **stx-e2e-tests**, not in fx-ui or fx-bff.
3. Shared `data-testid` / testID modules. No new absolute XPath. No `Thread.sleep`.
4. API seed and cleanup. Screenshot on UI fail; quit WebDriver. No secrets in git.
5. Cypress intercepts = integration, not a substitute for live smoke. API smoke = status + JSON schema.
6. Personas and per-tier YAML. `@ignoreDev` only with a reason. Soft assert only for non-critical UI.

## Artifacts

```text
docs/qa/<ticket-or-slug>/
  test-cases.md
  test-review.md
  qa-estimate.md
```
