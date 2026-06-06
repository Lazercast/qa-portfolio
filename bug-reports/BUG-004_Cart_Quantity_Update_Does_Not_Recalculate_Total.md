# BUG-004 — Shopping Cart Quantity Update Does Not Reflect New Total Price

---

## Summary

When a logged-in user changes the quantity of an item in the shopping cart, the item count updates visually in the quantity input field, but the **line item total** and **order total** prices are **not recalculated**. The stale prices persist until the page is manually refreshed, at which point incorrect totals may be sent to the checkout flow.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-004                          |
| **Title**        | Cart quantity change does not update item or order total price |
| **Type**         | Functional                       |
| **Severity**     | High                             |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-02                       |
| **Assigned To**  | Frontend Team                    |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/cart`  |
| **Browser**      | Chrome 124.0, Firefox 126.0, Edge 124.0 |
| **OS**           | Windows 11 Pro / macOS Ventura 13.6 |
| **Resolution**   | 1920×1080                        |
| **Account State**| Logged in as registered user     |

---

## Preconditions

- User is logged in to a registered account.
- At least one product has been added to the shopping cart.
- The cart page (`/cart`) loads successfully and displays the item(s).

---

## Steps to Reproduce

1. Log in to `https://demo.shopeasy.io` with valid credentials.
2. Browse to any product page and add a product (e.g., **"Wireless Headphones — $49.99"**) to the cart with quantity **1**.
3. Navigate to the cart page: `https://demo.shopeasy.io/cart`.
4. Confirm the displayed values:
   - **Quantity:** 1
   - **Line Total:** $49.99
   - **Order Total:** $49.99
5. Click the **"+"** button or manually type `3` into the quantity input field for the item.
6. Click the **"Update Cart"** button (or press Enter / Tab away from the field).
7. Observe the **Line Total** and **Order Total** values.

---

## Expected Result

After updating the quantity to **3**, the displayed prices should update immediately:

- **Line Total:** $149.97 (3 × $49.99)
- **Order Total:** $149.97 (plus applicable taxes/shipping)

---

## Actual Result

After updating the quantity to **3**:

- The quantity input field correctly shows **3**.
- The **Line Total** still displays **$49.99** (unchanged from quantity 1).
- The **Order Total** still displays **$49.99** (unchanged).

The prices only refresh after a **full page reload** (F5). Even after reload, the URL-based cart state sometimes reverts to the previous quantity.

---

## Impact Assessment

This is a significant functional bug with potential financial implications:

- A user could proceed to checkout with a quantity of 3 items but be charged for only 1.
- Alternatively, if the server-side total is correct but the UI shows an incorrect lower amount, the user may be surprised by the actual charge at payment.
- Affects **all browsers** tested — this is not a browser-specific issue.

---

## Additional Information

- The cart API endpoint (`PATCH /api/v1/cart/items/{id}`) appears to accept the quantity update correctly (returns `200 OK` with updated quantity in the response body). The bug appears to be a **frontend rendering issue** — the UI is not consuming the updated API response to re-render prices.
- Tested with multiple product types (single item, items with variants) — the issue reproduces consistently.

**API Response (correct):**
```json
{
  "item_id": "prod_xyz789",
  "quantity": 3,
  "unit_price": 49.99,
  "line_total": 149.97
}
```
Despite the correct API response, the frontend does not update the displayed `line_total`.

---

## Attachments

- `screenshot_cart_before_update.png` — Cart showing quantity 1, total $49.99
- `screenshot_cart_after_update.png` — Cart showing quantity 3, total still $49.99 (bug)
- `network_tab_patch_response.png` — DevTools Network tab showing correct API response

---

## Suggested Fix

The frontend cart component should listen for the API response to the `PATCH /api/v1/cart/items/{id}` call and update the `line_total` and `order_total` state values accordingly. Currently it appears only the quantity input field state is updated after the API call, while price fields remain bound to their initial render values.
