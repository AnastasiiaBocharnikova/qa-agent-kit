# Commit message

`type(TICKET-ID): Description`

- `type`: `feat` | `fix` | `test` | `chore` | `refactor` | `build`
- `TICKET-ID`: Jira key the operator provided (`DASH-2208`). Do not invent one. If missing, stop and ask.
- `Description`: imperative, starts with a capital letter, no period.

## Cypress

- New or changed specs, fixtures, or test locators → `test`
- Cypress package or Cypress config only → `build`
- Do not use `feat` for a test file.

```text
test(DASH-2208): Add Cypress coverage for AppBar skip link
test(DASH-2208): Use findByDataTestId in AppBar focus test
build(DASH-1234): Update Cypress dependencies
```
