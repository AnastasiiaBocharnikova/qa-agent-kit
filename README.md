# qa-agent-kit

Agent skills for **writing tests** (TDD), plus optional review, QA effort, and a thin orchestrator for mixed work.

Standalone. It does not depend on Dev Doc Harness. House rules come from **fx-ui**, **fx-bff**, and **stx-e2e-tests**.

## Who does what

- **Package:** `.agents/skills/` (`qa-orchestrator`, `qa-agent-kit`, `qa-test-design`, `qa-test-review`, `qa-effort`).
- **This repo’s `AGENTS.md`:** kit development only. Not copied into products.
- **Product insert:** [AGENTS.snippet.md](AGENTS.snippet.md) — paste into the existing product `AGENTS.md`. Do not replace that file.
- **`qa-orchestrator`:** only dispatcher (mixed/ticket, Task spawn, human gate).
- **`qa-agent-kit`:** write-tests specialist (foundation + one stack file).

## Install

1. Copy `.agents/skills/qa-orchestrator`, `qa-agent-kit`, `qa-test-design`, `qa-test-review`, and `qa-effort`.
2. Paste `AGENTS.snippet.md` into the product `AGENTS.md`.

## Progressive disclosure

1. Mixed or ticket-level QA → `qa-orchestrator`.
2. Writing tests / TDD → `qa-agent-kit`, then **one** stack file.
3. Do not load review or effort skills while writing tests.

Agent outputs are drafts until a human reviews them.

## License

Use and copy in your own repositories unless a later commit adds a different license.
