# Model selection

Optimize for **price / quality / speed**. Do not start a QA role on a flagship or max-reasoning model. After the root write-tests skill, load **one** stack file — not the whole `references/` folder.

Portable fields (stable): `capability_tier` + `reasoning_effort`.  
`resolved_target` is a current Cursor mapping (2026-08) and may be remapped when the runtime names change.

| Role | capability_tier | reasoning_effort | resolved_target | Why |
|---|---|---|---|---|
| `qa-orchestrator` | fast/economy | low | Composer 2.5 Fast | Classify and dispatch. Not design, write, or review. |
| Write tests / TDD `qa-agent-kit` | balanced | medium | Grok 4.6 | Foundation + one stack file. Not architecture. |
| `qa-test-design` / `test-design-analyst` | balanced | medium | Grok 4.6 | Case list only. |
| `qa-test-review` / `test-quality-reviewer` | balanced | medium | Grok 4.6 | Rubric + diff. Escalate only when the table below matches. Never closes the human gate. |
| `qa-effort` / `qa-effort-advisor` | fast/economy | low | Composer 2.5 Fast | S/M/L table. |

## Escalate (once, with a reason)

Use **balanced / high** when a **review** spans auth, money/checkout, leftover-data risk, or LambdaTest-only flake.

Use **flagship / medium** only after balanced missed a high-impact gap. Do not use flagship/high or max for kit work.

## Save tokens besides the model

- Writing tests: root skill + **one** stack reference.
- Curated context: ticket + the files you are editing, not the whole monorepo.
- Sub-agents: same envelope as the parent role. The orchestrator decides when to spawn; specialists do not self-spawn.
- Fast/economy must not be the final authority on a blocker finding in auth/money.
- Human review is the release gate. Agent review is a briefing.
