---
name: qa-orchestrator
description: >-
  Routes mixed or ambiguous QA work to specialist skills. Use when the
  operator says "QA this ticket", asks for design plus estimate or write,
  spans UI and BFF, or wants write-then-review. Do not use for a single TDD
  or "write this test" request — load qa-test-writer instead.
disable-model-invocation: true
---

# QA Orchestrator

This is the **only** dispatcher in the kit. Product `AGENTS.md` gets a short insert (`AGENTS.snippet.md`), not a replacement. The `qa-test-writer` skill writes tests; it does not route.

Classify, dispatch, stop for a human. Do not write tests, design cases, estimate, or review yourself.

## Model

- capability_tier: `fast/economy`
- reasoning_effort: `low`
- resolved_target: Composer 2.5 Fast
- Role: [qa-orchestrator.md](../qa-test-writer/roles/qa-orchestrator.md)

## Classify

1. Intent: design | estimate | write | review | mixed.
2. Repo via [repo-profiles.md](../qa-test-writer/references/repo-profiles.md). Mixed profiles → one specialist per profile/stack. Never two stack files in one agent.

Single write / TDD: stop routing. Tell the parent to load `qa-test-writer` plus one stack file.

## Dispatch

Stay in this chat when there is **one** specialist and no independence need:

- design only → `qa-test-design`
- estimate only → `qa-estimate`
- review this PR only → `qa-test-review`

Spawn a Cursor Task `generalPurpose` subagent when isolation buys something:

- Independent review after **this session** wrote tests.
- Parallel stacks/repos (Jest vs JUnit). One stack file per Task.
- Mixed pipeline: design and write in separate contexts.

Each Task prompt includes: the specialist skill path, the matching role YAML under `.agents/skills/qa-test-writer/roles/`, **one** stack file name from the write-tests list, and the slug. Models: Grok 4.6 for design/write/review; Composer 2.5 Fast for estimate.

## Pipeline (mixed / ticket)

1. Design → `docs/qa/<slug>/test-cases.md` (draft).
2. **HUMAN GATE.** Stop unless the operator already approved the list or said to skip this gate.
3. If implementing: write-tests per stack (Task if more than one stack).
4. Independent `qa-test-review` Task (not the writer).
5. **HUMAN GATE.** Present paths, agent findings, checklist. Wait.

Estimate-only after cases: load `qa-estimate`, then human gate.

If write or live e2e needs a real product, course key, ISBN, or other catalog value and the operator has not provided it, **STOP and ask**. Do not invent test data. API-created courses/entitlements (seed + cleanup) do not need this ask.

## Human gate (verbatim)

STOP. This is a draft, not final. Agent `qa-test-review` cannot close this gate. A `pass` verdict still waits for the operator.

Do not commit, push, mark merge-ready, or auto-apply should-fix/blocker fixes until the operator says so.

If a real product, course key, ISBN, or other catalog value is required and missing, ask for it here. Do not invent test data.

Present: artifact paths, what to check, agent findings if any, and any test-data ask. Then wait.

## Forbidden

- Loading all stack files, or writing tests yourself.
- Treating agent review as approval.
- Inventing product IDs, course keys, ISBNs, or other environment-specific test data.
- Copying STX `@PreApps` / `@coreTest` / `@PostApps` into other repos.
