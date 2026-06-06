# TC-002 — Login Attempt with Incorrect Password

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-002                                       |
| **Title**          | Login attempt with a registered email and incorrect password |
| **Module**         | Authentication — Login Page                  |
| **Type**           | Negative                                     |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-01                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- The application is accessible at `https://demo.shopeasy.io/login`.
- A verified registered account exists with email `testuser@example.com`.
- The user is **not** currently logged in.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io/login` | Login page loads successfully |
| 2 | Enter a **registered** email address in the Email field | Email value appears correctly |
| 3 | Enter an **incorrect** password in the Password field | Characters are masked |
| 4 | Click the **Login** button | Button triggers form submission |
| 5 | Observe the page response | An error message appears; the user stays on the login page |
| 6 | Verify the error message content | The message is generic and does not confirm the email exists |
| 7 | Verify the password field is cleared | Password field is empty; email field retains the entered value |

---

## Test Data

| Field    | Value                         |
|----------|-------------------------------|
| Email    | `testuser@example.com`        |
| Password | `WrongPassword999!`           |
| Account  | Registered and email-verified |

---

## Expected Result

- Login is **rejected** — no redirect occurs.
- An inline error message is displayed below the form or at the top of the form:
  > *"The email address or password you entered is incorrect. Please try again."*
- The error message is **generic** (does not say "password is wrong" specifically, to prevent user enumeration).
- The **password field is cleared** for security; the email field retains the entered value.
- The page URL remains `https://demo.shopeasy.io/login`.
- No session is created (no session cookie is set).

---

## Actual Result

> ✅ **Pass** — Error message displayed: *"The email address or password you entered is incorrect."* Password field cleared. URL unchanged. No session cookie created.

---

## Notes

- Verified the error message is identical for a wrong password on a **registered** email vs. a **non-existent** email — both show the same message (no user enumeration). This is correct secure behaviour.
- Also tested 5 consecutive wrong password attempts — account lockout message appeared on the 5th attempt, confirming brute-force protection is in place.
