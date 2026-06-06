# BUG-008 — "Proceed to Checkout" Button Remains Enabled on Empty Cart Page

---

## Summary

The **"Proceed to Checkout"** button on the shopping cart page remains visible and clickable when the cart contains **zero items**. Clicking the button initiates the checkout flow and loads the checkout page with a $0.00 order total, which allows users to submit a "checkout" with no items — causing a broken order to be created in the system.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-008                          |
| **Title**        | Checkout button enabled and functional on empty cart |
| **Type**         | UI / Functional / Validation     |
| **Severity**     | Medium                           |
| **Priority**     | Medium                           |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-04                       |
| **Assigned To**  | Frontend Team                    |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/cart`  |
| **Browser**      | Chrome 124.0, Firefox 126.0     |
| **OS**           | Windows 11 Pro                   |
| **Resolution**   | 1920×1080                        |
| **Account State**| Logged in as registered user     |

---

## Preconditions

- User is logged in with a registered account.
- The shopping cart is currently **empty** (either was never populated, or all items have been removed).
- Cart page (`/cart`) is accessible and loads the "Your cart is empty" state.

---

## Steps to Reproduce

**Scenario A — Remove all items:**

1. Log in to `https://demo.shopeasy.io`.
2. Add any product to the cart.
3. Navigate to `https://demo.shopeasy.io/cart`.
4. Click the **"Remove"** or **"Delete"** icon next to the item.
5. Confirm the cart now shows the "Your cart is empty" message.
6. Observe the **"Proceed to Checkout"** button — note it is still visible.
7. Click the **"Proceed to Checkout"** button.
8. Observe what happens.

**Scenario B — Direct navigation with empty cart:**

1. Log in with a fresh account (no items ever added).
2. Navigate directly to `https://demo.shopeasy.io/cart`.
3. Click the **"Proceed to Checkout"** button.

---

## Expected Result

When the cart is empty:

- The **"Proceed to Checkout"** button should be **disabled** (grayed out, non-clickable) or **hidden entirely**.
- A friendly message should be displayed: *"Your cart is empty. [Continue Shopping →]"*
- Clicking a disabled button (if still visible) should produce no action.

---

## Actual Result

- The **"Proceed to Checkout"** button remains fully **enabled and styled as active**.
- Clicking it navigates the user to the checkout page (`/checkout`).
- The checkout page loads with:
  - **Order Summary:** "0 items"
  - **Subtotal:** $0.00
  - **Total:** $0.00
- The user can fill in shipping details and click **"Place Order"** on the $0.00 checkout — this creates a real order record in the system with 0 items and $0.00 value.

---

## Additional Information

- An empty-cart order being created in the database creates orphaned order records that may interfere with reporting, inventory management, and order processing workflows.
- The $0.00 order also bypasses payment validation since no payment is required for a zero-value order.
- This reproduces across all tested browsers — the button state is not conditionally rendered.
- **Related UI note:** The cart item count badge in the header correctly shows `0` when the cart is empty, suggesting the cart state is tracked correctly in some parts of the UI but not applied to the checkout button's disabled state.

---

## Attachments

- `screenshot_empty_cart_button_enabled.png` — Empty cart page with active Proceed to Checkout button
- `screenshot_checkout_0_items.png` — Checkout page showing 0 items, $0.00 total
- `screenshot_order_created_0_value.png` — Order confirmation page for a $0.00 order

---

## Suggested Fix

The cart page component should evaluate the cart item count when rendering. If `cart.itemCount === 0`:

1. Either **hide** the checkout button and show a "Continue Shopping" CTA instead.
2. Or **disable** the button (add `disabled` attribute and apply appropriate styling) with a tooltip: *"Add items to your cart to proceed."*

Additionally, the checkout API endpoint (`POST /api/v1/orders`) should validate server-side that the cart contains at least one item before creating an order record.
