# ✅ QA Test Case Portfolio

**Junior QA Engineer Portfolio** — Manual Testing Practice on a Demo E-Commerce Application & Public REST APIs

---

## About This Repository

This repository contains a collection of professionally written manual test cases produced as part of QA testing practice. Test cases cover a demo e-commerce web application (`demo.shopeasy.io`) and two public REST APIs (`jsonplaceholder.typicode.com` and `reqres.in`).

The cases demonstrate skills in:
- Functional, UI, validation, API, and mobile responsiveness testing
- Writing clear, step-by-step test procedures
- Defining precise expected results and acceptance criteria
- Designing both positive and negative test scenarios
- Input validation and boundary value testing
- REST API testing using Postman and cURL
- Cross-device and responsive layout testing

---

## Test Case Index

| ID | Title | Module | Type | Priority | Status |
|----|-------|--------|------|----------|--------|
| [TC-001](./TC-001_Valid_Login.md) | Valid login with correct credentials | Login | Positive | High | ✅ Pass |
| [TC-002](./TC-002_Invalid_Password_Login.md) | Login with incorrect password | Login | Negative | High | ✅ Pass |
| [TC-003](./TC-003_Registration_Empty_Fields.md) | Registration with all fields empty | Registration | Negative / Validation | High | ✅ Pass |
| [TC-004](./TC-004_Password_Reset_Valid_Email.md) | Password reset with valid registered email | Password Reset | Positive | High | ✅ Pass |
| [TC-005](./TC-005_Add_Item_To_Cart.md) | Add single product to cart and verify total | Shopping Cart | Positive | High | ✅ Pass |
| [TC-006](./TC-006_Search_Valid_Keyword.md) | Search returns relevant results for valid keyword | Search | Positive | High | ✅ Pass |
| [TC-007](./TC-007_Search_Special_Characters.md) | Search handles special characters and boundary inputs | Search / Validation | Negative / Boundary | Medium | ✅ Pass |
| [TC-008](./TC-008_API_GET_Request_Validation.md) | GET /posts/{id} returns 200 with correct JSON | API — GET | Positive / API | High | ✅ Pass |
| [TC-009](./TC-009_API_POST_Request_Validation.md) | POST /api/users creates user and returns 201 | API — POST | Positive / API | High | ✅ Pass |
| [TC-010](./TC-010_Mobile_Responsiveness_Login_Page.md) | Login page layout correct on mobile viewports | Mobile / UI | Positive / UI | High | ✅ Pass |

---

## Coverage Summary

### By Test Type

| Type               | Count | Test Case IDs              |
|--------------------|-------|----------------------------|
| Positive           | 6     | TC-001, TC-004, TC-005, TC-006, TC-008, TC-009 |
| Negative           | 3     | TC-002, TC-003, TC-007     |
| Validation         | 2     | TC-003, TC-007             |
| Boundary Value     | 1     | TC-007                     |
| API                | 2     | TC-008, TC-009             |
| UI / Responsive    | 2     | TC-007 (partial), TC-010   |

### By Priority

| Priority | Count | Test Case IDs                                        |
|----------|-------|------------------------------------------------------|
| High     | 9     | TC-001 – TC-006, TC-008, TC-009, TC-010              |
| Medium   | 1     | TC-007                                               |
| Low      | 0     | —                                                    |

### By Application Module

| Module              | Test Case IDs             |
|---------------------|---------------------------|
| Login               | TC-001, TC-002, TC-010    |
| Registration        | TC-003                    |
| Password Reset      | TC-004                    |
| Shopping Cart       | TC-005                    |
| Search              | TC-006, TC-007            |
| API (GET)           | TC-008                    |
| API (POST)          | TC-009                    |
| Mobile / UI         | TC-010                    |

---

## Test Case Template

Each test case follows this standard structure:

```
- Test Case ID
- Title
- Module / Type / Priority / Status
- Environment
- Preconditions
- Test Steps (table with action + expected outcome per step)
- Test Data
- Expected Result
- Actual Result
- Additional checklists or matrices where applicable
- Notes
```

---

## APIs Tested

| API | Base URL | Used In |
|-----|----------|---------|
| JSONPlaceholder | `https://jsonplaceholder.typicode.com` | TC-008 |
| Reqres | `https://reqres.in` | TC-009 |
| ShopEasy Demo API | `https://api.demo.shopeasy.io` | TC-001 – TC-007, TC-010 |

---

## Tools & Skills Demonstrated

| Tool / Skill                    | Used In                    |
|---------------------------------|----------------------------|
| Postman (API testing)           | TC-008, TC-009             |
| Chrome DevTools (responsive)    | TC-010                     |
| Chrome DevTools (Network tab)   | TC-003, TC-005             |
| Boundary value analysis         | TC-007                     |
| Equivalence partitioning        | TC-007                     |
| Cross-device testing (physical) | TC-010                     |
| Security-aware testing          | TC-007 (XSS / SQLi checks) |
| HTTP status code verification   | TC-008, TC-009             |
| JSON schema validation          | TC-008, TC-009             |
| Postman test scripts (JS)       | TC-008, TC-009             |

---

## Related Repository

This test case portfolio is paired with a **Bug Report Portfolio** containing 10 professional bug reports discovered during the same testing cycle:

👉 [QA Bug Report Portfolio](../qa-bug-reports/README.md)

---

## About Me

Junior QA Engineer with a focus on manual testing, API testing, and building a professional testing portfolio.

📧 muhit7nisanov@gmail.com
🔗 [LinkedIn Profile](www.linkedin.com/in/mukhit-nishanov-ba9846386)

---

*All test cases in this repository were written for portfolio and practice purposes against a demo application and public mock APIs.*
