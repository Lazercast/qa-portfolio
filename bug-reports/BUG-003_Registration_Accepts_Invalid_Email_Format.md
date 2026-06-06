# BUG-003 — Registration Form Accepts Clearly Invalid Email Addresses

---

## Summary

The user registration form accepts and successfully submits email addresses in invalid formats (e.g., missing `@` symbol, missing domain, plain text with no structure). No client-side or server-side validation error is shown, and the account is created with a malformed email address that cannot receive confirmation emails.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-003                          |
| **Title**        | Registration form accepts invalid email address formats |
| **Type**         | Validation                       |
| **Severity**     | High                             |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-02                       |
| **Assigned To**  | Frontend & Backend Team          |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/register` |
| **Browser**      | Chrome 124.0 / Firefox 126.0    |
| **OS**           | Windows 11 Pro                   |
| **Resolution**   | 1920×1080                        |
| **Network**      | Wi-Fi                            |

---

## Preconditions

- Registration page is accessible and loads without errors.
- The user does **not** have an existing account.
- JavaScript is enabled.

---

## Steps to Reproduce

1. Navigate to `https://demo.shopeasy.io/register`.
2. Fill in all required fields with valid data:
   - **First Name:** `Test`
   - **Last Name:** `User`
   - **Password:** `ValidPass123!`
   - **Confirm Password:** `ValidPass123!`
3. In the **Email** field, enter one of the following invalid values:
   - `notanemail`
   - `missing@`
   - `@nodomain.com`
   - `user@.com`
   - `user name@domain.com` (with a space)
4. Click the **Create Account** button.
5. Observe whether a validation error is shown or if the form submits.

---

## Expected Result

The form should **not submit**. A clear inline validation error message should appear below the Email field, such as:

> *"Please enter a valid email address (e.g., name@example.com)."*

The account should **not** be created until a valid, properly formatted email is provided.

---

## Actual Result

The form submits successfully for all invalid email values tested. A green success message appears: *"Account created! Please check your email to verify your account."*

The user account is created in the system with the malformed email address. No confirmation email is sent (as expected, since the address is invalid), leaving the account in a permanently unverified state.

---

## Test Data — Validation Matrix

| Input Value             | Should Be Accepted | Actually Accepted | Result |
|-------------------------|--------------------|-------------------|--------|
| `user@example.com`      | ✅ Yes             | ✅ Yes            | PASS   |
| `notanemail`            | ❌ No              | ✅ Yes            | **FAIL** |
| `missing@`             | ❌ No              | ✅ Yes            | **FAIL** |
| `@nodomain.com`         | ❌ No              | ✅ Yes            | **FAIL** |
| `user@.com`            | ❌ No              | ✅ Yes            | **FAIL** |
| `user name@domain.com`  | ❌ No              | ✅ Yes            | **FAIL** |
| `user@domain`           | ❌ No              | ✅ Yes            | **FAIL** |

---

## Additional Information

- The issue exists on both **client-side** (no browser-level validation fires) and **server-side** (the API accepts and stores the malformed address).
- The `<input type="email">` HTML attribute validation appears to have been overridden or removed from the form markup.
- This creates a data quality issue in the user database and prevents account confirmation workflows from functioning.
- Verified on Chrome 124, Firefox 126, and via direct API POST — all accept the invalid values.

---

## Attachments

- `screenshot_invalid_email_submitted.png` — Success message shown after submitting `notanemail`
- `screenshot_account_created_db.png` — Admin panel showing malformed email stored in user table

---

## Suggested Fix

1. **Client-side:** Restore `type="email"` on the email input field and add a regex pattern attribute for additional validation.
2. **Server-side:** Implement email format validation in the registration API endpoint using a standard email validation library (e.g., `validator.js` for Node.js, `email-validator` for Python). Server-side validation must exist independently of client-side checks.
