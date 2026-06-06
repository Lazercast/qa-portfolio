# Test Cases: POST /users

**API:** JSONPlaceholder & ReqRes  
**Endpoint:** `POST /users`  
**Tester:** Junior QA Engineer  
**Date:** 2025-06-05  

---

## Summary

| Total | ✅ Positive | ❌ Negative |
|-------|------------|------------|
| 6 | 3 | 3 |

---

## Test Cases

### TC-P001 — POST User: Successful Creation

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P001 |
| **Title** | POST with valid body creates user and returns 201 |
| **Type** | Positive |
| **Priority** | High |
| **Endpoint** | `POST https://jsonplaceholder.typicode.com/users` |

**Request:**
```http
POST /users HTTP/1.1
Host: jsonplaceholder.typicode.com
Content-Type: application/json

{
  "name": "Aizat Bekova",
  "username": "aizat_qa",
  "email": "aizat.bekova@example.com",
  "phone": "+7-700-123-4567",
  "website": "aizat.dev"
}
```

**Steps:**
1. Open Postman, set method to POST
2. Enter URL: `https://jsonplaceholder.typicode.com/users`
3. Go to **Body** → select **raw** → **JSON**
4. Paste request body above
5. Click **Send**

**Expected Result:**
- Status code: `201 Created`
- Response body contains all sent fields
- Response body includes a new `id` field (auto-generated)
- `Content-Type` header is `application/json`

**Expected Response Body:**
```json
{
  "name": "Aizat Bekova",
  "username": "aizat_qa",
  "email": "aizat.bekova@example.com",
  "phone": "+7-700-123-4567",
  "website": "aizat.dev",
  "id": 11
}
```

**Actual Result:** ✅ PASS  
**Notes:** JSONPlaceholder simulates creation; real ID will always be 11 (fake API behavior).

---

### TC-P002 — POST User: Minimum Required Fields

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P002 |
| **Title** | POST with only name and email returns 201 |
| **Type** | Positive |
| **Priority** | Medium |
| **Endpoint** | `POST https://jsonplaceholder.typicode.com/users` |

**Request Body:**
```json
{
  "name": "Test User",
  "email": "test@example.com"
}
```

**Expected Result:**
- Status code: `201 Created`
- Response includes `id`, `name`, `email`

**Actual Result:** ✅ PASS

---

### TC-P003 — POST User on ReqRes: Verify createdAt Field

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P003 |
| **Title** | POST to ReqRes returns createdAt timestamp |
| **Type** | Positive |
| **Priority** | Medium |
| **Endpoint** | `POST https://reqres.in/api/users` |

**Request Body:**
```json
{
  "name": "Aizat Bekova",
  "job": "QA Engineer"
}
```

**Expected Result:**
- Status code: `201 Created`
- Response contains `name`, `job`, `id`, `createdAt`
- `createdAt` is a valid ISO timestamp string

**Actual Result:** ✅ PASS  
**Notes:** `createdAt` format: `2025-06-05T10:22:15.123Z`

---

### TC-P004 — POST User: Empty Body (Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P004 |
| **Title** | POST with empty body — check API behavior |
| **Type** | Negative |
| **Priority** | High |
| **Endpoint** | `POST https://jsonplaceholder.typicode.com/users` |

**Request Body:** (empty `{}`)

**Expected Result:**
- Status code: `400 Bad Request` OR API should not accept empty data
- Body: Error message explaining missing fields

**Actual Result:** ⚠️ PARTIAL FAIL  
**Notes:** JSONPlaceholder returns `201` even with empty body — this is a known limitation of this fake API. Real APIs should return `400`. Documented as known behavior, not a real bug.

---

### TC-P005 — POST User: Invalid Email Format (Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P005 |
| **Title** | POST with invalid email format should be rejected |
| **Type** | Negative |
| **Priority** | High |
| **Endpoint** | `POST https://reqres.in/api/users` |

**Request Body:**
```json
{
  "name": "Bad User",
  "email": "not-a-valid-email"
}
```

**Expected Result:**
- Status code: `400 Bad Request`
- Body contains an error message about invalid email

**Actual Result:** ⚠️ NOTE  
**Notes:** ReqRes does not validate email format (fake API). On real production APIs, this must return `400`. This test is intended to document the concept.

---

### TC-P006 — POST User: Missing Content-Type Header (Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-P006 |
| **Title** | POST without Content-Type header — check behavior |
| **Type** | Negative |
| **Priority** | Medium |
| **Endpoint** | `POST https://jsonplaceholder.typicode.com/users` |

**Request:** Sent without `Content-Type: application/json` header.

**Expected Result:**
- Status code: `415 Unsupported Media Type` OR `400 Bad Request`
- Server should not process request without correct Content-Type

**Actual Result:** ⚠️ NOTE  
**Notes:** JSONPlaceholder accepts it anyway (fake API). In production, missing `Content-Type` should result in `415`. Added for documentation purposes.

---

## Test Execution Summary

| TC ID | Test Name | Type | Result |
|-------|-----------|------|--------|
| TC-P001 | POST with full valid body | Positive | ✅ PASS |
| TC-P002 | POST with minimal fields | Positive | ✅ PASS |
| TC-P003 | POST to ReqRes, verify timestamp | Positive | ✅ PASS |
| TC-P004 | POST with empty body | Negative | ⚠️ API limitation |
| TC-P005 | POST with invalid email | Negative | ⚠️ Fake API, documented |
| TC-P006 | POST without Content-Type | Negative | ⚠️ Documented for real APIs |
