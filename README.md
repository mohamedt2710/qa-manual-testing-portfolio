# QA Manual Testing Portfolio

Manual testing project for the [Swag Labs](https://www.saucedemo.com) demo e-commerce application.

This repository documents a full manual testing cycle: test planning, test case design, execution, defect reporting, and summary reporting. It was created as a hands-on practice project to demonstrate junior QA skills.

## Application Under Test

**Swag Labs** (saucedemo.com) is a public demo e-commerce web application built for testing practice. It provides several test user accounts, each with different behaviors:

| Username | Behavior |
|---|---|
| `standard_user` | Normal, defect-free user |
| `locked_out_user` | Blocked at login |
| `problem_user` | UI and functional defects |
| `performance_glitch_user` | Slow performance |
| `error_user` | Functional defects |
| `visual_user` | Visual/layout defects |

Password for all accounts: `secret_sauce`

## Repository Contents

| File | Description |
|---|---|
| [test-plan.md](test-plan.md) | Test plan: scope, approach, criteria, risks |
| [test-cases.md](test-cases.md) | 20 test cases covering login, inventory, cart, checkout, and navigation |
| [bug-reports.md](bug-reports.md) | Defects found during execution, with severity, priority, and reproduction steps |
| [test-summary-report.md](test-summary-report.md) | Execution results and quality assessment |
| Screenshots | Captured during execution and embedded in [bug-reports.md](bug-reports.md) |

## Approach

1. Exploratory testing of the application with the `standard_user` account to learn expected behavior.
2. Test case design based on the observed flows and requirements inferred from the application.
3. Structured execution across all test accounts.
4. Defect reporting for every deviation from expected behavior, with evidence.

## Tools

- Browser: Google Chrome
- Documentation: Markdown
- Defect and evidence capture: manual
