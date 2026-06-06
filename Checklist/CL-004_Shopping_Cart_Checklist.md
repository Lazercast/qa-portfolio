# CL-004 — Shopping Cart Checklist

---

## Checklist Details

| Field            | Details                                      |
|------------------|----------------------------------------------|
| **Checklist ID** | CL-004                                       |
| **Title**        | Shopping Cart — Manual Testing Checklist     |
| **Module**       | E-Commerce — Shopping Cart                   |
| **Testing Types**| Functional, Validation, UI, Usability        |
| **Priority**     | High                                         |
| **Prepared By**  | QA Engineer                                  |
| **Date**         | 2025-06-02                                   |
| **Environment**  | Chrome 124 / Windows 11 / 1920×1080          |
| **App URL**      | `https://demo.shopeasy.io/cart`              |

---

## Preconditions

- User is logged in with a registered account.
- At least one product is available in the catalogue.
- Browser cache is cleared before starting.

---

## 1. Adding Items to the Cart

- [ ] Clicking **"Add to Cart"** on a product page adds the item to the cart.
- [ ] A **success notification** (toast or banner) appears after adding an item.
- [ ] The **cart icon badge** in the navigation updates immediately to reflect the new item count.
- [ ] Adding the **same product twice** increases the quantity to 2 (not duplicates the line item).
- [ ] Adding items from **multiple product categories** adds all items correctly.
- [ ] Adding a product with **variants** (e.g., size, colour) adds the correct selected variant.
- [ ] The **"Add to Cart"** button shows a loading state while the request is processing.

---

## 2. Cart Page — Layout & Load

- [ ] The cart page (`/cart`) loads within 3 seconds.
- [ ] Each cart item displays: **product image**, **product name**, **variant info** (if applicable), **unit price**, **quantity selector**, **line total**, and a **remove button**.
- [ ] The **cart subtotal**, **estimated tax** (if shown), and **order total** are displayed clearly.
- [ ] A **"Proceed to Checkout"** button is present and visible.
- [ ] A **"Continue Shopping"** link is present.
- [ ] An **empty cart message** is shown when no items are in the cart (e.g., *"Your cart is empty."*).
- [ ] The **"Proceed to Checkout"** button is **disabled or hidden** when the cart is empty.

---

## 3. Quantity Management

- [ ] Increasing the quantity using the **"+"** button updates the quantity and recalculates the line total.
- [ ] Decreasing the quantity using the **"–"** button updates the quantity and recalculates the line total.
- [ ] Setting quantity to **0** via the input field removes the item or shows a remove confirmation.
- [ ] Setting quantity to **1** (minimum) disables the **"–"** button or shows a minimum quantity warning.
- [ ] Entering a **negative number** in the quantity field is rejected.
- [ ] Entering **letters** in the quantity field is rejected.
- [ ] Entering an **extremely large number** (e.g., 99999) is either capped or an appropriate error is shown.
- [ ] The **order total** updates correctly after every quantity change.

---

## 4. Removing Items

- [ ] Clicking the **Remove** button on an item removes it from the cart.
- [ ] The **cart badge count** updates after removal.
- [ ] The **subtotal and order total** recalculate after item removal.
- [ ] Removing the **last item** shows the empty cart state.
- [ ] A **confirmation prompt** appears before removing an item (if applicable to the design).

---

## 5. Price Calculation Accuracy

- [ ] Line total = unit price × quantity (verified manually for each item).
- [ ] Subtotal = sum of all line totals.
- [ ] Applying a **discount code / coupon** (if supported) reduces the total by the correct amount.
- [ ] An **invalid coupon code** shows an appropriate error.
- [ ] Tax and shipping estimates (if shown) are clearly separated from the subtotal.
- [ ] The total displayed in the cart **matches** the total shown at checkout.

---

## 6. Cart Persistence

- [ ] Cart items **persist after logging out and back in** (server-side cart).
- [ ] Cart items **persist after closing and reopening the browser** (for logged-in users).
- [ ] Cart items **persist after navigating away** to a product page and returning.
- [ ] Guest cart items are **merged** with the user's account cart upon login (if guest cart is supported).

---

## 7. UI & Styling Checks

- [ ] All product images in the cart are loaded correctly (no broken image icons).
- [ ] Product names in the cart are clickable and link to the correct product page.
- [ ] Quantity input fields are correctly sized and aligned.
- [ ] The **"Proceed to Checkout"** button is prominently styled and easily identifiable.
- [ ] Error messages (e.g., invalid quantity) are visible and clearly worded.
- [ ] The cart layout is not broken on standard desktop widths (1280px, 1440px, 1920px).

---

## 8. Usability Checks

- [ ] The cart is accessible from any page via the **cart icon** in the navigation.
- [ ] The cart page or drawer opens within **1 second** of clicking the icon.
- [ ] Users can easily distinguish between individual line items.
- [ ] The tab order on the cart page is logical (quantity → remove → checkout).

---

## Summary

| Category              | Total Items | Checked | Passed | Failed | Skipped |
|-----------------------|-------------|---------|--------|--------|---------|
| Adding Items          | 7           |         |        |        |         |
| Page Layout & Load    | 7           |         |        |        |         |
| Quantity Management   | 8           |         |        |        |         |
| Removing Items        | 5           |         |        |        |         |
| Price Calculation     | 6           |         |        |        |         |
| Cart Persistence      | 4           |         |        |        |         |
| UI & Styling          | 6           |         |        |        |         |
| Usability             | 4           |         |        |        |         |
| **Total**             | **47**      |         |        |        |         |

---

## Notes & Observations

> *(Record any defects found, environment-specific issues, or additional observations here.)*

---

*Checklist version 1.0 — ShopEasy Demo Application*
