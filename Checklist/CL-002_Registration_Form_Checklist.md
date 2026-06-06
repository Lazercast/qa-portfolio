# CL-002 — Registration Form Checklist

---

## Checklist Details

| Field            | Details                                      |
|------------------|----------------------------------------------|
| **Checklist ID** | CL-002                                       |
| **Title**        | Registration Form — Manual Testing Checklist |
| **Module**       | Authentication — Registration                |
| **Testing Types**| Functional, Validation, UI, Security         |
| **Priority**     | High                                         |
| **Prepared By**  | QA Engineer                                  |
| **Date**         | 2025-06-01                                   |
| **Environment**  | Chrome 124 / Windows 11 / 1920×1080          |
| **App URL**      | `https://demo.shopeasy.io/register`          |

---

## Preconditions

- Registration page loads without errors.
- The tester has access to a test email inbox to verify confirmation emails.
- Browser cache is cleared before starting.
- No existing account uses the test email addresses.

---

## 1. Page Load & Layout

- [ ] Registration page loads within 3 seconds.
- [ ] Page title in the browser tab is correct (e.g., *"Create Account — ShopEasy"*).
- [ ] All form fields are visible: First Name, Last Name, Email, Password, Confirm Password.
- [ ] Field labels are present, clearly readable, and positioned correctly above or beside each field.
- [ ] **Create Account** button is visible and clearly styled as the primary action.
- [ ] A **"Already have an account? Log in"** link is present.
- [ ] No broken images or missing icons on the page.

---

## 2. Functional Testing — Positive Scenarios

- [ ] Submitting the form with all valid data creates an account and shows a success message or redirects.
- [ ] A **confirmation/verification email** is sent to the registered email address within 2 minutes.
- [ ] The confirmation email contains a working **verification link**.
- [ ] Clicking the verification link activates the account and allows login.
- [ ] After successful registration, the user is either automatically logged in or redirected to the login page (consistent behaviour).
- [ ] The **"Already have an account? Log in"** link navigates to the login page.

---

## 3. Functional Testing — Negative Scenarios

- [ ] Submitting with **all fields empty** shows validation errors on every required field without submitting.
- [ ] Submitting with **only First Name filled** shows errors on all remaining required fields.
- [ ] Registering with an **email already in use** shows an error: e.g., *"An account with this email already exists."*
- [ ] Submitting with **Password and Confirm Password not matching** shows a mismatch error.
- [ ] A form with **all valid data except one missing required field** does not submit.

---

## 4. Field-Level Validation

### First Name & Last Name
- [ ] First Name field is required — empty submission triggers an error.
- [ ] Last Name field is required — empty submission triggers an error.
- [ ] First Name accepts letters, hyphens, and apostrophes (e.g., `O'Brien`, `Mary-Jane`).
- [ ] First Name rejects numbers and special symbols (e.g., `John123`, `@dm!n`).
- [ ] First Name with only spaces is treated as empty and triggers a required field error.
- [ ] Name fields have a **maximum character limit** — test at 50, 100, and 256 characters.

### Email
- [ ] Email field is required — empty submission triggers an error.
- [ ] Valid email formats are accepted: `user@example.com`, `user.name+tag@domain.co.uk`.
- [ ] Invalid formats are rejected: `notanemail`, `@domain.com`, `user@`, `user@.com`, `user name@domain.com`.
- [ ] Email field is **not case-sensitive** — `User@Example.com` and `user@example.com` are treated as the same address.

### Password
- [ ] Password field is required — empty submission triggers an error.
- [ ] Password is masked with bullet characters (`•••`).
- [ ] Password must meet the stated strength requirements (e.g., minimum 8 characters, at least one uppercase, one number, one special character).
- [ ] A **weak password** (e.g., `password`, `12345678`) is rejected with a clear error describing the requirement.
- [ ] A **strong password** meeting all requirements is accepted.
- [ ] Password strength indicator (if present) updates in real time as the user types.

### Confirm Password
- [ ] Confirm Password field is required — empty submission triggers an error.
- [ ] Passwords **matching** — no error shown; form submits normally.
- [ ] Passwords **not matching** — error shown: e.g., *"Passwords do not match."*
- [ ] Changing the Password field after filling Confirm Password re-triggers the mismatch check.

---

## 5. Error Messages

- [ ] All error messages appear **inline below the relevant field** (not just at the top of the page).
- [ ] Error messages use **clear, non-technical language**.
- [ ] Error messages are visually distinct (red text or border, warning icon).
- [ ] Errors clear when the user corrects the input and re-submits.
- [ ] Submitting an already-registered email shows an error but **does not confirm** whether a password is known (security consideration).

---

## 6. UI & Styling Checks

- [ ] All input fields are consistently sized and aligned.
- [ ] Field labels and placeholder text are present and readable.
- [ ] The **Create Account** button is styled as the primary CTA (prominent colour, full width or prominent placement).
- [ ] The button shows a **loading indicator** during form submission (prevents double submission).
- [ ] Tab order is logical: First Name → Last Name → Email → Password → Confirm Password → Submit button.
- [ ] Focus states are visible on all input fields when navigating by keyboard.

---

## 7. Security Checks

- [ ] Page is served over **HTTPS**.
- [ ] Password and Confirm Password fields use `type="password"` — characters are masked.
- [ ] Passwords are **not** sent in the URL query string (verifiable in DevTools → Network tab).
- [ ] The registration form includes **CSRF protection**.
- [ ] The page does not expose server-side validation error details (e.g., raw stack traces or database error messages).

---

## Summary

| Category              | Total Items | Checked | Passed | Failed | Skipped |
|-----------------------|-------------|---------|--------|--------|---------|
| Page Load & Layout    | 7           |         |        |        |         |
| Functional — Positive | 6           |         |        |        |         |
| Functional — Negative | 5           |         |        |        |         |
| Field-Level Validation| 21          |         |        |        |         |
| Error Messages        | 5           |         |        |        |         |
| UI & Styling          | 6           |         |        |        |         |
| Security              | 5           |         |        |        |         |
| **Total**             | **55**      |         |        |        |         |

---

## Notes & Observations

> *(Record any defects found, environment-specific issues, or additional observations here.)*

---

*Checklist version 1.0 — ShopEasy Demo Application*
