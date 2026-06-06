# TC-007 — Product Search Handles Special Characters and Boundary Inputs Safely

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-007                                       |
| **Title**          | Search field handles special characters, empty input, and boundary values without errors |
| **Module**         | Search Functionality — Input Validation       |
| **Type**           | Negative / Validation / Boundary              |
| **Priority**       | Medium                                       |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-03                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- Application is accessible at `https://demo.shopeasy.io`.
- Search bar is visible on the homepage.
- The tester will run multiple sub-tests using different input values from the Test Data table.

---

## Test Steps

Repeat the following steps for **each input value** in the Test Data table:

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io` | Homepage loads |
| 2 | Click the search input field | Field receives focus |
| 3 | Enter the test input value | Input is accepted (or appropriately limited/sanitised) |
| 4 | Press **Enter** or click the Search icon | Search is triggered |
| 5 | Observe the results page or error response | Page handles the input gracefully; no server error |
| 6 | Check the page title / result message | Appropriate "no results" or sanitised results message shown |
| 7 | Check for any JavaScript console errors | DevTools console shows no new errors |
| 8 | Verify the URL in the address bar | URL encodes the query safely (no raw special characters breaking the URL) |

---

## Test Data

| # | Input Value | Input Type | Expected Behaviour |
|---|-------------|------------|-------------------|
| 1 | *(empty — press Enter immediately)* | Empty | No search; inline prompt to enter a keyword |
| 2 | `   ` (3 spaces only) | Whitespace | Treated as empty; same as Test 1 |
| 3 | `!@#$%^&*()` | Special characters | No results shown; no server crash |
| 4 | `<script>alert('XSS')</script>` | XSS attempt | Script tag is not executed; shown as plain text or sanitised |
| 5 | `' OR '1'='1` | SQL injection attempt | No data leak; "no results" shown; no server error |
| 6 | `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` (100 chars) | Boundary — max length | Input either accepted (no results) or truncated at character limit |
| 7 | `🎧🎵🎤` | Emoji input | "No results found" displayed; no crash |
| 8 | `NULL` | Reserved word | Treated as a literal text search; "no results" shown |

---

## Expected Result

For **all** inputs above:

- The application does **not crash** or return an HTTP 500 error.
- No JavaScript errors appear in the browser console.
- Special characters in the URL are **percent-encoded** (e.g., `%3Cscript%3E`), not raw.
- The `<script>` tag input is **not executed** — no alert dialogue appears (XSS protection confirmed).
- SQL injection input returns a *"No results found"* message — no database error or unexpected data is returned.
- Empty / whitespace-only input either: (a) does not submit, prompting the user to enter a keyword, or (b) returns all products or a friendly prompt.
- The 100-character input is handled without error (either searched or truncated with a visible character limit message).

---

## Actual Result

> ✅ **Pass (all 8 sub-tests)** — No server errors for any input. XSS script tag was not executed (rendered as plain text in the "no results" message). SQL injection attempt returned "No results found" with no data exposure. Empty submit showed inline prompt. 100-char input returned "No results found." Emoji input handled without crash. URLs correctly percent-encoded in all cases.

---

## Results Summary

| # | Input            | Server Error | JS Console Error | XSS Executed | SQL Data Exposed | Result  |
|---|------------------|-------------|-----------------|--------------|-----------------|---------|
| 1 | Empty            | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |
| 2 | Spaces only      | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |
| 3 | `!@#$%^&*()`     | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |
| 4 | XSS script tag   | ❌ No       | ❌ No           | ❌ No        | N/A             | ✅ Pass |
| 5 | SQL injection    | ❌ No       | ❌ No           | N/A          | ❌ No           | ✅ Pass |
| 6 | 100-char string  | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |
| 7 | Emoji `🎧🎵🎤` | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |
| 8 | `NULL`           | ❌ No       | ❌ No           | N/A          | N/A             | ✅ Pass |

---

## Notes

- XSS and SQL injection tests are standard practice in manual QA to confirm basic input sanitisation — these are not penetration tests but smoke-level security checks.
- The 100-character test confirms no buffer overflow or UI breakage from very long inputs.
