# BUG-007 — GET /api/v1/orders Returns 500 Internal Server Error Without Auth Token Instead of 401

---

## Summary

The orders API endpoint (`GET /api/v1/orders`) returns an **HTTP 500 Internal Server Error** when called without a valid `Authorization` header, instead of the expected **401 Unauthorized** response. This indicates the server is crashing during the authentication middleware check rather than handling the missing token gracefully.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-007                          |
| **Title**        | GET /api/v1/orders returns 500 instead of 401 when Authorization header is missing |
| **Type**         | API / Functional                 |
| **Severity**     | High                             |
| **Priority**     | High                             |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-03                       |
| **Assigned To**  | Backend Team                     |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce API (demo)   |
| **API Base URL** | `https://api.demo.shopeasy.io`   |
| **Endpoint**     | `GET /api/v1/orders`             |
| **API Version**  | v1                               |
| **Tool Used**    | Postman v11.0 / cURL             |
| **Auth Type**    | Bearer Token (JWT)               |

---

## Preconditions

- The API server is running and accessible.
- The tester has access to Postman or cURL.
- The endpoint `GET /api/v1/orders` is documented as requiring a valid Bearer token.

---

## Steps to Reproduce

**Using cURL (no Authorization header):**

```bash
curl -X GET https://api.demo.shopeasy.io/api/v1/orders \
  -H "Content-Type: application/json"
```

**Using Postman:**

1. Create a new **GET** request.
2. Set the URL to `https://api.demo.shopeasy.io/api/v1/orders`.
3. Ensure **no** `Authorization` header is set (or remove any existing Bearer token).
4. Click **Send**.
5. Observe the HTTP status code and response body.

**Using cURL (expired/malformed token):**

```bash
curl -X GET https://api.demo.shopeasy.io/api/v1/orders \
  -H "Authorization: Bearer invalid.token.here"
```

---

## Expected Result

**HTTP Status:** `401 Unauthorized`

**Expected Response Body:**
```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Authentication required. Please provide a valid Bearer token."
  }
}
```

---

## Actual Result

**HTTP Status:** `500 Internal Server Error`

**Actual Response Body:**
```json
{
  "success": false,
  "error": "Internal Server Error"
}
```

The server returns a generic 500 error with no useful information. The same 500 response is returned for:
- Missing `Authorization` header
- Malformed Bearer token
- Expired JWT token

---

## Additional Information

**Correct Behaviour (for comparison):**
When a valid, non-expired Bearer token is provided, the endpoint returns `200 OK` with the user's orders — this confirms the endpoint itself functions correctly for authenticated requests.

**Security Concern:**
A 500 error on missing authentication may expose internal server details in error logs or stack traces visible to the client, depending on the server configuration. Even without visible stack traces, 500 errors caused by authentication failures suggest the auth middleware is throwing an unhandled exception rather than returning a controlled error response.

**Error Scenarios Tested:**

| Request Type                         | Expected Status | Actual Status |
|--------------------------------------|-----------------|---------------|
| Valid Bearer token                   | 200 OK          | 200 OK ✓     |
| No Authorization header              | 401             | 500 ✗        |
| `Authorization: Bearer invalid.abc`  | 401             | 500 ✗        |
| `Authorization: Bearer` (empty)      | 401             | 500 ✗        |
| Expired valid JWT token              | 401             | 500 ✗        |

---

## Attachments

- `postman_collection_BUG007.json` — Postman collection with all auth test cases
- `screenshot_500_no_token.png` — Postman response showing 500 status
- `screenshot_200_valid_token.png` — Postman response showing correct 200 status with valid token

---

## Suggested Fix

The authentication middleware should catch all token-related exceptions (missing token, malformed token, expired token, invalid signature) and return a controlled `401 Unauthorized` response rather than allowing the exception to propagate to the global error handler and produce a 500 response.

**Pseudocode example:**
```javascript
function authMiddleware(req, res, next) {
  const authHeader = req.headers['authorization'];

  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({
      success: false,
      error: { code: 'UNAUTHORIZED', message: 'Authentication required.' }
    });
  }

  try {
    const token = authHeader.split(' ')[1];
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    // Catch all JWT errors (expired, malformed, invalid signature)
    return res.status(401).json({
      success: false,
      error: { code: 'UNAUTHORIZED', message: 'Invalid or expired token.' }
    });
  }
}
```
