# Zephyr steps

One table per case. Consecutive rows. **No blank lines between rows. No empty rows.**

Zephyr Scale columns: Step, Test Data, Expected Result. Zephyr numbers the rows — do not insert spacer steps.

| Step | Test Data | Expected Result |
|------|-----------|-----------------|
| Scroll down to a position clearly below the top of the results | | The lower part of the results or footer is visible |
| Submit a new search without manually scrolling back to the top | math | Results for the new search are displayed |
| Verify the scroll position after the new results render | | The results view is at the top (or the product’s specified position) |

- **Step** and **Expected Result** are required on every row.
- **Test Data** may be an empty cell. That is not an empty step.
- Do not emit a row of only `|`, a blank markdown line inside the table, or a second table for the next step.
- Wiki paste uses the same rule: no blank line between `|...|` rows.

Wrong (blank line → empty Zephyr step):

```text
| Scroll down | | Footer is visible |

| Submit a new search | math | New results are displayed |
```
