# Bug Reports — Swag Labs

Defects found during test execution on 24 November 2026.
Environment: Chrome, https://www.saucedemo.com. Password for all accounts: `secret_sauce`.

---

## BUG-01: All product images show the same wrong image (problem_user)

| | |
|---|---|
| Severity | Major |
| Priority | High |
| Account | `problem_user` |
| Found in | TC-07 |
| Status | Open |

**Description:** On the inventory page, all 6 products display the same placeholder image (a dog photo) instead of each product's own image. The image file served for every product is the same (`sl-404` image). Product names, descriptions, and prices are correct.

**Steps to reproduce:**
1. Log in as `problem_user`.
2. Open the inventory page.
3. Observe the product images.

**Expected:** Each product shows its own correct image, as it does for `standard_user`.
**Actual:** Every product shows the same incorrect image.

**Evidence:** ![BUG-01: all products show the same wrong image](https://github.com/user-attachments/assets/05db1984-2d7f-46eb-819c-74a7d20fff93)

---

## BUG-02: Sorting by price does not apply (problem_user)

| | |
|---|---|
| Severity | Major |
| Priority | Medium |
| Account | `problem_user` |
| Found in | TC-10 |
| Status | Open |

**Description:** Selecting "Price (low to high)" in the sort dropdown has no effect. The product order stays "Name (A to Z)" and the dropdown reverts to the previous selection. The same steps work correctly for `standard_user` (prices reorder to $7.99, $9.99, $15.99, $15.99, $29.99, $49.99).

**Steps to reproduce:**
1. Log in as `problem_user`.
2. On the inventory page, select "Price (low to high)" in the sort dropdown.
3. Observe the product order.

**Expected:** Products reorder by ascending price.
**Actual:** Order does not change; the first product remains Sauce Labs Backpack at $29.99.

---

## BUG-03: "About" menu link leads to a 404 page

| | |
|---|---|
| Severity | Minor |
| Priority | Low |
| Account | All |
| Found in | Exploratory testing |
| Status | Open |

**Description:** The "About" link in the side menu points to `https://saucelabs.com/error/404`, which renders a page with the title "Not Found".

**Steps to reproduce:**
1. Log in with any account.
2. Open the side menu.
3. Click "About".

**Expected:** The About page of the application or company loads.
**Actual:** A "Not Found" (404) page loads.

---

## BUG-04: Half of the products cannot be added to the cart (error_user)

| | |
|---|---|
| Severity | Critical |
| Priority | High |
| Account | `error_user` |
| Found in | TC-15 |
| Status | Open |

**Description:** Clicking "Add to cart" does nothing for 3 of the 6 products: Sauce Labs Bolt T-Shirt, Sauce Labs Fleece Jacket, and Test.allTheThings() T-Shirt (Red). The button does not change to "Remove" and the cart badge does not increase. The other 3 products (Backpack, Bike Light, Onesie) add normally.

**Steps to reproduce:**
1. Log in as `error_user`.
2. On the inventory page, click "Add to cart" on Sauce Labs Bolt T-Shirt.
3. Observe the button and the cart badge.
4. Repeat for each remaining product.

**Expected:** Every product can be added to the cart and the badge count matches the number of added products.
**Actual:** 3 products cannot be added at all. A user on this account cannot buy half of the catalog.

---

## BUG-05: Last Name field does not accept input, and checkout proceeds without it (error_user)

| | |
|---|---|
| Severity | Major |
| Priority | High |
| Account | `error_user` |
| Found in | TC-17 / TC-18 execution with `error_user` |
| Status | Open |

**Description:** On the checkout information form, the Last Name field does not accept input: after typing, the field reads back empty. Pressing Continue with Last Name empty does not trigger the "Last Name is required" validation error. The form advances to the order overview with no last name on record. For `standard_user`, the same field works and empty-field validation fires correctly ("First Name is required" was verified for the First Name field).

**Steps to reproduce:**
1. Log in as `error_user` and add any product to the cart.
2. Open the cart and click Checkout.
3. Type any text into the Last Name field.
4. Fill First Name and Zip/Postal Code, then click Continue.

**Expected:** Last Name accepts the typed text; if it were left empty, the form would reject the submission with "Last Name is required".
**Actual:** The field stays empty after typing, and the form proceeds to the overview page anyway.

**Evidence:** ![BUG-05: checkout overview reached with an empty Last Name](https://github.com/user-attachments/assets/5043b2c7-0366-4601-89ca-e405f0ba0a4b)

---

## BUG-06: Finish button unresponsive; order cannot be completed (error_user)

| | |
|---|---|
| Severity | Critical |
| Priority | High |
| Account | `error_user` |
| Found in | TC-17 execution with `error_user` |
| Status | Open |

**Description:** On the checkout overview page, clicking the Finish button has no effect. The page stays on `checkout-step-two.html` and the order confirmation never appears. Repeated clicks behave the same. The full checkout flow works correctly for `standard_user` (see TC-17 evidence).

**Steps to reproduce:**
1. Log in as `error_user` and add a product to the cart.
2. Complete the checkout information form and click Continue.
3. On the overview page, click Finish.

**Expected:** The order completes and the "Thank you for your order!" confirmation appears.
**Actual:** Nothing happens. The user cannot complete a purchase.

**Evidence:** ![BUG-06: Finish button unresponsive on the overview page](https://github.com/user-attachments/assets/13fee720-cc55-46ce-b007-a5fed4d3cd48)

---

## BUG-07: Reset App State clears the cart but not the button states

| | |
|---|---|
| Severity | Minor |
| Priority | Low |
| Account | `standard_user` |
| Found in | TC-16 |
| Status | Open |

**Description:** After using "Reset App State" from the side menu, the cart badge is cleared, but the button of a product that was in the cart still shows "Remove" instead of reverting to "Add to cart". The button state only corrects after a page reload.

**Steps to reproduce:**
1. Log in as `standard_user` and add a product to the cart.
2. Open the side menu and click Reset App State.
3. Observe the product button on the inventory page.

**Expected:** The badge clears and all product buttons return to "Add to cart".
**Actual:** The badge clears, but the affected product's button still shows "Remove".
