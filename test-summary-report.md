# Test Summary Report — Swag Labs

| | |
|---|---|
| Project | Swag Labs manual testing |
| Execution date | 24 November 2026 |
| Environment | Chrome, https://www.saucedemo.com |
| Tester | Mohamed Tantawy |

## Execution Results

| Metric | Count |
|---|---|
| Test cases planned | 20 |
| Executed | 20 |
| Passed | 16 |
| Failed | 4 |
| Defects raised | 7 |

Result details per test case are recorded in the Result column of [test-cases.md](test-cases.md). Defect details are in [bug-reports.md](bug-reports.md).

## Failed Test Cases

| Test case | Defect |
|---|---|
| TC-07 Product images render correctly | BUG-01 |
| TC-10 Sort applies for problem user | BUG-02 |
| TC-15 Add to cart for error user | BUG-04 |
| TC-16 Reset App State clears the cart | BUG-07 |

Two further defects were found while executing TC-17/TC-18 with the `error_user` account (BUG-05, BUG-06); the same cases pass with `standard_user`. BUG-03 was found during exploratory testing of the navigation menu.

## Defect Summary

| Severity | Count | Defects |
|---|---|---|
| Critical | 2 | BUG-04, BUG-06 |
| Major | 3 | BUG-01, BUG-02, BUG-05 |
| Minor | 2 | BUG-03, BUG-07 |

## Key Findings

- The application is **fully functional for the `standard_user` account**: login, browsing, sorting, cart management, and a complete checkout with correct price calculation (item total $53.97 + tax $4.32 = $58.29) all pass.
- The `error_user` account **cannot complete a purchase**: half of the catalog cannot be added to the cart (BUG-04), the Last Name field is broken and its validation is bypassed (BUG-05), and the Finish button is unresponsive (BUG-06). For a real store these are release-blocking.
- The `problem_user` account has **Major catalog presentation defects**: wrong images on every product (BUG-01) and non-working price sorting (BUG-02).
- The `locked_out_user` is correctly rejected at login with a clear error message.

## Performance Observation (out of scope, noted for awareness)

Login with `performance_glitch_user` took approximately **5.4 seconds** from clicking Login to the inventory page rendering, compared to roughly 1-2 seconds for `standard_user` on the same connection. No full performance testing was performed.

## Recommendations

1. Fix BUG-04 and BUG-06 before any release: they block the purchase flow for affected users.
2. Fix BUG-05 together with them: broken field validation lets incomplete orders through.
3. Correct the image mapping for BUG-01 and the sorting handler for BUG-02.
4. Repoint the About link (BUG-03) and revert button states on Reset App State (BUG-07) in a normal maintenance cycle.
5. Re-run the failed test cases after fixes, then a full regression pass across all accounts.

## Conclusion

The core purchase flow works for a normal user, and all authentication validations behave as specified. However, the defects concentrated in the `error_user` and `problem_user` accounts would block or seriously degrade purchases for any real user hitting them. In their current state, those code paths are **not fit for release**.
