# TC-010 — Login Page Displays and Functions Correctly on Mobile Viewports

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-010                                       |
| **Title**          | Login page layout, elements, and functionality are correct on mobile viewports |
| **Module**         | Authentication — Login Page / Mobile Responsiveness |
| **Type**           | Positive / UI                                |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-05                                   |
| **Environment**    | Chrome DevTools Responsive Mode + iPhone 15 (physical device) |

---

## Preconditions

- Application is accessible at `https://demo.shopeasy.io/login`.
- Testing is performed using both **Chrome DevTools Responsive Mode** and a **physical iOS device** (iPhone 15, iOS 17.4.1).
- The device/viewport is set to the dimensions listed in the Test Data table.
- No browser extensions that modify page layout are active.
- The user is **not** currently logged in.

---

## Test Steps

For **each viewport size** listed in the Test Data table:

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open Chrome DevTools (F12) and activate Responsive Mode (Ctrl+Shift+M) | Responsive mode is active |
| 2 | Set the viewport to the dimensions from the Test Data row | Viewport resizes to the specified dimensions |
| 3 | Navigate to `https://demo.shopeasy.io/login` | Login page loads |
| 4 | Check the **site logo/brand name** is visible | Logo is visible and not cut off or overlapping |
| 5 | Check the **Email** input field | Field is fully visible, not clipped, and correctly sized for the viewport |
| 6 | Check the **Password** input field | Field is fully visible and correctly sized |
| 7 | Check the **Login** button | Button spans an appropriate width; text is not truncated; fully tappable |
| 8 | Check the **"Forgot Password?"** link | Link is visible and has sufficient tap target size (≥44×44px) |
| 9 | Check the **"Create an account"** link | Link is visible and accessible |
| 10 | Scroll the page | No horizontal scroll appears; all content fits within the viewport width |
| 11 | **Tap the Email field** on a touch device | Mobile keyboard opens; field does not zoom in unexpectedly |
| 12 | Enter email and password, then tap **Login** | Login functions correctly (same as desktop) |
| 13 | Check that no elements **overlap** each other | All elements have adequate spacing |
| 14 | Confirm text is **readable** without zooming | Font size is appropriate; no microscopic text |

---

## Test Data — Viewports Tested

| # | Device Simulated        | Viewport Width | Viewport Height | OS / Browser            |
|---|-------------------------|---------------|-----------------|-------------------------|
| 1 | iPhone SE (3rd gen)     | 375px         | 667px           | iOS Safari (DevTools)   |
| 2 | iPhone 15               | 390px         | 844px           | iOS Safari (physical)   |
| 3 | Samsung Galaxy S23      | 360px         | 780px           | Android Chrome (DevTools) |
| 4 | Google Pixel 7          | 412px         | 915px           | Android Chrome (DevTools) |
| 5 | iPad Mini               | 768px         | 1024px          | iPadOS Safari (DevTools) |

---

## Expected Result

At all tested mobile viewport sizes:

- The login form is **centred** on the screen with appropriate left/right padding.
- All input fields span the full usable width (with margins), making them easy to tap.
- The **Login button** is wide enough for comfortable thumb tapping (minimum 44px height per Apple HIG / Google Material guidelines).
- **No horizontal scrollbar** appears at any viewport size.
- **No elements overlap** each other.
- Text is readable at the default zoom level (no need to pinch-zoom to read labels).
- Tapping an input field opens the appropriate mobile keyboard (email field opens the email keyboard with `@` symbol accessible).
- The `viewport` meta tag prevents unintended page zoom on input field focus.
- The page functions identically to desktop — login works correctly on mobile.

---

## Actual Result

> ✅ **Pass (4/5 viewports)** — All UI checks passed on iPhone SE, iPhone 15, Galaxy S23, and Pixel 7 viewports. Login functioned correctly on all. On **iPad Mini (768px)**, the navigation menu showed an overflow issue *(separate bug already logged as BUG-005)*. The login form itself was unaffected on iPad Mini.

---

## UI Checklist by Viewport

| Check                              | 375px | 390px | 360px | 412px | 768px |
|------------------------------------|-------|-------|-------|-------|-------|
| Logo visible                       | ✅    | ✅    | ✅    | ✅    | ✅    |
| Email field fully visible          | ✅    | ✅    | ✅    | ✅    | ✅    |
| Password field fully visible       | ✅    | ✅    | ✅    | ✅    | ✅    |
| Login button full-width, tappable  | ✅    | ✅    | ✅    | ✅    | ✅    |
| No horizontal scroll               | ✅    | ✅    | ✅    | ✅    | ✅    |
| No overlapping elements            | ✅    | ✅    | ✅    | ✅    | ✅    |
| Text readable without zoom         | ✅    | ✅    | ✅    | ✅    | ✅    |
| Email keyboard on email field      | ✅    | ✅    | ✅    | ✅    | ✅    |
| No unexpected zoom on input focus  | ✅    | ✅    | ✅    | ✅    | ✅    |
| Login functions correctly          | ✅    | ✅    | ✅    | ✅    | ✅    |

---

## Additional UI Observations

- The **"Forgot Password?"** link has a comfortable tap target on all mobile viewports (verified with DevTools accessibility inspector — tap target ≥ 44×44px).
- The email input correctly uses `inputmode="email"` — the email keyboard layout appears on mobile with the `@` and `.com` keys readily accessible.
- The `<meta name="viewport" content="width=device-width, initial-scale=1">` tag is present (confirmed via DevTools Elements panel), preventing unwanted scaling.

---

## Notes

- Physical device testing (iPhone 15) matched DevTools simulation results — a good indicator that the responsive design is implemented consistently.
- The navigation overflow on the iPad Mini viewport is a known issue logged separately in **BUG-005** and does not block this test case from passing for the login form itself.
- Testing was also performed in **landscape orientation** on the iPhone 15 (844×390px) — the form adapted correctly to landscape with no layout breakage.
