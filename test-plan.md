# Test Plan — Swag Labs (saucedemo.com)

| | |
|---|---|
| Project | Swag Labs manual testing |
| Version | 1.0 |
| Date | November 2026 |
| Author | Mohamed Tantawy |

## 1. Objective

Verify the core user flows of the Swag Labs demo e-commerce application: authentication, product browsing, cart management, and checkout. Identify and document defects that affect these flows.

## 2. Scope

### In scope
- Login and logout (all provided test accounts)
- Product inventory page (listing, images, sorting)
- Product detail page
- Cart (add, remove, badge count, contents)
- Checkout (information form, overview, confirmation)
- Navigation (menu, reset app state, links)

### Out of scope
- Performance/load testing (observations only)
- Security testing
- Mobile/responsive testing
- Cross-browser testing beyond Chrome
- Backend/API testing

## 3. Test Approach

- **Functional testing** against the test cases in [test-cases.md](test-cases.md).
- **Exploratory testing** using the different test accounts, which are documented to contain seeded defects.
- **Boundary and negative testing** on the checkout form fields.
- Each test case is executed with `standard_user` first to establish the expected baseline, then repeated with defect-seeded accounts where relevant.

## 4. Test Environment

| Item | Value |
|---|---|
| Application URL | https://www.saucedemo.com |
| Browser | Google Chrome (latest) |
| OS | Windows / Linux desktop |
| Test accounts | standard_user, locked_out_user, problem_user, performance_glitch_user, error_user, visual_user |
| Password | secret_sauce |

## 5. Entry Criteria

- Application is reachable and the login page loads.
- Test accounts and credentials are available.
- Test cases are written and reviewed.

## 6. Exit Criteria

- All 20 planned test cases executed.
- All defects found are reported with reproduction steps and evidence.
- Test summary report is completed.

## 7. Deliverables

- Test plan (this document)
- Test cases
- Bug reports with screenshots
- Test summary report

## 8. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Demo app behavior changes without notice | Test cases may fail for environment reasons | Re-baseline against standard_user before reporting a defect |
| Seeded defects overlap between accounts | Defect attribution may be unclear | Record the exact account used per test run |
| Shared public app state | Cart/session state may differ between runs | Reset App State before each run |

## 9. Defect Severity and Priority Definitions

| Severity | Meaning |
|---|---|
| Critical | Core flow is blocked; no workaround |
| Major | Core flow works but with significant defects or a difficult workaround |
| Minor | Small functional or cosmetic issue; flow works |
| Trivial | Cosmetic issue with no functional impact |

| Priority | Meaning |
|---|---|
| High | Fix before release |
| Medium | Fix in the current cycle |
| Low | Fix when convenient |
