# 🧪 QA API Testing Portfolio

<div align="center">

![QA Engineer](https://img.shields.io/badge/Role-Junior%20QA%20Engineer-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Looking-brightgreen?style=for-the-badge)
![Goal](https://img.shields.io/badge/Goal-Kolesa%20Academy%20Internship-orange?style=for-the-badge)

*A hands-on API testing portfolio demonstrating real-world QA skills using industry-standard tools.*

</div>

---

## 👤 About Me

Hi! I'm a beginner QA Engineer passionate about software quality and testing. I am actively building my skills in **API testing**, **test case design**, and **bug reporting** to prepare for my first internship in QA.

I believe quality software starts with thorough testing — and I'm here to learn, grow, and contribute.

- 🎯 **Goal:** Junior QA Internship / Kolesa Academy
- 📍 **Location:** Kazakhstan
- 📚 **Currently learning:** Postman, REST API testing, test design techniques

---

## 🛠️ Skills

| Category | Skills |
|----------|--------|
| **API Testing** | REST API, HTTP Methods, Status Codes, JSON |
| **Tools** | Postman, Newman, Git, GitHub |
| **Test Design** | Positive/Negative testing, Boundary value analysis |
| **Documentation** | Test cases, Bug reports, API notes |
| **Other** | Markdown, Basic JSON validation |

---

## 🔧 Tools Used

- **[Postman](https://www.postman.com/)** — API testing and collection management
- **[JSONPlaceholder](https://jsonplaceholder.typicode.com/)** — Free fake REST API for testing
- **[ReqRes](https://reqres.in/)** — Hosted REST API for testing
- **Git & GitHub** — Version control and portfolio hosting
- **Markdown** — Documentation

---

## 🌐 APIs Tested

### 1. JSONPlaceholder (`https://jsonplaceholder.typicode.com/`)
A free, public fake API with realistic data — perfect for practicing GET, POST, PUT, and DELETE requests.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/users` | GET | Get all users |
| `/users/{id}` | GET | Get user by ID |
| `/posts` | GET | Get all posts |
| `/posts/{id}` | GET | Get post by ID |
| `/users` | POST | Create a new user |
| `/users/{id}` | PUT | Update a user |
| `/users/{id}` | DELETE | Delete a user |

### 2. ReqRes (`https://reqres.in/`)
A hosted REST API with support for authentication simulation and user management.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/users` | GET | Get paginated users |
| `/api/users/{id}` | GET | Get single user |
| `/api/users` | POST | Create a user |
| `/api/users/{id}` | PUT | Update a user |
| `/api/users/{id}` | DELETE | Delete a user |
| `/api/login` | POST | Login simulation |

---

## 📁 Portfolio Contents

```
qa-api-portfolio/
│
│
├── 📂 test-cases/
│   ├── TC_GET_Users.md                     ← Test cases for GET /users
│   ├── TC_POST_User.md                     ← Test cases for POST /users
│   ├── TC_PUT_User.md                      ← Test cases for PUT /users
│   └── TC_DELETE_User.md                   ← Test cases for DELETE /users
│
├── 📂 bug-reports/
│   ├── BUG-001_Wrong_Status_Code.md        ← Bug: unexpected status code
│   ├── BUG-002_Missing_Field.md            ← Bug: missing field in response
│   ├── BUG-003_Invalid_JSON.md             ← Bug: malformed JSON structure
│   └── BUG-004_Slow_Response.md            ← Bug: performance issue
│
├── 📂 api-notes/
│   ├── HTTP_Methods.md                     ← Notes on GET, POST, PUT, DELETE
│   ├── Status_Codes.md                     ← Common HTTP status codes
│   ├── REST_API_Basics.md                  ← What is REST API?
│   └── JSON_Basics.md                      ← JSON structure and syntax
│
├── 📂 screenshots/
│   └── README.md                           ← Guide on screenshots to add
│
└── 📄 README.md                            ← This file
```

---

## 🧪 Sample Test: GET /users

**Request:**
```
GET https://jsonplaceholder.typicode.com/users
```

**Expected Response:**
- Status Code: `200 OK`
- Response type: JSON array
- Each object contains `id`, `name`, `email`, `username`

**Sample Response Body:**
```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "username": "Bret",
    "email": "Sincere@april.biz",
    "phone": "1-770-736-0860 x56442",
    "website": "hildegard.org"
  }
]
```

**Test Result:** ✅ PASS

---

## 🐛 Sample Bug Report

**BUG-001 | Incorrect Status Code on DELETE**

| Field | Detail |
|-------|--------|
| **Title** | DELETE /users/{id} returns 404 instead of 200 |
| **Severity** | High |
| **Status** | Open |
| **Endpoint** | `DELETE https://reqres.in/api/users/999` |
| **Expected** | `200 OK` or `404 Not Found` with error message |
| **Actual** | `404 Not Found` with empty body |

---

## 📈 Progress Tracker

- [x] Set up Postman and created first collection
- [x] Tested GET endpoints on JSONPlaceholder
- [x] Tested POST, PUT, DELETE with request bodies
- [x] Written test cases (positive + negative)
- [x] Written bug reports
- [x] Created API testing notes
- [ ] Add Postman test scripts (JavaScript assertions)
- [ ] Learn Newman for CLI test runs
- [ ] Add CI/CD pipeline integration

---

## 🚀 How to Use This Portfolio

1. **Clone the repo:**
   ```bash
   git clone https://github.com/Lazercast/qa-portfolio.git
   ```

2. **Import Postman Collections:**
   - Open Postman
   - Click **Import**
   - Select files from `/collections/` folder

3. **Run the tests:**
   - Select a collection
   - Click **Run Collection**
   - Review results

---

## 📬 Contact

> 💡 *This portfolio is a work in progress. I update it regularly as I learn new QA skills.*

---

<div align="center">

Made with ❤️ by a Junior QA Engineer in training

</div>
