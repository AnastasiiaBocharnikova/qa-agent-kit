# qa-agent-kit

Agent skills for **writing tests** (TDD), plus optional review, QA effort, and a thin orchestrator for mixed work.

Standalone companion package. It does not depend on Dev Doc Harness. Copy `AGENTS.md` (merge if the destination already has one) plus the `.agents/` folder into a product repository.

House rules come from **fx-ui**, **fx-bff**, and **stx-e2e-tests**.

## Who does what

- **`AGENTS.md`** — map only. Which skill to open. Not an orchestrator.
- **`qa-orchestrator`** — the only dispatcher (mixed/ticket, Task spawn, human gate).
- **`qa-agent-kit`** — write-tests specialist (foundation + one stack file). Not a router.

## Progressive disclosure

1. Mixed or ambiguous QA (“QA this ticket”, design + write, UI + BFF): load `.agents/skills/qa-orchestrator/SKILL.md`. It classifies and dispatches; it does not write tests.
2. Always load `.agents/skills/qa-agent-kit/SKILL.md` when writing tests (TDD: every cycle). That file is the shared foundation, not a dispatcher.
3. Load **only one** stack file it names: Jest, Cypress, Playwright, backend unit, Pact, deployment, or Selenium.
4. Do not load review or effort skills while writing tests.

Agent outputs are drafts. **Final** exists only after a human reviews them. `qa-test-review` is a briefing for the operator, not a substitute for that gate.

## Other skills

- Mixed / “QA this ticket” → `qa-orchestrator` · Composer 2.5 Fast
- Writing tests / TDD → `qa-agent-kit` · Grok 4.6
- Case list only → `qa-test-design` · Grok 4.6
- PR review → `qa-test-review` · Grok 4.6
- Estimate → `qa-effort` · Composer 2.5 Fast

## Install

Merge this repo’s `AGENTS.md` into the product `AGENTS.md`, and copy `.agents/skills/qa-orchestrator`, `qa-agent-kit`, `qa-test-design`, `qa-test-review`, and `qa-effort`.

## Layout

```text
AGENTS.md                            # map: which skill to open (not a dispatcher)
.agents/skills/qa-orchestrator/      # only dispatcher: mixed / ticket + human gate
.agents/skills/qa-agent-kit/SKILL.md # write-tests specialist + stack index
.agents/skills/qa-agent-kit/references/  # one file per stack
.agents/skills/qa-test-design/
.agents/skills/qa-test-review/
.agents/skills/qa-effort/
docs/qa/<slug>/                      # optional artifacts (drafts until human OK)
```

## License

Use and copy in your own repositories unless a later commit adds a different license.
