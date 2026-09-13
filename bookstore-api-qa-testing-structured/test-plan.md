# Test Plan

**Project:** Bookstore API

**Repository:** Xmwo3i/Bookstore-API

**Application Type**: RESTful API

**Technology:** Node.js, Express.js, JSON file storage

**Testing Tools:** Postman, Jest, Supertest

**Local Environment:** http://localhost:4000

**Objective:**

To validate the functionality, reliability, input validation, error handling, security, and

REST API behavior of the Bookstore API. Testing will cover Books, Authors, and Users

endpoints using functional, positive, negative, regression, security, penetration, unit,

and API testing approaches.

**Scope (In-Scope):**

- Books API, Authors API, Users API

- CRUD operations (Create, Read, Update, Delete)

- Input validation and error handling

- HTTP status code accuracy

- API response structure

- Basic security and penetration testing (authentication bypass, injection, exposed secrets)

- Unit/integration test coverage

- Regression testing following defect fixes

**Out-of-Scope**:

- UI/frontend testing (API-only project)

- Load/performance/stress testing

- \[State auth testing scope explicitly, or note if API has no auth layer\]

- Production/staging environment testing (local environment only)

**Entry Criteria:**

- Application runs successfully in local environment

- Test scenarios and test cases documented prior to execution

**Exit Criteria:**

- All high-priority test cases executed

- All identified defects documented with severity and status

- Test summary/closure report completed

**Risks:**

- Shared JSON file storage may not reliably support concurrent read/write operations

- Limited time (3 days) may constrain full penetration testing depth

**Deliverables:**

- Test scenarios and test cases

- Postman collection

- Bug reports

- Automated unit test suite

- Test execution evidence (screenshots/logs)

- Test summary/closure report
