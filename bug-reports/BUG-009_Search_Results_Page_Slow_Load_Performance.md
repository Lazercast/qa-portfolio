# BUG-009 — Product Search Results Page Loads in 8–12 Seconds for Generic Search Terms

---

## Summary

Searching for common, broad product terms (e.g., "shoes", "phone", "jacket") causes the search results page to take **8–12 seconds to fully load** on a standard broadband connection. The page renders a blank white screen during the load period, with no loading indicator displayed to the user. This significantly degrades the user experience and may cause users to abandon the site.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-009                          |
| **Title**        | Product search results page takes 8–12 seconds to load for broad search terms |
| **Type**         | Performance                      |
| **Severity**     | Medium                           |
| **Priority**     | Medium                           |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-04                       |
| **Assigned To**  | Backend / Frontend Team          |

---

## Environment

| Parameter           | Value                            |
|---------------------|----------------------------------|
| **Application**     | ShopEasy E-Commerce (demo)       |
| **URL**             | `https://demo.shopeasy.io/search?q=shoes` |
| **Browser**         | Chrome 124.0                     |
| **OS**              | Windows 11 Pro                   |
| **Connection**      | Wi-Fi — 100 Mbps download / 20 Mbps upload |
| **Network Throttle**| No throttling (native connection) |
| **Device**          | Desktop PC (Intel Core i7, 16GB RAM) |

---

## Preconditions

- The application is accessible and the user is on the homepage.
- A stable internet connection with ≥ 50 Mbps download speed is available.
- Browser cache has been cleared prior to testing (Ctrl+Shift+Del → Clear all).
- No browser extensions that affect network requests are active (tested in Incognito mode).

---

## Steps to Reproduce

1. Open `https://demo.shopeasy.io` in Chrome.
2. Clear the browser cache (Ctrl+Shift+Del → clear all data).
3. Open **DevTools → Network tab** and tick **Disable cache**.
4. Click the search bar and type `shoes`.
5. Press **Enter** or click the search icon.
6. Start a timer from the moment Enter is pressed.
7. Stop the timer when the search results are fully rendered (product cards visible and interactive).
8. Repeat steps 2–7 with search terms: `phone`, `jacket`, `laptop`.
9. Record the load time for each search.

---

## Expected Result

The search results page should load within **2–3 seconds** on a standard broadband connection. Industry standard for e-commerce search response time is under 2 seconds (Google's benchmark for acceptable page load). A **loading spinner or skeleton UI** should appear immediately while results are being fetched to maintain user feedback.

---

## Actual Result

| Search Term | Results Count | Observed Load Time |
|-------------|---------------|--------------------|
| `shoes`     | ~1,200 results| 11.4 seconds       |
| `phone`     | ~850 results  | 9.7 seconds        |
| `jacket`    | ~640 results  | 8.2 seconds        |
| `laptop`    | ~420 results  | 6.1 seconds        |
| `samsung galaxy s25` | ~12 results | 1.8 seconds ✓ |

**Pattern:** Load time is strongly correlated with the number of results returned. Large result sets (>500 results) consistently exceed 8 seconds.

Additionally, during the load period:
- A **blank white screen** is displayed — no loading spinner, progress bar, or skeleton UI is shown.
- Users have no visual feedback that anything is happening, making it appear the site has frozen.

---

## Performance Metrics (Chrome DevTools — Lighthouse)

| Metric                          | Value      | Benchmark  |
|---------------------------------|------------|------------|
| **Largest Contentful Paint (LCP)**  | 10.8s  | < 2.5s ✗  |
| **Time to First Byte (TTFB)**       | 7.2s   | < 800ms ✗ |
| **Total Blocking Time (TBT)**       | 1,400ms| < 200ms ✗ |
| **Cumulative Layout Shift (CLS)**   | 0.08   | < 0.1 ✓   |

The **TTFB of 7.2 seconds** suggests the primary bottleneck is a slow server-side database query when fetching large result sets.

---

## Additional Information

- Specific search terms that return **fewer than 100 results** load acceptably (1.5–2.5 seconds).
- The Network tab shows a **single API call** to `GET /api/v1/search?q=shoes` that takes **7.1 seconds** to respond, returning the full result set of 1,200 items in a single response payload (**4.2 MB JSON**).
- It appears no **pagination** or **lazy loading** is implemented — the API returns all matching products in a single unfiltered request.
- A loading indicator is missing entirely — users see a white screen during the wait.

---

## Attachments

- `lighthouse_report_search_shoes.html` — Full Lighthouse report
- `devtools_network_search_shoes.png` — Network tab showing 7.1s API response
- `screenshot_blank_screen_during_load.png` — White screen shown while waiting for results

---

## Suggested Fix

Two improvements are recommended:

**1. Server-side pagination (Primary Fix)**
Limit the search API to return a maximum of 20–50 results per page, with pagination parameters:
`GET /api/v1/search?q=shoes&page=1&limit=20`
This will reduce response payload from ~4MB to ~80KB and significantly reduce TTFB.

**2. Loading state UI (UX Fix)**
Display a skeleton loader or spinner immediately when the search is initiated, before the API response is received. This ensures users receive visual feedback and understand the page is working.
