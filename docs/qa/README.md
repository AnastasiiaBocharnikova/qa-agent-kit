# docs/qa

Ticket-local QA artifacts live here:

```text
docs/qa/<ticket-or-slug>/
  test-cases.md
  test-review.md
  qa-estimate.md
```

`<ticket-or-slug>` is a Jira key (`DASH-123`) or a short kebab name (`checkout-coupon`). Create only the files the routed skill needs.

These files are **drafts** until the operator sets status/human gate to approved. Agent review cannot mark them final.

Templates: `.agents/skills/qa-agent-kit/assets/templates/`.
