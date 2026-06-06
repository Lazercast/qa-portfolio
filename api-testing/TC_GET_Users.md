# Test Cases: GET /users

**API:** JSONPlaceholder & ReqRes  
**Endpoint:** `GET /users` and `GET /users/{id}`  
**Tester:** Junior QA Engineer  
**Date:** 2025-06-05  

---

## Summary

| Total | ✅ Positive | ❌ Negative |
|-------|------------|------------|
| 8 | 5 | 3 |

---

## Test Cases

### TC-001 — GET All Users: Successful Response

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-001 |
| **Title** | GET all users returns 200 OK with user list |
| **Type** | Positive |
| **Priority** | High |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users` |

**Preconditions:** API is available, no authentication required.

**Request:**
```http
GET /users HTTP/1.1
Host: jsonplaceholder.typicode.com
Accept: application/json
```

**Steps:**
1. Open Postman
2. Set method to GET
3. Enter URL: `https://jsonplaceholder.typicode.com/users`
4. Click **Send**

**Expected Result:**
- Status code: `200 OK`
- Response type: `application/json`
- Body is a JSON array (not empty)
- Each user object contains: `id`, `name`, `username`, `email`, `phone`, `website`, `address`, `company`

**Actual Result:** ✅ PASS  
**Notes:** Returns 10 user objects as expected.

---

### TC-002 — GET Single User by Valid ID

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-002 |
| **Title** | GET user by ID = 1 returns correct user object |
| **Type** | Positive |
| **Priority** | High |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users/1` |

**Request:**
```http
GET /users/1 HTTP/1.1
Host: jsonplaceholder.typicode.com
```

**Steps:**
1. Set method to GET
2. Enter URL: `https://jsonplaceholder.typicode.com/users/1`
3. Click **Send**

**Expected Result:**
- Status code: `200 OK`
- Body is a single JSON object (not array)
- `id` field value equals `1`
- `name` is a non-empty string
- `email` contains `@` symbol

**Sample Expected Response:**
```json
{
  "id": 1,
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.biz",
  "phone": "1-770-736-0860 x56442",
  "website": "hildegard.org",
  "address": { ... },
  "company": { ... }
}
```

**Actual Result:** ✅ PASS

---

### TC-003 — GET User: Verify Required Fields in Response

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-003 |
| **Title** | User response object contains all required fields |
| **Type** | Positive |
| **Priority** | Medium |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users/1` |

**Steps:**
1. Send GET request to `/users/1`
2. Inspect response body

**Expected Result:**
All of the following fields are present and non-null:
- `id` — integer
- `name` — string
- `username` — string
- `email` — string with `@`
- `phone` — string
- `website` — string
- `address` — object with `street`, `city`, `zipcode`
- `company` — object with `name`

**Actual Result:** ✅ PASS

---

### TC-004 — GET User: Response Time is Acceptable

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-004 |
| **Title** | GET /users responds within 2000ms |
| **Type** | Positive (Performance) |
| **Priority** | Medium |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users` |

**Steps:**
1. Send GET /users
2. Check response time in Postman (bottom status bar)

**Expected Result:**
- Response time < 2000ms

**Actual Result:** ✅ PASS — Avg ~350ms  
**Notes:** Tested 3 times; all under 500ms.

---

### TC-005 — GET Users: Content-Type Header is Correct

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-005 |
| **Title** | Response Content-Type is application/json |
| **Type** | Positive |
| **Priority** | Low |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users` |

**Steps:**
1. Send GET /users
2. Check **Headers** tab in Postman response panel

**Expected Result:**
- Header `Content-Type` contains `application/json`

**Actual Result:** ✅ PASS

---

### TC-006 — GET User by Non-existent ID (Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-006 |
| **Title** | GET user with ID = 9999 returns 404 |
| **Type** | Negative |
| **Priority** | High |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users/9999` |

**Request:**
```http
GET /users/9999 HTTP/1.1
Host: jsonplaceholder.typicode.com
```

**Steps:**
1. Set method to GET
2. Enter URL: `https://jsonplaceholder.typicode.com/users/9999`
3. Click **Send**

**Expected Result:**
- Status code: `404 Not Found`
- Body: `{}` (empty object)

**Actual Result:** ✅ PASS  
**Notes:** API correctly returns 404 for non-existent resource.

---

### TC-007 — GET User by String ID (Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-007 |
| **Title** | GET user with string ID returns 404 |
| **Type** | Negative |
| **Priority** | Medium |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users/abc` |

**Steps:**
1. Enter URL: `https://jsonplaceholder.typicode.com/users/abc`
2. Click **Send**

**Expected Result:**
- Status code: `404 Not Found`

**Actual Result:** ✅ PASS  
**Notes:** API does not crash, returns 404 gracefully.

---

### TC-008 — GET User with ID = 0 (Boundary - Negative)

| Field | Detail |
|-------|--------|
| **Test Case ID** | TC-008 |
| **Title** | GET /users/0 returns 404 (boundary value test) |
| **Type** | Negative (Boundary) |
| **Priority** | Low |
| **Endpoint** | `GET https://jsonplaceholder.typicode.com/users/0` |

**Steps:**
1. Enter URL: `https://jsonplaceholder.typicode.com/users/0`
2. Click **Send**

**Expected Result:**
- Status code: `404 Not Found`
- No user with ID 0 should exist

**Actual Result:** ✅ PASS  
**Notes:** IDs start at 1. ID = 0 correctly returns 404.

---

## Test Execution Summary

| TC ID | Test Name | Type | Result |
|-------|-----------|------|--------|
| TC-001 | GET all users — 200 OK | Positive | ✅ PASS |
| TC-002 | GET user by valid ID | Positive | ✅ PASS |
| TC-003 | Verify required fields | Positive | ✅ PASS |
| TC-004 | Response time < 2000ms | Positive | ✅ PASS |
| TC-005 | Content-Type header | Positive | ✅ PASS |
| TC-006 | GET user — ID not found | Negative | ✅ PASS |
| TC-007 | GET user — string ID | Negative | ✅ PASS |
| TC-008 | GET user — ID = 0 | Negative | ✅ PASS |
