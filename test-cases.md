# Test Cases — Swag Labs

Environment: Chrome, https://www.saucedemo.com. Password for all accounts: `secret_sauce`.
Result column: filled after execution. See [bug-reports.md](bug-reports.md) for failures.

## Authentication

| ID | Title | Preconditions | Steps | Expected Result | Priority | Result |
|---|---|---|---|---|---|---|
| TC-01 | Login with valid credentials | On login page | 1. Enter `standard_user` 2. Enter password 3. Click Login | User lands on the inventory page showing 6 products | High | Pass |
| TC-02 | Login with locked out user | On login page | 1. Enter `locked_out_user` 2. Enter password 3. Click Login | Login is rejected with the error "Sorry, this user has been locked out." | High | Pass |
| TC-03 | Login with invalid password | On login page | 1. Enter `standard_user` 2. Enter a wrong password 3. Click Login | Login is rejected with an error that credentials do not match any user | Medium | Pass |
| TC-04 | Login with empty fields | On login page | 1. Leave username and password empty 2. Click Login | Login is rejected with the error "Username is required" | Medium | Pass |
| TC-05 | Logout | Logged in as `standard_user` | 1. Open the menu 2. Click Logout | User returns to the login page and the session is cleared | High | Pass |

## Inventory

| ID | Title | Preconditions | Steps | Expected Result | Priority | Result |
|---|---|---|---|---|---|---|
| TC-06 | All products are listed | Logged in as `standard_user` | 1. Open the inventory page | 6 products are displayed, each with an image, name, description, price, and Add to Cart button | High | Pass |
| TC-07 | Product images render correctly | Logged in as `problem_user` | 1. Open the inventory page 2. Inspect product images | Each product shows its own correct image | Medium | Fail (BUG-01) |
| TC-08 | Sort products by price (low to high) | Logged in as `standard_user` | 1. Select "Price (low to high)" in the sort dropdown | Products reorder by ascending price: $7.99, $9.99, $15.99, $15.99, $29.99, $49.99 | Medium | Pass |
| TC-09 | Sort products by name (Z to A) | Logged in as `standard_user` | 1. Select "Name (Z to A)" in the sort dropdown | Products reorder in reverse alphabetical order | Medium | Pass |
| TC-10 | Sort applies for problem user | Logged in as `problem_user` | 1. Select "Price (low to high)" in the sort dropdown | Products reorder by ascending price | Medium | Fail (BUG-02) |
| TC-11 | Open product detail page | Logged in as `standard_user` | 1. Click a product name | The product detail page shows the correct product name, description, image, and price | Medium | Pass |

## Cart

| ID | Title | Preconditions | Steps | Expected Result | Priority | Result |
|---|---|---|---|---|---|---|
| TC-12 | Add a product to the cart | Logged in as `standard_user`, on inventory | 1. Click Add to Cart on "Sauce Labs Backpack" | Cart badge shows 1, button changes to Remove, product appears on the cart page | High | Pass |
| TC-13 | Add multiple products to the cart | Logged in as `standard_user` | 1. Add 3 different products to the cart | Cart badge shows 3 and all 3 products appear on the cart page with correct names and prices | High | Pass |
| TC-14 | Remove a product from the cart | Product already in cart | 1. Click Remove on the product | Product is removed, badge count decreases, button changes back to Add to Cart | High | Pass |
| TC-15 | Add to cart for error user | Logged in as `error_user` | 1. Click Add to Cart on each product, one at a time | Every product can be added and the badge count matches | High | Fail (BUG-04) |
| TC-16 | Reset App State clears the cart | Cart contains items | 1. Open the menu 2. Click Reset App State | Cart badge is cleared and products return to Add to Cart state | Low | Fail (BUG-07) |

## Checkout

| ID | Title | Preconditions | Steps | Expected Result | Priority | Result |
|---|---|---|---|---|---|---|
| TC-17 | Complete a full checkout | 1 item in cart | 1. Open cart 2. Click Checkout 3. Enter first name, last name, postal code 4. Continue 5. Finish | Order completes with the "Thank you for your order!" confirmation | High | Pass with standard_user ([screenshot](https://github.com/user-attachments/assets/1d458cf3-e52e-4151-8f3f-9866395c2a43)); fails with error_user (BUG-05, BUG-06) |
| TC-18 | Checkout with empty first name | 1 item in cart, on checkout form | 1. Leave First Name empty 2. Fill last name and postal code 3. Click Continue | Submission is rejected with the error "First Name is required" | High | Pass with standard_user; see BUG-05 for error_user |
| TC-19 | Checkout overview shows correct totals | 2 items in cart | 1. Complete the information form 2. On the overview page check Item total, Tax, and Total | Item total equals the sum of item prices; Total equals item total plus tax | Medium | Pass |
| TC-20 | Cancel checkout returns to cart | 1 item in cart, on checkout form | 1. Click Cancel | User returns to the cart page and cart contents are unchanged | Low | Pass |
