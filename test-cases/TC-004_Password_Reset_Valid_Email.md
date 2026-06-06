# TC-004 — Password Reset Request with a Registered Email Address

---

## Test Case Details

| Field              | Details                                      |
|--------------------|----------------------------------------------|
| **Test Case ID**   | TC-004                                       |
| **Title**          | Password reset request submitted with a valid registered email |
| **Module**         | Authentication — Password Reset              |
| **Type**           | Positive                                     |
| **Priority**       | High                                         |
| **Status**         | Pass                                         |
| **Tested By**      | QA Engineer                                  |
| **Date Tested**    | 2025-06-02                                   |
| **Environment**    | Chrome 124 / Windows 11 / 1920×1080          |

---

## Preconditions

- Password reset page is accessible at `https://demo.shopeasy.io/forgot-password`.
- A verified registered account exists with the email in Test Data.
- The tester has access to the inbox for the test email account.
- The user is **not** currently logged in.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open `https://demo.shopeasy.io/forgot-password` | Page loads with a single Email input field and a "Send Reset Link" button |
| 2 | Click the **Email** field | Field receives focus |
| 3 | Enter the registered email address from Test Data | Email appears correctly in the field |
| 4 | Click the **Send Reset Link** button | Button triggers submission; brief loading state visible |
| 5 | Observe the on-page confirmation | A success message is displayed on the page |
| 6 | Open the test email inbox | Check for a new email from the application |
| 7 | Locate the password reset email | Email received; sender and subject line are correct |
| 8 | Click the **Reset Password** link in the email | A new browser tab opens to the password reset form |
| 9 | Verify the reset link is valid (page loads, not expired) | Reset form is displayed with New Password and Confirm Password fields |

---

## Test Data

| Field  | Value                          |
|--------|--------------------------------|
| Email  | `testuser@example.com`         |
| Inbox  | Accessible via test email tool |

---

## Expected Result

- After submitting the form, a **neutral confirmation message** is shown:
  > *"If an account with that email exists, a password reset link has been sent."*
  *(Note: the message should not confirm whether the email is registered — same message for registered and unregistered emails.)*
- A **reset email** is received within **2 minutes**.
- The email includes:
  - **Sender:** `no-reply@shopeasy.io`
  - **Subject:** *"Reset your ShopEasy password"*
  - A clearly labelled **"Reset Password" button or link**
  - An expiry notice (e.g., *"This link expires in 1 hour"*)
- Clicking the link opens a valid password reset form.
- The reset link is a **one-time-use** URL (clicking it a second time should show an "expired or already used" message).

---

## Actual Result

> ✅ **Pass** — Confirmation message displayed. Reset email received within 45 seconds. Email contained correct sender, subject, and a one-time reset link. Link opened a valid reset form. Second click on the used link showed "This link has expired or already been used."

---

## Additional Checks

| Check                                          | Result |
|------------------------------------------------|--------|
| Confirmation message shown on page             | ✅ Pass |
| Reset email received within 2 minutes          | ✅ Pass |
| Correct sender address                         | ✅ Pass |
| Correct subject line                           | ✅ Pass |
| Reset link opens valid form                    | ✅ Pass |
| Reset link is single-use only                  | ✅ Pass |
| Link expiry notice present in email            | ✅ Pass |
| Confirmation message is generic (no enumeration) | ✅ Pass |

---

## Notes

- Also tested with a **non-registered email** (`nobody@example.com`) — the confirmation message was identical, confirming no user enumeration in the reset flow.
- The reset link URL contains a secure token (appears to be a UUID or similar random string, not sequential or predictable).
