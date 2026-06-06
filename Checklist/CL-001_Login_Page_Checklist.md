# CL-001 — Login Page Checklist

---

## Checklist Details

| Field            | Details                                      |
|------------------|----------------------------------------------|
| **Checklist ID** | CL-001                                       |
| **Title**        | Login Page — Manual Testing Checklist        |
| **Module**       | Authentication — Login                       |
| **Testing Types**| Functional, Validation, UI, Usability        |
| **Priority**     | High                                         |
| **Prepared By**  | QA Engineer                                  |
| **Date**         | 2025-06-01                                   |
| **Environment**  | Chrome 124 / Windows 11 / 1920×1080          |
| **App URL**      | `https://demo.shopeasy.io/login`             |

---

## Preconditions

- Application is accessible and the login page loads without errors.
- At least one verified registered account exists for positive test scenarios.
- Browser cache is cleared before starting.
- JavaScript is enabled; no interfering browser extensions are active.

---

## 1. Page Load & Layout

- [ ] Login page loads within 3 seconds on a standard broadband connection.
- [ ] Page title in the browser tab is correct (e.g., *"Login — ShopEasy"*).
- [ ] Site logo is visible and links back to the homepage.
- [ ] Email input field is visible and correctly labelled.
- [ ] Password input field is visible and correctly labelled.
- [ ] **Login** button is visible, fully rendered, and not overlapping other elements.
- [ ] **"Forgot Password?"** link is visible below or near the password field.
- [ ] **"Create an account"** / **"Register"** link is present on the page.
- [ ] No broken images or missing icons on the page.
- [ ] Page layout is not broken at 1280px, 1440px, and 1920px desktop widths.

---

## 2. Functional Testing — Positive Scenarios

- [ ] Logging in with a valid registered email and correct password redirects the user to the dashboard.
- [ ] After successful login, the user's name or avatar is visible in the navigation bar.
- [ ] Pressing **Enter** on the keyboard after filling in both fields submits the form (same as clicking the button).
- [ ] The session persists after refreshing the page (F5) — user remains logged in.
- [ ] The **"Forgot Password?"** link navigates to the password reset page.
- [ ] The **"Create an account"** link navigates to the registration page.
- [ ] After login, clicking the browser **Back** button does not return the user to the login page (session is active).

---

## 3. Functional Testing — Negative Scenarios

- [ ] Submitting the form with a **correct email and wrong password** shows an error message and does not log the user in.
- [ ] Submitting with a **non-existent email** shows the same generic error message as a wrong password (no user enumeration).
- [ ] Submitting with **both fields empty** triggers validation errors on both fields without submitting the form.
- [ ] Submitting with only the **Email field empty** triggers a validation error on the Email field.
- [ ] Submitting with only the **Password field empty** triggers a validation error on the Password field.
- [ ] Entering an **incorrectly formatted email** (e.g., `notanemail`, `user@`) shows a format validation error.
- [ ] After **5 consecutive wrong password attempts**, the account is temporarily locked and an appropriate message is shown.
- [ ] The login page is **not accessible** when the user is already logged in (redirects to dashboard instead).

---

## 4. Input Field Validation

- [ ] The Email field accepts standard valid email formats (e.g., `user@example.com`, `user.name+tag@domain.co`).
- [ ] The Email field rejects clearly invalid formats without submitting (e.g., `@domain`, `user@`, `plaintext`).
- [ ] The Password field masks entered characters with bullet points (`•••`).
- [ ] The **Show/Hide password** toggle (if present) reveals and re-masks the password correctly.
- [ ] No auto-correct or auto-capitalisation is applied to the Email field on desktop browsers.
- [ ] Pasting text into both fields works correctly.
- [ ] Copy-pasting the password into the field works (characters remain masked).

---

## 5. Error Messages

- [ ] Error messages appear **inline** below the relevant field or at the top of the form.
- [ ] Error messages are **visible** (not hidden behind other elements, not white text on white background).
- [ ] Error messages are written in **clear, user-friendly language** (no technical jargon or raw error codes).
- [ ] Error messages **disappear** when the user corrects the relevant field and re-submits or re-focuses.
- [ ] Only **one** error state is shown per field at a time (no duplicate messages).

---

## 6. UI & Styling Checks

- [ ] Email and Password fields are visually aligned and consistent in size.
- [ ] The Login button styling (colour, font, size) matches the site's design system.
- [ ] Focus states are visible on both input fields when navigating with the keyboard (Tab key).
- [ ] The Login button shows a loading indicator (spinner or text change) while the request is in progress.
- [ ] The Login button is **disabled** or shows a loading state while a request is in progress (prevents double-submission).
- [ ] All fonts on the page are readable and consistent with the rest of the site.
- [ ] There are no obvious alignment or spacing inconsistencies between form elements.

---

## 7. Security Checks

- [ ] The page is served over **HTTPS** (padlock icon in the browser address bar).
- [ ] The Password field uses `type="password"` (not `type="text"`).
- [ ] The browser does not autofill the password into a visible plain-text field.
- [ ] The login form includes a **CSRF token** or equivalent protection (verifiable in page source or DevTools).
- [ ] After logout, the previous session is invalidated — navigating back to the dashboard (via browser history) redirects to the login page.

---

## 8. Usability Checks

- [ ] Tab order moves logically: Email → Password → Login button → links.
- [ ] The **Email** field is auto-focused when the login page loads (cursor ready to type immediately).
- [ ] The page provides a clear visual indicator of which field currently has focus.
- [ ] Error states do not clear the Email field — the user only has to re-enter the password.

---

## Summary

| Category              | Total Items | Checked | Passed | Failed | Skipped |
|-----------------------|-------------|---------|--------|--------|---------|
| Page Load & Layout    | 10          |         |        |        |         |
| Functional — Positive | 7           |         |        |        |         |
| Functional — Negative | 8           |         |        |        |         |
| Input Validation      | 7           |         |        |        |         |
| Error Messages        | 5           |         |        |        |         |
| UI & Styling          | 7           |         |        |        |         |
| Security              | 5           |         |        |        |         |
| Usability             | 4           |         |        |        |         |
| **Total**             | **53**      |         |        |        |         |

---

## Notes & Observations

> *(Record any defects found, environment-specific issues, or additional observations during testing here.)*

---

*Checklist version 1.0 — ShopEasy Demo Application*
