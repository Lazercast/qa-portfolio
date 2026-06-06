# TC-008 — API GET Request Returns Correct Status Code and Valid JSON Response

---

## Test Case Details

| Field              | Details                                       |
|--------------------|-----------------------------------------------|
| **Test Case ID**   | TC-008                                        |
| **Title**          | GET /posts/{id} returns 200 OK with correct JSON structure |
| **Module**         | API Testing — GET Request                     |
| **Type**           | Positive / API                                |
| **Priority**       | High                                          |
| **Status**         | Pass                                          |
| **Tested By**      | QA Engineer                                   |
| **Date Tested**    | 2025-06-03                                    |
| **Environment**    | Postman v11.0 / Windows 11                    |
| **API Under Test** | JSONPlaceholder — `https://jsonplaceholder.typicode.com` |

---

## Preconditions

- Postman is installed and open.
- An active internet connection is available.
- No authentication is required for this public API.
- The tester is familiar with reading JSON responses.

---

## Test Steps

| # | Action | Expected Outcome |
|---|--------|-----------------|
| 1 | Open Postman and create a new **GET** request | New request tab is open |
| 2 | Set the request URL to `https://jsonplaceholder.typicode.com/posts/1` | URL is entered correctly |
| 3 | Ensure no Authorization headers are set | Request will be sent without auth |
| 4 | Click **Send** | Request is sent to the server |
| 5 | Check the **HTTP status code** in the response panel | Status code is displayed |
| 6 | Check the **response time** in Postman | Response time is displayed in milliseconds |
| 7 | Check the **Content-Type** header in the Response → Headers tab | `Content-Type` header is present |
| 8 | Review the **response body** in the Body tab | JSON data is displayed |
| 9 | Validate the JSON structure includes all expected fields | `userId`, `id`, `title`, `body` fields present |
| 10 | Validate the data types of each field | `id` and `userId` are integers; `title` and `body` are strings |
| 11 | Verify `id` in the response matches the requested ID (`1`) | `"id": 1` in the response body |

---

## Test Data

| Parameter      | Value                                                    |
|----------------|----------------------------------------------------------|
| Method         | GET                                                      |
| URL            | `https://jsonplaceholder.typicode.com/posts/1`           |
| Headers        | None required                                            |
| Request Body   | None (GET request)                                       |

---

## Expected Result

**HTTP Status Code:** `200 OK`

**Response Headers include:**
```
Content-Type: application/json; charset=utf-8
```

**Response Body (exact):**
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

**Validations:**
- Status code: `200`
- `id` is an integer equal to `1`
- `userId` is an integer
- `title` is a non-empty string
- `body` is a non-empty string
- Response time: under `500ms`

---

## Actual Result

> ✅ **Pass** — Status `200 OK` received. Response body matched expected JSON structure exactly. All fields present with correct data types. `id: 1` confirmed. Response time: 184ms. `Content-Type: application/json; charset=utf-8` confirmed.

---

## Response Validation Checklist

| Validation Check                   | Expected          | Actual            | Result   |
|------------------------------------|-------------------|-------------------|----------|
| HTTP Status Code                   | 200               | 200               | ✅ Pass  |
| Content-Type header                | application/json  | application/json  | ✅ Pass  |
| Field present: `userId`            | Yes (integer)     | Yes — `1`         | ✅ Pass  |
| Field present: `id`                | Yes (integer = 1) | Yes — `1`         | ✅ Pass  |
| Field present: `title`             | Yes (string)      | Yes               | ✅ Pass  |
| Field present: `body`              | Yes (string)      | Yes               | ✅ Pass  |
| Response time                      | < 500ms           | 184ms             | ✅ Pass  |
| Response is valid JSON             | Yes               | Yes               | ✅ Pass  |

---

## Additional Tests Performed

| Endpoint                                              | Expected Status | Actual Status | Notes                         |
|-------------------------------------------------------|-----------------|---------------|-------------------------------|
| `GET /posts/1`                                        | 200             | 200 ✅        | Valid resource                |
| `GET /posts/100`                                      | 200             | 200 ✅        | Last valid post (boundary)    |
| `GET /posts/101`                                      | 404             | 404 ✅        | Resource does not exist       |
| `GET /posts/0`                                        | 404             | 404 ✅        | Zero ID — invalid resource    |
| `GET /posts/abc`                                      | 404             | 404 ✅        | Non-numeric ID                |

---

## Notes

- JSONPlaceholder is a free, public REST API used for testing and prototyping. Data is fake and not persisted.
- Postman's built-in test runner can automate these checks using the **Tests** tab with JavaScript assertions.

**Example Postman Test Script:**
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has correct id", function () {
    const json = pm.response.json();
    pm.expect(json.id).to.eql(1);
});

pm.test("Response has required fields", function () {
    const json = pm.response.json();
    pm.expect(json).to.have.property("userId");
    pm.expect(json).to.have.property("title");
    pm.expect(json).to.have.property("body");
});
```
