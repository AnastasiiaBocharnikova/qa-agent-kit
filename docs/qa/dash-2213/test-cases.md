# Test cases: DASH-2213

- Work slug: `dash-2213`
- Behavior: Validation errors for `Section Name` are cleared after the value becomes valid, and any remaining validation error blocks course/section creation.
- Repo profile: ui-frontend (`fx-ui`)
- Sources: Jira DASH-2213; QA environment; course creation flow, step 4, `Section Information`

| ID | Case | Technique | Layer | Surface | Stack | Suite tag | Run target | Auto / manual | Priority |
|---|---|---|---|---|---|---|---|---|---|
| TC-001 | Enter a valid `Section Name` after an invalid value containing `\\`; verify the validation message disappears immediately | Boundary / state transition | integration | ui | Cypress | AuthUser | local + CI | auto | P0 |
| TC-002 | Enter valid `Section Name` values after each forbidden character: `%`, `\\`, `/`; verify no validation error remains | Equivalence partitioning | integration | ui | Cypress | AuthUser | local + CI | auto | P0 |
| TC-003 | Enter an invalid `Section Name`, then replace it with a valid value and click `Finish`; verify the course/section is created and no stale validation message is displayed | End-to-end journey | e2e | ui | Cypress | AuthUser | local + CI | auto | P0 |
| TC-004 | Leave any validation error on the form and click `Finish`; verify submission is blocked and no course/section is created | Negative / invariant | e2e | ui | Cypress | AuthUser | local + CI | auto | P0 |
| TC-005 | Trigger validation, correct the value, then make it invalid again; verify the message is shown again and submission is blocked | State transition | integration | ui | Cypress | AuthUser | local + CI | auto | P1 |
| TC-006 | Correct the value using typing, select-all replacement, and deleting/re-entering; verify validation state is recalculated consistently | Interaction variation | integration | ui | Cypress | AuthUser | local + CI | auto | P1 |
| TC-007 | Refresh or navigate back to step 4 after a failed validation attempt; verify stale validation state is not incorrectly retained for a valid value | State reset | e2e | ui | Cypress | AuthUser | local + CI | auto | P1 |

## Notes

- Why live e2e exists: TC-003, TC-004, and TC-007 must verify the real course-creation submission and that invalid form state cannot create backend data; Cypress integration alone cannot prove this.
- Data setup/cleanup: use the Jira-provided QA user and course-creation URL. Remove any successfully created test course/section through the project cleanup mechanism or API after each applicable case.
- Expected validation text for forbidden characters: `These special characters are not allowed: % \\ /`.
- Out of scope: browser compatibility testing is not specified in the ticket; API validation rules are covered only indirectly through the real submission journey.
