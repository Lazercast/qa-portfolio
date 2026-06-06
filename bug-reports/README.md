# 🐛 QA Bug Report Portfolio

**Junior QA Engineer Portfolio** — Manual Testing Practice on a Demo E-Commerce Application

---

## About This Repository

This repository contains a collection of professionally written bug reports produced as part of manual QA testing practice. All bugs were identified through exploratory and structured testing of a demo e-commerce web application and its REST API.

The reports demonstrate skills in:
- Functional, UI, validation, API, and performance testing
- Writing clear, reproducible steps to reproduce
- Communicating impact and severity to development teams
- API testing using Postman and cURL
- Mobile and cross-browser testing
- Security-aware testing mindset

---

## Bug Report Index

| Bug ID | Title | Type | Severity | Status |
|--------|-------|------|----------|--------|
| [BUG-001](./BUG-001_Login_Button_Unresponsive_On_Mobile.md) | Login button unresponsive on mobile devices | Functional / Mobile | Critical | Open |
| [BUG-002](./BUG-002_API_Returns_200_For_Invalid_Credentials.md) | POST /api/v1/auth/login returns 200 for invalid credentials | API | High | Open |
| [BUG-003](./BUG-003_Registration_Accepts_Invalid_Email_Format.md) | Registration form accepts invalid email formats | Validation | High | Open |
| [BUG-004](./BUG-004_Cart_Quantity_Update_Does_Not_Recalculate_Total.md) | Cart quantity update does not recalculate total price | Functional | High | Open |
| [BUG-005](./BUG-005_Navigation_Overflow_On_Tablet_Viewport.md) | Navigation menu overflows on tablet viewport (768px–1024px) | UI / Responsive | Medium | Open |
| [BUG-006](./BUG-006_Password_Field_Displays_Plain_Text_On_Registration.md) | Registration password field displays plain text | UI / Security | High | Open |
| [BUG-007](./BUG-007_API_Returns_500_Instead_Of_401_Missing_Auth_Token.md) | GET /api/v1/orders returns 500 instead of 401 without auth | API | High | Open |
| [BUG-008](./BUG-008_Checkout_Button_Enabled_On_Empty_Cart.md) | Checkout button enabled and functional on empty cart | UI / Functional | Medium | Open |
| [BUG-009](./BUG-009_Search_Results_Page_Slow_Load_Performance.md) | Search results page takes 8–12 seconds to load | Performance | Medium | Open |
| [BUG-010](./BUG-010_Login_Error_Reveals_Email_Registration_Status.md) | Login error reveals whether email is registered (enumeration) | Validation / Security | Medium | Open |

---

## Coverage Summary

### By Bug Type

| Type              | Count | Bug IDs                    |
|-------------------|-------|----------------------------|
| Functional        | 3     | BUG-001, BUG-004, BUG-008  |
| API               | 2     | BUG-002, BUG-007           |
| UI                | 2     | BUG-005, BUG-006           |
| Validation        | 2     | BUG-003, BUG-010           |
| Performance       | 1     | BUG-009                    |

### By Severity

| Severity | Count | Bug IDs                              |
|----------|-------|--------------------------------------|
| Critical | 1     | BUG-001                              |
| High     | 5     | BUG-002, BUG-003, BUG-004, BUG-006, BUG-007 |
| Medium   | 4     | BUG-005, BUG-008, BUG-009, BUG-010  |
| Low      | 0     | —                                    |

### By Application Area

| Area                    | Bug IDs               |
|-------------------------|-----------------------|
| Login / Authentication  | BUG-001, BUG-002, BUG-010 |
| Registration            | BUG-003, BUG-006      |
| Shopping Cart           | BUG-004, BUG-008      |
| API Endpoints           | BUG-002, BUG-007      |
| UI / Responsiveness     | BUG-005, BUG-006      |
| Search / Performance    | BUG-009               |

---

## Bug Report Template

Each bug report follows this standard structure:

```
- Bug ID
- Title
- Type / Severity / Priority / Status
- Environment (Browser, OS, Device, URL)
- Preconditions
- Steps to Reproduce
- Expected Result
- Actual Result
- Additional Information (console errors, API responses, test data tables)
- Attachments (screenshots, Postman collections, logs)
- Suggested Fix
```

---

## Tools & Skills Demonstrated

| Tool / Skill             | Used In           |
|--------------------------|-------------------|
| Postman (API testing)    | BUG-002, BUG-007  |
| cURL (API testing)       | BUG-002, BUG-007  |
| Chrome DevTools          | BUG-001, BUG-005, BUG-006, BUG-009 |
| Lighthouse (Performance) | BUG-009           |
| Mobile / Responsive Testing | BUG-001, BUG-005 |
| Cross-browser Testing    | BUG-003, BUG-004  |
| Security-aware Testing   | BUG-006, BUG-010  |
| HTTP Status Code Knowledge | BUG-002, BUG-007 |
| REST API Testing         | BUG-002, BUG-007  |

---

## Application Under Test

- **Name:** ShopEasy E-Commerce (Demo)
- **Type:** E-commerce web application with REST API
- **Scope:** Public-facing website and API (demo/staging environment)

---

## About Me

Junior QA Engineer with a focus on manual testing, API testing, and building a professional testing portfolio.

📧 your.email@example.com
🔗 [LinkedIn Profile](https://linkedin.com/in/yourprofile)

---

*All bug reports in this repository were written for portfolio and practice purposes against a demo application.*
