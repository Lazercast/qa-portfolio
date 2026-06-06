# TC-003 — Registration Form Submission with All Fields Empty

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-003                                       |
| **Title**          | Registration form submission with all required fields left empty |
| **Module**         | Authentication — Registration Page           |
| **Type**           | Negative / Validation                        |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-01                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- The registration page is accessible at `https://demo.shopeasy.io/register`.
- The user has **not** filled in any fields.
- The user does **not** have an existing account.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io/register` | Registration form loads; all fields are empty |
| 2 | Do **not** enter any data in any field | All fields remain blank |
| 3 | Click the **Create Account** button without filling in any field | Form attempts submission |
| 4 | Observe which fields display validation errors | Inline error messages appear on all required fields |
| 5 | Check error message for the **First Name** field | Validation error shown |
| 6 | Check error message for the **Last Name** field | Validation error shown |
| 7 | Check error message for the **Email** field | Validation error shown |
| 8 | Check error message for the **Password** field | Validation error shown |
| 9 | Check error message for the **Confirm Password** field | Validation error shown |
| 10 | Verify the page URL has not changed | URL remains at `/register` |

---

## Test Data

| Field            | Value  |
|------------------|--------|
| First Name       | *(empty)* |
| Last Name        | *(empty)* |
| Email            | *(empty)* |
| Password         | *(empty)* |
| Confirm Password | *(empty)* |

---

## Expected Result

- The form is **not submitted**. No network request is sent (verifiable via DevTools → Network tab).
- **Each required field** displays an individual inline validation error message directly below it:
  - First Name: *"First name is required."*
  - Last Name: *"Last name is required."*
  - Email: *"Email address is required."*
  - Password: *"Password is required."*
  - Confirm Password: *"Please confirm your password."*
- Error messages are visible, clearly readable, and styled in red or with a warning icon.
- The **Create Account** button remains on the page (form is not submitted).
- The page URL stays at `https://demo.shopeasy.io/register`.

---

## Actual Result

> ✅ **Pass** — All five required fields displayed individual inline error messages. No network request was sent (confirmed in DevTools Network tab — zero new requests on button click). URL unchanged.

---

## Validation Error Checklist

| Field            | Error Shown | Error Message Correct | Styling Correct |
|------------------|-------------|----------------------|-----------------|
| First Name       | ✅ Yes      | ✅ Yes               | ✅ Yes          |
| Last Name        | ✅ Yes      | ✅ Yes               | ✅ Yes          |
| Email            | ✅ Yes      | ✅ Yes               | ✅ Yes          |
| Password         | ✅ Yes      | ✅ Yes               | ✅ Yes          |
| Confirm Password | ✅ Yes      | ✅ Yes               | ✅ Yes          |

---

## Notes

- Tested by pressing **Enter** inside a field as well as clicking the button — both trigger the same validation behaviour.
- Error messages disappear as soon as the user starts typing in the relevant field (real-time clearing of errors) — correct UX behaviour.
