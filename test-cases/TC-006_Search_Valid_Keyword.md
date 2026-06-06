# TC-006 — Product Search Returns Relevant Results for a Valid Keyword

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-006                                       |
| **Title**          | Product search with a valid keyword returns relevant, correctly displayed results |
| **Module**         | Search Functionality                         |
| **Type**           | Positive                                     |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-02                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- Application is accessible at `https://demo.shopeasy.io`.
- The product catalogue contains at least one product matching the search keyword.
- The user may be logged in or browsing as a guest (search is available to both).

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io` | Homepage loads successfully |
| 2 | Locate the search bar in the top navigation | Search bar is visible and accepts input |
| 3 | Click inside the search input field | Field receives focus; cursor appears |
| 4 | Type `headphones` into the search field | Text appears in the field as typed; autocomplete suggestions may appear |
| 5 | Press **Enter** or click the **Search** icon | Search is triggered; page navigates to search results |
| 6 | Observe the search results page URL | URL reflects the search query (e.g., `/search?q=headphones`) |
| 7 | Observe the search results | Product cards are displayed |
| 8 | Verify each result card contains required elements | Product image, name, price, and "Add to Cart" button visible on each card |
| 9 | Verify the results are relevant to the query | All displayed products are related to "headphones" |
| 10 | Note the results count displayed | A count such as *"Showing 12 results for 'headphones'"* is visible |

---

## Test Data

| Field          | Value          |
|----------------|----------------|
| Search Keyword | `headphones`   |
| Min Expected Results | ≥ 1 result |

---

## Expected Result

- The search results page loads within **3 seconds**.
- The page title or heading shows: *"Results for 'headphones'"* or similar.
- The result count is displayed (e.g., *"12 products found"*).
- Each product card displays:
  - Product image (not broken)
  - Product name (containing or related to "headphones")
  - Price formatted correctly (e.g., `$49.99`)
  - An **"Add to Cart"** button
- Results are **relevant** — no completely unrelated products appear.
- Pagination controls are visible if the result count exceeds the per-page limit.

---

## Actual Result

> ✅ **Pass** — Search results page loaded in 1.8 seconds. Displayed *"14 results for 'headphones'"*. All 14 product cards showed images, names, prices, and Add to Cart buttons. All results were headphone-related products. Pagination appeared after result 12 (2 pages total).

---

## Results Spot-Check

| Product Name                      | Price   | Image | Add to Cart |
|-----------------------------------|---------|-------|-------------|
| Wireless Bluetooth Headphones     | $49.99  | ✅    | ✅          |
| Noise-Cancelling Over-Ear Headphones | $129.00 | ✅  | ✅          |
| Gaming Headset Pro                | $79.99  | ✅    | ✅          |

---

## Notes

- Also tested with **mixed case** (`Headphones`, `HEADPHONES`) — search is case-insensitive, results identical.
- Tested with a **partial keyword** (`head`) — returned headphones plus other "head" products (correct behaviour for partial matching).
- Tested with **extra leading/trailing spaces** (` headphones `) — spaces were trimmed and search returned normal results.
