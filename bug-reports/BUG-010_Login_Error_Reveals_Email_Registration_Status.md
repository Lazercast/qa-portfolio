# BUG-010 — Login Error Message Reveals Whether an Email Address Is Registered

---

## Summary

The login page displays **different error messages** depending on whether the submitted email address exists in the system. This information disclosure allows an attacker to enumerate valid user accounts by probing the login form — a security vulnerability known as **user enumeration**. Both "email not found" and "incorrect password" scenarios should return an identical, generic error message.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-010                          |
| **Title**        | Login error messages reveal whether an email address is registered (user enumeration) |
| **Type**         | Validation / Security            |
| **Severity**     | Medium                           |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-05                       |
| **Assigned To**  | Backend Team                     |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/login` |
| **Browser**      | Chrome 124.0, Firefox 126.0     |
| **OS**           | Windows 11 Pro                   |
| **Resolution**   | 1920×1080                        |
| **Network**      | Wi-Fi                            |

---

## Preconditions

- Login page is accessible.
- At least one registered user account exists (e.g., `registered@example.com`).
- The tester knows one email address that is **registered** and one that is **not registered**.

---

## Steps to Reproduce

**Test Case A — Registered email, wrong password:**

1. Navigate to `https://demo.shopeasy.io/login`.
2. Enter a **registered** email address: `registered@example.com`.
3. Enter an **incorrect** password: `WrongPassword1!`.
4. Click **Login**.
5. Note the exact error message displayed.

**Test Case B — Unregistered email:**

1. Navigate to `https://demo.shopeasy.io/login`.
2. Enter an email address **not** in the system: `notregistered@example.com`.
3. Enter any password: `AnyPassword1!`.
4. Click **Login**.
5. Note the exact error message displayed.

---

## Expected Result

**Both Test Case A and Test Case B** should display the **same generic error message**, giving no indication of whether the email address is registered:

> *"The email address or password you entered is incorrect. Please try again."*

This prevents an attacker from determining which email addresses correspond to valid accounts.

---

## Actual Result

**Test Case A — Registered email, wrong password:**
> *"Incorrect password. Please try again or [reset your password]."*

**Test Case B — Unregistered email:**
> *"No account found with that email address. [Create an account?]"*

The two distinct error messages reveal exactly whether the email address exists in the system. An attacker can automate login attempts with a list of email addresses and use these different responses to build a list of valid registered accounts — without ever needing to know a password.

---

## Security Impact

**User enumeration** is classified as a security vulnerability by:

- **OWASP Testing Guide (OTG-IDENT-004):** *"Test for Account Enumeration and Guessable User Account"*
- **OWASP ASVS v4.0, Section 2.2.1:** Authentication systems should not reveal whether a username is registered.

**Attack scenario:** A malicious actor submits POST requests to `/api/v1/auth/login` with a list of 10,000 email addresses. For each one that returns the "Incorrect password" message (vs. "No account found"), the attacker learns the email is registered. This list can then be used for targeted phishing, credential stuffing, or brute-force attacks against specific accounts.

---

## Test Data

| Email                         | Password           | Error Shown                                | Info Disclosed   |
|-------------------------------|--------------------|--------------------------------------------|------------------|
| `registered@example.com`      | `WrongPass1!`      | "Incorrect password. Try again…"           | Email exists ✗   |
| `notregistered@example.com`   | `AnyPass1!`        | "No account found with that email…"        | Email not found ✗|
| `registered@example.com`      | `CorrectPass1!`    | Successful login → Dashboard               | N/A              |

---

## Additional Information

- This also applies to the **"Forgot Password"** flow — the page currently shows *"A reset link has been sent to your email"* for registered addresses, and *"We couldn't find an account with that email"* for unregistered ones. The same generic-message fix should be applied there.
- The API response body also differs (`"error": "PASSWORD_INCORRECT"` vs `"error": "USER_NOT_FOUND"`), which exposes the same information to anyone inspecting API responses directly.

---

## Attachments

- `screenshot_error_wrong_password.png` — Login error for registered email with wrong password
- `screenshot_error_no_account.png` — Login error for unregistered email
- `postman_response_user_not_found.png` — API response body showing `USER_NOT_FOUND` error code

---

## Suggested Fix

1. **Unify error messages** — return the same message for both scenarios:
   > *"The email address or password you entered is incorrect."*

2. **Unify API error codes** — return the same generic error code for both cases:
   ```json
   {
     "success": false,
     "error": {
       "code": "INVALID_CREDENTIALS",
       "message": "The email address or password you entered is incorrect."
     }
   }
   ```

3. **Apply the same fix to the Forgot Password flow** — always show:
   > *"If an account with that email exists, a reset link has been sent."*

4. **Consider rate limiting** the login endpoint to mitigate brute-force and enumeration attempts regardless of the message unification.
