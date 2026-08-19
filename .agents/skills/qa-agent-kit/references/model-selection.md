# Model selection

Optimize for **price / quality / speed**. Do not start a QA role on a flagship or max-reasoning model. Load only the routed skill and the one stack reference you need — not the whole kit.

Portable fields (stable): `capability_tier` + `reasoning_effort`.  
`resolved_target` is a current Cursor mapping (2026-08) and may be remapped when the runtime names change.

| Role | capability_tier | reasoning_effort | resolved_target | Why |
|---|---|---|---|---|
| Router `qa-agent-kit` | fast/economy | low | Composer 2.5 Fast | Classify repo + pick one skill. No case design. |
| `qa-effort` / `qa-effort-advisor` | fast/economy | low | Composer 2.5 Fast | S/M/L table from a short ticket summary. |
| `qa-test-design` / `test-design-analyst` | balanced | medium | Grok 4.6 | Needs layer/technique judgment; not architecture. |
| `qa-test-review` / `test-quality-reviewer` | balanced | medium | Grok 4.6 | Rubric + diff. Escalate only when the table below matches. |

## Escalate (once, with a reason)

Use **balanced / high** (same Grok 4.6 class, more effort) when the review spans auth, money/checkout, leftover-data risk, or LambdaTest-only flake.

Use **flagship / medium** only after balanced missed a high-impact gap (security, PII, production `@PostApps` invasiveness). Do not use flagship/high or max for kit work.

## Save tokens besides the model

- One skill per request unless the operator asked for more.
- Curated context: ticket + diff + test layout, not the whole monorepo.
- Sub-agents: same envelope as the parent role. Do not give a reviewer a stronger model than this table without a written reason.
- Fast/economy must not be the **final** authority on a blocker finding in auth/money; escalate that review, do not re-run the whole kit on flagship.
