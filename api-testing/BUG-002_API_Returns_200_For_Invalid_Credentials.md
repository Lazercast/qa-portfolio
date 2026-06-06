# BUG-002 — POST /api/v1/auth/login Returns 200 OK for Invalid Credentials

---

## Summary

The authentication API endpoint returns an HTTP **200 OK** status code when a user submits incorrect credentials, instead of the correct **401 Unauthorized** response. The response body contains an `"error"` field, but HTTP clients and middleware relying on status codes for error handling will incorrectly treat this as a successful request.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-002                          |
| **Title**        | POST /api/v1/auth/login returns 200 OK for invalid credentials |
| **Type**         | API / Functional                 |
| **Severity**     | High                             |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-01                       |
| **Assigned To**  | Backend Team                     |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce API (demo)   |
| **API Base URL** | `https://api.demo.shopeasy.io`   |
| **Endpoint**     | `POST /api/v1/auth/login`        |
| **API Version**  | v1                               |
| **Tool Used**    | Postman v11.0 / cURL             |
| **Auth**         | None (public endpoint)           |

---

## Preconditions

- The API server is running and accessible.
- A registered user account exists with email `testuser@example.com`.
- The tester has access to Postman or cURL.
- API base URL is reachable (no VPN or firewall blocks).

---

## Steps to Reproduce

**Using cURL:**

```bash
curl -X POST https://api.demo.shopeasy.io/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "testuser@example.com",
    "password": "WrongPassword123!"
  }'
```

**Using Postman:**

1. Open Postman and create a new **POST** request.
2. Set the URL to `https://api.demo.shopeasy.io/api/v1/auth/login`.
3. Set the **Body** to `raw` → `JSON`.
4. Enter the following payload:
   ```json
   {
     "email": "testuser@example.com",
     "password": "WrongPassword123!"
   }
   ```
5. Click **Send**.
6. Observe the HTTP status code and response body.

---

## Expected Result

**HTTP Status:** `401 Unauthorized`

**Expected Response Body:**
```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "The email or password you entered is incorrect."
  }
}
```

---

## Actual Result

**HTTP Status:** `200 OK` ← **Incorrect**

**Actual Response Body:**
```json
{
  "success": false,
  "error": "Invalid email or password",
  "token": null
}
```

The server returns a `200 OK` status despite authentication failure. The body correctly indicates failure via the `"success": false` field, but HTTP status code semantics are violated.

---

## Additional Information

- **Successful login** (correct credentials) also returns `200 OK` with `"success": true` and a JWT token — this behaviour is correct.
- The incorrect status code for failed logins can cause issues with:
  - API gateway error logging (gateways often only log non-2xx responses as errors)
  - Frontend interceptors that check status codes rather than body content
  - Security monitoring tools that flag authentication failures based on HTTP 401 responses
- Verified with **Postman**, **cURL**, and **Insomnia** — all show `200 OK` for invalid credentials.

---

## Test Data

| Email                    | Password             | Expected Status | Actual Status |
|--------------------------|----------------------|-----------------|---------------|
| testuser@example.com     | WrongPassword123!    | 401             | 200 ✗         |
| nonexistent@example.com  | AnyPassword1!        | 401             | 200 ✗         |
| testuser@example.com     | CorrectPassword1!    | 200             | 200 ✓         |

---

## Attachments

- `postman_collection_BUG002.json` — Postman collection with all test cases
- `screenshot_200_response.png` — Postman screenshot showing incorrect 200 status

---

## Suggested Fix

Update the authentication controller to return HTTP `401 Unauthorized` when credentials are invalid. Per [RFC 9110 §15.5.2](https://www.rfc-editor.org/rfc/rfc9110#section-15.5.2), 401 is the correct status for failed authentication. The fix should be applied consistently to all authentication-related failure scenarios.
