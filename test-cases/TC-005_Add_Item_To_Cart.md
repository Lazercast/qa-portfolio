# TC-005 — Add a Single Product to the Shopping Cart and Verify Total

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-005                                       |
| **Title**          | Add a single product to the cart and verify item count and total price |
| **Module**         | Shopping Cart                                |
| **Type**           | Positive                                     |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-02                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- User is logged in with a registered account.
- The shopping cart is **empty** before the test begins (verified by checking the cart badge shows `0`).
- The product listed in Test Data is in stock and visible on its product page.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Navigate to the product page for "Wireless Bluetooth Headphones" | Product page loads; price is visible as $49.99; "Add to Cart" button is enabled |
| 2 | Verify the current cart badge count in the navigation | Cart badge shows `0` |
| 3 | Click the **Add to Cart** button | A success notification appears; button state may change to "Added ✓" |
| 4 | Observe the cart badge in the top navigation | Badge updates to `1` |
| 5 | Click the cart icon in the navigation to open the cart | Cart page or drawer opens |
| 6 | Verify the product appears in the cart | Product name, image, quantity (1), and unit price ($49.99) are displayed |
| 7 | Verify the cart subtotal | Subtotal displays $49.99 |
| 8 | Verify the cart item count | Cart shows 1 item |

---

## Test Data

| Field          | Value                           |
|----------------|---------------------------------|
| Product Name   | Wireless Bluetooth Headphones   |
| Product Price  | $49.99                          |
| Quantity       | 1 (default)                     |
| Expected Total | $49.99                          |
| User Account   | `testuser@example.com`          |

---

## Expected Result

- The product is added to the cart successfully.
- A success **toast notification** or confirmation message appears briefly: *"Wireless Bluetooth Headphones added to your cart."*
- The **cart badge** in the header updates from `0` to `1` without requiring a page refresh.
- The cart page/drawer displays:
  - Product name: *Wireless Bluetooth Headphones*
  - Product image: correct thumbnail
  - Quantity: `1`
  - Unit price: `$49.99`
  - Line total: `$49.99`
  - Subtotal: `$49.99`
- The **"Proceed to Checkout"** button is visible and enabled.

---

## Actual Result

> ✅ **Pass** — Product added successfully. Toast notification appeared and disappeared after 3 seconds. Cart badge updated to `1` immediately. Cart page showed correct product name, image, price ($49.99), and subtotal ($49.99). Checkout button visible and enabled.

---

## Price Calculation Verification

| Item                          | Qty | Unit Price | Line Total |
|-------------------------------|-----|------------|------------|
| Wireless Bluetooth Headphones | 1   | $49.99     | $49.99     |
| **Cart Subtotal**             |     |            | **$49.99** |

---

## Notes

- Tested by adding the same product twice — cart updated to quantity `2` with a subtotal of `$99.98` (correct).
- Verified the cart persists after logging out and back in (cart state is saved server-side, not just in localStorage).
