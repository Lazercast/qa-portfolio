# TC-009 — API POST Request Creates a New User and Returns Correct Response

---

## Test Case Details

| Field              | Details                                       |
|--------------------|-----------------------------------------------|
| **Test Case ID**   | TC-009                                        |
| **Title**          | POST /api/users creates a new user and returns 201 Created with correct response body |
| **Module**         | API Testing — POST Request                    |
| **Type**           | Positive / API                                |
| **Priority**       | High                                          |
| **Status**         | Pass                                          |
| **Tested By**      | QA Engineer                                   |
| **Date Tested**    | 2025-06-04                                    |
| **Environment**    | Postman v11.0 / Windows 11                    |
| **API Under Test** | Reqres — `https://reqres.in`                  |

---

## Preconditions

- Postman is installed and open.
- An active internet connection is available.
- No authentication token is required for this public mock API.
- The tester understands JSON request body formatting.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open Postman and create a new **POST** request | New request tab is open |
| 2 | Set the request URL to `https://reqres.in/api/users` | URL is entered correctly |
| 3 | Go to the **Headers** tab and add `Content-Type: application/json` | Header is set |
| 4 | Go to the **Body** tab, select **raw**, and choose **JSON** from the dropdown | Body editor is set to JSON mode |
| 5 | Enter the request body from Test Data | JSON body is entered correctly |
| 6 | Click **Send** | Request is sent |
| 7 | Check the **HTTP status code** | Status code is displayed |
| 8 | Review the **response body** | JSON response is visible |
| 9 | Verify the `name` field in the response matches the request | Name value is echoed back |
| 10 | Verify the `job` field in the response matches the request | Job value is echoed back |
| 11 | Verify the response contains an `id` field | A new user ID has been generated |
| 12 | Verify the response contains a `createdAt` timestamp | Timestamp is present and in ISO 8601 format |

---

## Test Data

**Request:**

| Field          | Value                             |
|----------------|-----------------------------------|
| Method         | POST                              |
| URL            | `https://reqres.in/api/users`     |
| Content-Type   | `application/json`                |

**Request Body:**
```json
{
  "name": "Jane Doe",
  "job": "QA Engineer"
}
```

---

## Expected Result

**HTTP Status Code:** `201 Created`

**Response Headers include:**
```
Content-Type: application/json; charset=utf-8
```

**Response Body:**
```json
{
  "name": "Jane Doe",
  "job": "QA Engineer",
  "id": "496",
  "createdAt": "2025-06-04T10:23:41.892Z"
}
```

*(Note: `id` and `createdAt` values will differ on each request — validate presence and format, not exact value.)*

**Validations:**
- Status code is `201`
- `name` equals `"Jane Doe"` (echoed from request)
- `job` equals `"QA Engineer"` (echoed from request)
- `id` is present and is a non-empty string
- `createdAt` is present and matches ISO 8601 format (`YYYY-MM-DDTHH:mm:ss.sssZ`)
- Response time is under `1000ms`

---

## Actual Result

> ✅ **Pass** — Status `201 Created` received. `name` and `job` fields matched request values exactly. `id` was present as a non-empty string (`"496"`). `createdAt` was in valid ISO 8601 format. Response time: 312ms.

---

## Response Validation Checklist

| Validation Check                        | Expected              | Actual               | Result   |
|-----------------------------------------|-----------------------|----------------------|----------|
| HTTP Status Code                        | 201                   | 201                  | ✅ Pass  |
| Content-Type header                     | application/json      | application/json     | ✅ Pass  |
| Field `name` echoed from request        | "Jane Doe"            | "Jane Doe"           | ✅ Pass  |
| Field `job` echoed from request         | "QA Engineer"         | "QA Engineer"        | ✅ Pass  |
| Field `id` present (non-empty string)   | Yes                   | Yes — "496"          | ✅ Pass  |
| Field `createdAt` present (ISO 8601)    | Yes                   | Yes                  | ✅ Pass  |
| Response time                           | < 1000ms              | 312ms                | ✅ Pass  |
| Response is valid JSON                  | Yes                   | Yes                  | ✅ Pass  |

---

## Negative API Test Cases (Additional)

| Scenario                               | Request Body                          | Expected Status | Actual Status | Notes                      |
|----------------------------------------|---------------------------------------|-----------------|---------------|----------------------------|
| Empty body                             | `{}`                                  | 201             | 201 ✅        | API accepts; fields absent in response |
| Missing `name` field                   | `{"job": "QA Engineer"}`              | 201             | 201 ✅        | Reqres is permissive by design        |
| Invalid JSON body                      | `{name: Jane Doe}` (malformed)        | 400             | 400 ✅        | Bad request — invalid JSON           |
| Wrong HTTP method — GET on `/api/users`| —                                     | 200             | 200 ✅        | Returns list of users                |

---

## Postman Test Script

```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Name is echoed correctly", function () {
    const json = pm.response.json();
    pm.expect(json.name).to.eql("Jane Doe");
});

pm.test("Job is echoed correctly", function () {
    const json = pm.response.json();
    pm.expect(json.job).to.eql("QA Engineer");
});

pm.test("ID is present and non-empty", function () {
    const json = pm.response.json();
    pm.expect(json.id).to.be.a("string").and.not.empty;
});

pm.test("createdAt is present", function () {
    const json = pm.response.json();
    pm.expect(json).to.have.property("createdAt");
});

pm.test("Response time is under 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

---

## Notes

- Reqres is a public hosted mock REST API that simulates real-world REST API behaviour for testing purposes. Data created via POST is not permanently stored.
- The `id` is dynamically generated per request and will differ between runs — test scripts should validate presence and type, not the exact value.
