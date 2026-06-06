# BUG-001 — Login Button Unresponsive on Mobile Devices

---

## Summary

The **Login** button on the sign-in page does not respond to tap events on mobile devices running iOS Safari and Android Chrome. The button appears visually active (hover/focus state visible) but submitting the form is impossible without switching to a desktop browser.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-001                          |
| **Title**        | Login button unresponsive on mobile devices |
| **Type**         | Functional / Mobile Responsiveness |
| **Severity**     | Critical                         |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-01                       |
| **Assigned To**  | Frontend Team                    |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io/login` |
| **Browser**      | Safari 17.4 / Chrome 124 (Android) |
| **OS**           | iOS 17.4.1 / Android 14         |
| **Device**       | iPhone 15 / Samsung Galaxy S23  |
| **Screen Size**  | 390×844 / 360×780               |
| **Network**      | Wi-Fi                            |

---

## Preconditions

- User has a registered account with valid credentials.
- Application is accessible and the login page loads successfully.
- JavaScript is enabled in the browser.
- No browser extensions or content blockers are active.

---

## Steps to Reproduce

1. Open `https://demo.shopeasy.io/login` on a mobile device.
2. Enter a valid registered email address in the **Email** field.
3. Enter the correct password in the **Password** field.
4. Tap the **Login** button.
5. Observe the page behaviour.

---

## Expected Result

The form submits successfully. The user is authenticated and redirected to the account dashboard (`/dashboard`).

---

## Actual Result

The **Login** button does not respond to the tap event. No form submission occurs, no error message is displayed, and the user remains on the login page. The button briefly highlights on touch (indicating the touch is registered by the OS), but no JavaScript action is fired.

---

## Additional Information

- The issue is **not reproducible on desktop** browsers (Chrome 124, Firefox 126, Edge 124 on Windows 11).
- Tested on **two different mobile devices** and **two different mobile browsers** — all exhibit the same behaviour.
- DevTools remote inspection shows a JavaScript console error immediately after the tap:

```
Uncaught TypeError: Cannot read properties of null (reading 'addEventListener')
    at login.js:42:18
```

- The button functions correctly when the page is loaded in desktop mode via the browser's "Request Desktop Site" option.

---

## Attachments

- `screenshot_login_mobile_ios.png` — Login page on iPhone 15
- `screenshot_login_mobile_android.png` — Login page on Samsung Galaxy S23
- `console_error_log.txt` — Browser console output captured via remote DevTools

---

## Suggested Fix

Investigate `login.js` line 42. A DOM element targeted by `addEventListener` is likely `null` due to a selector that returns `null` on mobile viewports (possibly querying a desktop-only element). Ensure the event binding is conditional or the selector targets the correct element across all screen sizes.
