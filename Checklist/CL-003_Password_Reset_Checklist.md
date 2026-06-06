# CL-003 — Password Reset Checklist

---

## Checklist Details

| Field            | Details                                      |
|------------------|----------------------------------------------|
| **Checklist ID** | CL-003                                       |
| **Title**        | Password Reset — Manual Testing Checklist    |
| **Module**       | Authentication — Password Reset              |
| **Testing Types**| Functional, Validation, Security, UI         |
| **Priority**     | High                                         |
| **Prepared By**  | QA Engineer                                  |
| **Date**         | 2025-06-02                                   |
| **Environment**  | Chrome 124 / Windows 11 / 1920×1080          |
| **App URL**      | `https://demo.shopeasy.io/forgot-password`   |

---

## Preconditions

- Password reset page is accessible.
- At least one verified registered account exists.
- The tester has access to the test email inbox.
- The user is **not** logged in.

---

## 1. Forgot Password Page — Layout & Load

- [ ] Page loads within 3 seconds.
- [ ] Page contains a clear heading such as *"Forgot your password?"* or *"Reset Password"*.
- [ ] An **Email** input field is present and correctly labelled.
- [ ] A **"Send Reset Link"** (or equivalent) button is present and clearly styled.
- [ ] A **"Back to Login"** link is visible.
- [ ] No broken images or layout issues are visible.

---

## 2. Forgot Password — Functional Checks

- [ ] Submitting a **registered email** shows a confirmation message on the page.
- [ ] The confirmation message is **generic** — does not confirm whether the email is registered (e.g., *"If an account with that email exists, a reset link has been sent."*).
- [ ] Submitting a **non-registered email** shows the **same** confirmation message as a registered email (no user enumeration).
- [ ] A **reset email** is received in the test inbox within **2 minutes**.
- [ ] The reset email is sent from the correct sender address (e.g., `no-reply@shopeasy.io`).
- [ ] The email subject line is clear (e.g., *"Reset your ShopEasy password"*).
- [ ] The email contains a clearly labelled **"Reset Password"** button or link.
- [ ] The email contains an **expiry notice** (e.g., *"This link expires in 1 hour"*).
- [ ] Submitting the form with an **empty Email field** shows a required field validation error without submitting.
- [ ] Submitting with an **invalid email format** (e.g., `notanemail`) shows a format validation error.

---

## 3. Reset Password Form (via Email Link)

- [ ] Clicking the reset link in the email opens the reset password form in the browser.
- [ ] The reset form page loads correctly with a clear heading (e.g., *"Set a New Password"*).
- [ ] The form contains **New Password** and **Confirm New Password** fields.
- [ ] Both fields mask entered characters (`•••`).
- [ ] Submitting a **valid, strong new password** (matching in both fields) resets the password successfully.
- [ ] After successful reset, a success message is shown and/or the user is redirected to the login page.
- [ ] The user can **log in with the new password** immediately after reset.
- [ ] The user **cannot log in with the old password** after a successful reset.

---

## 4. Reset Link Expiry & Security

- [ ] The reset link is **single-use** — using it a second time shows an *"expired or already used"* error page.
- [ ] The reset link **expires** after the stated time period (test by waiting beyond the expiry window, or by requesting a second reset link which should invalidate the first).
- [ ] The reset link contains a **long, random token** in the URL — not a sequential number or predictable pattern.
- [ ] The reset page is served over **HTTPS**.
- [ ] Requesting a **second reset link** for the same email invalidates the first link.
- [ ] After a successful password reset, the user's existing **active sessions** are invalidated (they are logged out on other devices).

---

## 5. New Password Validation (Reset Form)

- [ ] **Empty** New Password field — validation error shown; form not submitted.
- [ ] **Empty** Confirm New Password field — validation error shown.
- [ ] **Mismatched** passwords — error shown: *"Passwords do not match."*
- [ ] **Weak password** (e.g., `12345678`) — rejected with a clear policy error message.
- [ ] **Strong password** meeting all requirements — accepted successfully.
- [ ] **Same password as the old one** (if restricted) — appropriate error shown.

---

## 6. UI & Styling Checks

- [ ] The "Send Reset Link" button shows a **loading indicator** while the request is in progress.
- [ ] The button is **disabled** during the request to prevent duplicate submissions.
- [ ] All form fields have visible **focus states** when navigating by keyboard.
- [ ] Tab order is logical across all form fields and buttons.
- [ ] Error messages are clearly visible, styled in red or with a warning icon.

---

## Summary

| Category                    | Total Items | Checked | Passed | Failed | Skipped |
|-----------------------------|-------------|---------|--------|--------|---------|
| Page Load & Layout          | 6           |         |        |        |         |
| Forgot Password — Functional| 10          |         |        |        |         |
| Reset Form — Functional     | 8           |         |        |        |         |
| Link Expiry & Security      | 6           |         |        |        |         |
| New Password Validation     | 6           |         |        |        |         |
| UI & Styling                | 5           |         |        |        |         |
| **Total**                   | **41**      |         |        |        |         |

---

## Notes & Observations

> *(Record any defects found, environment-specific issues, or additional observations here.)*

---

*Checklist version 1.0 — ShopEasy Demo Application*
