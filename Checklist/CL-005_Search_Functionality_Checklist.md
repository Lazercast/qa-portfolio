# CL-005 — Search Functionality Checklist

---

## Checklist Details

| Field            | Details                                      |
|------------------|----------------------------------------------|
| **Checklist ID** | CL-005                                       |
| **Title**        | Search Functionality — Manual Testing Checklist |
| **Module**       | Search                                       |
| **Testing Types**| Functional, Validation, UI, Usability        |
| **Priority**     | High                                         |
| **Prepared By**  | QA Engineer                                  |
| **Date**         | 2025-06-03                                   |
| **Environment**  | Chrome 124 / Windows 11 / 1920×1080          |
| **App URL**      | `https://demo.shopeasy.io`                   |

---

## Preconditions

- Application is accessible and the homepage loads correctly.
- The search bar is visible in the top navigation.
- The product catalogue contains items for expected search terms.

---

## 1. Search Bar — Layout & Availability

- [ ] The search bar is visible on the homepage and all main catalogue pages.
- [ ] The search input field has a visible placeholder text (e.g., *"Search for products..."*).
- [ ] A **Search icon** or **Submit button** is present next to the input field.
- [ ] The search bar is focusable via mouse click and **Tab** key navigation.
- [ ] The search bar is present in the same location on all pages (consistent placement).

---

## 2. Functional Testing — Positive Scenarios

- [ ] Typing a **valid product name** (e.g., `headphones`) and pressing Enter returns relevant results.
- [ ] Clicking the **Search icon/button** after typing also triggers a search.
- [ ] Search is **case-insensitive** — `Headphones`, `HEADPHONES`, and `headphones` return identical results.
- [ ] A **partial keyword** (e.g., `head`) returns products containing that string.
- [ ] Search with **leading or trailing spaces** (e.g., ` headphones `) returns results as if trimmed.
- [ ] The results page URL contains the search query (e.g., `/search?q=headphones`).
- [ ] The results page displays a **result count** (e.g., *"14 results for 'headphones'"*).
- [ ] Each result card displays: **product image**, **product name**, **price**, and an **"Add to Cart"** button.
- [ ] Clicking a **product card** in the results navigates to the correct product detail page.

---

## 3. Functional Testing — Negative Scenarios

- [ ] Searching for a **non-existent term** (e.g., `xyznotaproduct123`) shows a *"No results found"* message.
- [ ] The *"No results found"* state offers a helpful suggestion (e.g., *"Try a different keyword"* or links to categories).
- [ ] Submitting an **empty search** (pressing Enter with no input) does not crash the page.
- [ ] Searching with only **spaces** is treated as empty and shows an appropriate message or all results.

---

## 4. Input Validation — Edge Cases

- [ ] **Special characters** (`!@#$%^&*()`) — no server error; *"No results"* or sanitised results shown.
- [ ] **XSS attempt** (`<script>alert('xss')</script>`) — script is **not** executed; shown as plain text or sanitised.
- [ ] **SQL injection** (`' OR '1'='1`) — no data exposure or server error; *"No results"* shown.
- [ ] **Very long input** (100+ characters) — no crash; results shown or input gracefully truncated.
- [ ] **Emoji input** (e.g., `🎧`) — no crash; *"No results"* or relevant results shown.
- [ ] Special characters in search query are **percent-encoded** in the URL (e.g., `%26`, `%3C`).

---

## 5. Autocomplete / Search Suggestions (if applicable)

- [ ] Typing 2+ characters shows an autocomplete **dropdown of suggestions**.
- [ ] Suggestions are **relevant** to the entered text.
- [ ] Clicking a suggestion populates the search field and triggers a search.
- [ ] Pressing **Escape** closes the autocomplete dropdown.
- [ ] Arrow keys can **navigate** through the autocomplete suggestions.
- [ ] The dropdown **closes** when the user clicks outside of it.

---

## 6. Results Page — Filtering & Sorting

- [ ] Filter options are displayed (e.g., by category, price range, rating).
- [ ] Applying a filter updates the results correctly.
- [ ] Removing a filter restores the full result set.
- [ ] Sort options are available (e.g., *Relevance*, *Price: Low to High*, *Price: High to Low*).
- [ ] Selecting a sort option reorders results correctly.
- [ ] Applied filters and sort options are reflected in the URL (for shareability).
- [ ] **Pagination** is shown if results exceed the per-page limit (e.g., 12 or 20 per page).
- [ ] Pagination navigates to the correct page of results.

---

## 7. Performance

- [ ] Search results load within **3 seconds** for common search terms on a standard connection.
- [ ] A **loading indicator** is shown while results are being fetched.
- [ ] The page does not show a blank white screen without any feedback during loading.

---

## 8. UI Checks

- [ ] The search query is **displayed in the search bar** on the results page.
- [ ] The result count text is clearly readable.
- [ ] Product images on the results page are not broken.
- [ ] Prices are formatted correctly (e.g., `$49.99`, not `49.990000`).
- [ ] The search bar is still visible and usable on the results page (for repeat searches).

---

## Summary

| Category               | Total Items | Checked | Passed | Failed | Skipped |
|------------------------|-------------|---------|--------|--------|---------|
| Layout & Availability  | 5           |         |        |        |         |
| Functional — Positive  | 9           |         |        |        |         |
| Functional — Negative  | 4           |         |        |        |         |
| Input Validation       | 6           |         |        |        |         |
| Autocomplete           | 6           |         |        |        |         |
| Filtering & Sorting    | 7           |         |        |        |         |
| Performance            | 3           |         |        |        |         |
| UI Checks              | 5           |         |        |        |         |
| **Total**              | **45**      |         |        |        |         |

---

## Notes & Observations

> *(Record any defects found, environment-specific issues, or additional observations here.)*

---

*Checklist version 1.0 — ShopEasy Demo Application*
