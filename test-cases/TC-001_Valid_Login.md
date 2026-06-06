# TC-001 — Valid Login with Correct Credentials

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-001                                       |
| **Title**          | Valid login with correct email and password   |
| **Module**         | Authentication — Login Page                  |
| **Type**           | Positive                                     |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-01                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- The application is accessible at `https://demo.shopeasy.io/login`.
- A verified registered account exists with the credentials listed in Test Data.
- The user is currently **not** logged in (no active session).
- JavaScript is enabled and no browser extensions interfere with the form.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io/login` in Chrome | Login page loads within 3 seconds; Email and Password fields are visible |
| 2 | Click the **Email** input field | Field receives focus; cursor is placed inside the field |
| 3 | Enter the email address from Test Data | Email value appears correctly in the field; no auto-correction |
| 4 | Click the **Password** input field | Field receives focus |
| 5 | Enter the password from Test Data | Password characters are masked (shown as `•••••`) |
| 6 | Click the **Login** button | Button is clickable; a loading indicator appears briefly |
| 7 | Observe the page after the request completes | User is redirected to the dashboard |

---

## Test Data

| Field      | Value                        |
|------------|------------------------------|
| Email      | `testuser@example.com`       |
| Password   | `ValidPass123!`              |
| Account    | Registered and email-verified |

---

## Expected Result

- The user is successfully authenticated.
- The browser redirects to `https://demo.shopeasy.io/dashboard`.
- The dashboard displays a personalised welcome message: *"Welcome back, Test User!"*
- The top navigation bar shows the user's name or avatar, confirming the session is active.
- No error messages are displayed.

---

## Actual Result

> ✅ **Pass** — The application redirected to the dashboard as expected. Welcome message and user avatar displayed correctly. Session cookie set in browser storage.

---

## Notes

- Tested with both mouse click and pressing **Enter** on the keyboard after filling in the password — both trigger submission correctly.
- Verified that the session persists after a page refresh (F5).
