# UI unit — Jest + Testing Library

Load only when writing `src/**/*.test.ts(x)` in a ui-frontend repo (fx-ui).

- Colocate tests with the component (`__tests__` or `*.test.tsx`).
- Render with the repo’s `Wrapper`. Mock API modules and context hooks; do not hit the network.
- Select with shared ids: `getByTestId(testID.…)` from `src/testID/`. Add a testID in product code if a new control has none.
- Cover loading, empty, error, and the action (click → handler/analytics). Do not snapshot the whole page.
- Keep the coverage gate (fx-ui: 85% branches/functions/lines/statements). Do not lower it to land a feature.
- Husky runs lint + unit on commit. Do not `--no-verify`.

If the test needs a real or mocked HTTP page, stop and load [cypress.md](cypress.md) instead.
