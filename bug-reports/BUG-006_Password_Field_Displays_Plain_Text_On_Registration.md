# BUG-006 — Registration Password Field Displays Characters as Plain Text Instead of Masked

---

## Summary

The **Password** and **Confirm Password** fields on the registration page display entered characters as **plain visible text** instead of masking them with bullet points or asterisks. This is a security and UI bug that exposes sensitive user credentials to anyone who can view the user's screen.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-006                          |
| **Title**        | Registration password field renders as plain text (not masked) |
| **Type**         | UI / Security                    |
| **Severity**     | High                             |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-03                       |
| **Assigned To**  | Frontend Team                    |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/register` |
| **Browser**      | Chrome 124.0, Firefox 126.0, Edge 124.0 |
| **OS**           | Windows 11 Pro, macOS Ventura   |
| **Resolution**   | 1920×1080                        |
| **Network**      | Any                              |

---

## Preconditions

- The registration page is accessible.
- The user navigates to `/register` in any major desktop browser.
- No browser extensions that modify form fields are active.

---

## Steps to Reproduce

1. Navigate to `https://demo.shopeasy.io/register`.
2. Click on the **Password** input field.
3. Type any value, e.g., `MySecurePass123!`.
4. Observe the characters displayed in the field.
5. Repeat for the **Confirm Password** field.

---

## Expected Result

As the user types into the **Password** and **Confirm Password** fields, each character should be immediately masked with a bullet (`•`) or asterisk (`*`) symbol. This is the standard browser behaviour for `<input type="password">` elements. The `Show/Hide password` toggle (if present) should only reveal characters when explicitly activated by the user.

---

## Actual Result

Both the **Password** and **Confirm Password** fields display every character as plain, readable text as the user types. For example, typing `MySecurePass123!` shows:

```
MySecurePass123!
```

instead of:

```
••••••••••••••••
```

---

## Additional Information

- Inspecting the HTML source in DevTools reveals the root cause:

  **Actual HTML (buggy):**
  ```html
  <input type="text" id="password" name="password" placeholder="Create a password">
  ```

  **Expected HTML:**
  ```html
  <input type="password" id="password" name="password" placeholder="Create a password" autocomplete="new-password">
  ```

- The `type` attribute is set to `"text"` rather than `"password"` for both password fields on the registration form. This appears to be a copy-paste or refactoring error.
- The **Login** page (`/login`) correctly uses `type="password"` and is **not** affected by this bug.
- This is reproducible across **all tested browsers** and **all operating systems** — it is not environment-specific.

---

## Security Impact

Exposing password characters as plain text is a significant security concern:

- Shoulder surfing (someone viewing the screen in a public place) can capture the user's password.
- Screen recording software, browser extension screenshots, or auto-fill logging may capture the plain-text password.
- This may violate OWASP security guidelines for authentication forms (OWASP ASVS v4.0, Section 2.1).

---

## Attachments

- `screenshot_password_plaintext.png` — Registration form showing password in plain text
- `devtools_html_inspection.png` — DevTools Elements panel showing `type="text"` on the password field

---

## Suggested Fix

Change the `type` attribute from `"text"` to `"password"` on both the **Password** and **Confirm Password** input fields in the registration form template. Also add `autocomplete="new-password"` to assist password managers and further enhance security.
