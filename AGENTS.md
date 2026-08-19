# QA Agent Kit

There is **one** orchestrator. The other two files are not dispatchers.

- **`AGENTS.md`** (this file) — map: which skill to open. Does not spawn Task agents or write tests.
- **`qa-orchestrator`** — only dispatcher (mixed/ticket, hybrid spawn, human gate). Does not write tests or load stack files.
- **`qa-agent-kit`** — write-tests specialist: foundation + one stack index. Not a router; does not choose design / review / effort.

When **writing tests** (TDD: every cycle), load `.agents/skills/qa-agent-kit/SKILL.md` first. Then load **only one** stack file named there. Do not preload the rest.

Mixed or ambiguous QA (“QA this ticket”, design + estimate or write, UI + BFF, write-then-review) goes through `.agents/skills/qa-orchestrator/SKILL.md`.

This kit is standalone. It does not require Dev Doc Harness. Optional artifacts: `docs/qa/<ticket-or-slug>/`. Artifacts and generated tests are **drafts** until the operator reviews them. Agent `qa-test-review` is a briefing, not the release gate.

## Skill map

- Mixed / “QA this ticket” → `qa-orchestrator` · Composer 2.5 Fast (fast/economy, low)
- Writing tests / TDD → `qa-agent-kit` · Grok 4.6 (balanced, medium)
- Case list only → `qa-test-design` · Grok 4.6 (balanced, medium)
- PR / “are these tests good enough” → `qa-test-review` · Grok 4.6 (balanced, medium)
- Ticket estimate → `qa-effort` · Composer 2.5 Fast (fast/economy, low)

Do not start QA work on a flagship or max-reasoning model. Escalate a **review** to balanced/high only for auth, money/checkout, leftover data, or LambdaTest-only flake. Full table: `.agents/skills/qa-agent-kit/references/model-selection.md`.

## Detect stack, then load one file

The write-tests skill’s “Where to look” table is authoritative. Profile cheat sheet: `.agents/skills/qa-agent-kit/references/repo-profiles.md`.

Do not force Java+Selenium onto a React UI repo, or Cypress onto a Java BFF.

## Human review before final

Nothing in this kit is final until the operator says so. Do not commit, push, mark merge-ready, or auto-apply review fixes without that approval. A `qa-test-review` `pass` still waits for the human gate.

If a test needs a real product, course key, ISBN, or similar catalog value, **stop and ask the operator**. Do not guess.

## House rules (from existing suites)

These sit in the write-tests skill so they load every time tests are written:

1. Lowest layer first (unit → mocked integration → live e2e → short smoke).
2. Suite tags from **that repo**: Cypress persona folders / Playwright `smoke`; JUnit `@Tag`; post-deploy not in `mvn clean install`. `@PreApps` / `@coreTest` / `@PostApps` exist only in **stx-e2e-tests**, not in fx-ui or fx-bff.
3. Shared `data-testid` / testID modules. No new absolute XPath. No `Thread.sleep`.
4. API seed and cleanup. Do not invent product IDs, course keys, or other env-specific test data — ask the operator. Screenshot on UI fail; quit WebDriver. No secrets in git.
5. Cypress intercepts = integration, not a substitute for live smoke. API smoke = status + JSON schema.
6. Personas and per-tier YAML. `@ignoreDev` only with a reason. Soft assert only for non-critical UI.

## Artifacts

```text
docs/qa/<ticket-or-slug>/
  test-cases.md
  test-review.md
  qa-estimate.md
```
