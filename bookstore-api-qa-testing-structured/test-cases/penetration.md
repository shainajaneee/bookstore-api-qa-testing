# Penetration Test Cases

## **TC-PEN-001: Access and Modify Resources Without Authentication**

**Related Scenario ID:** TS-PEN-001  
**Test Type:** Penetration/Access Control  
**Priority:** High  
**Target Endpoints:**

- GET /users

- POST /users

- PUT /users/{id}

- DELETE /users/{id}

### **Objective**

Determine whether user records can be accessed, created, modified, and deleted without authentication or authorization.

### **Preconditions**

- The API is running at http://localhost:4000.

- No authorization token or authentication cookie is included.

- A disposable user record is available.

- The project’s authentication requirements have been reviewed.

### **Test Data**

{

"name": "Penetration Test User",

"email": "pentest@example.com"

}

### **Steps**

- ~~Open Postman.~~

- ~~Remove any Authorization header.~~

- ~~Send GET http://localhost:4000/users.~~

- ~~Record the status code and response.~~

- ~~Send POST /users using the test payload.~~

- ~~Record the generated user ID.~~

- ~~Send PUT /users/{id} using the generated ID.~~

- ~~Send DELETE /users/{id} using the same disposable ID.~~

- ~~Record the result of every operation.~~

### **Expected Result**

If the endpoints are required to be protected, the API should return 401 Unauthorized or 403 Forbidden and should not expose or modify records.

If authentication is outside the repository’s intended scope, unrestricted access should be documented as a **security limitation or observation**, not automatically as a confirmed defect.

## **TC-PEN-002: Access Another User by Manipulating the ID**

**Related Scenario ID:** TS-PEN-002  
**Test Type:** Penetration/IDOR  
**Priority:** High  
**Endpoint:** GET /users/{id}

### **Objective**

Determine whether changing the ID in the request allows access to another user’s record without authorization.

### **Preconditions**

- At least two user records exist.

- Their user IDs are known.

- No authorization credentials are provided.

### **Test Data**

GET /users/1

GET /users/2

Replace the IDs with confirmed existing IDs.

### **Steps**

- ~~Send GET /users/1.~~

- ~~Record the returned user information.~~

- ~~Change the endpoint to GET /users/2.~~

- ~~Send the second request.~~

- ~~Determine whether the second user’s data is returned.~~

- ~~Check whether the API performs an authorization check.~~

### **Expected Result**

In an authenticated system, users should not access another user’s protected record without permission. The API should return 403 Forbidden or 404 Not Found.

If the project intentionally has no user ownership or authentication model, mark the result **Not Applicable** or record it as a design limitation.

## **TC-PEN-003: Submit Unexpected Privileged User Fields**

**Related Scenario ID:** TS-PEN-003  
**Test Type:** Penetration/Mass Assignment  
**Priority:** High  
**Endpoint:** POST /users

### **Objective**

Determine whether the API accepts unexpected security-sensitive fields during user creation.

### **Test Data**

{

"name": "Privilege Test User",

"email": "privilege-test@example.com",

"role": "admin",

"isAdmin": true

}

### **Preconditions**

- The API is running.

- The expected Users data structure has been reviewed.

- role and isAdmin are not normal user-input fields.

### **Steps**

- ~~Record the existing user collection.~~

- ~~Select POST.~~

- ~~Enter http://localhost:4000/users.~~

- ~~Add the test payload.~~

- ~~Click **Send**.~~

- ~~Record the status and response.~~

- ~~If the user is created, record its ID.~~

- ~~Send GET /users/{id}.~~

- ~~Check whether role or isAdmin was stored.~~

- ~~Delete the disposable record after documenting the result.~~

### **Expected Result**

The API should reject or ignore unexpected privileged properties. The fields must not grant administrative privileges or modify the intended user structure.

## **TC-PEN-004: Manipulate Resource IDs**

**Related Scenario ID:** TS-PEN-004  
**Test Type:** Penetration/Parameter Manipulation  
**Priority:** Medium  
**Endpoint:** GET /books/{id}

### **Objective**

Verify that negative, zero, alphabetic, and extremely large IDs are handled safely.

### **Test Data**

GET /books/-1

GET /books/0

GET /books/abc

GET /books/999999999999999999

### **Steps**

- ~~Send GET /books/-1.~~

- ~~Record the status and response.~~

- ~~Repeat using 0, abc, and the extremely large number.~~

- ~~Check for 500 Internal Server Error.~~

- ~~Check for stack traces, file paths, or technical details.~~

- ~~Send GET /books afterward.~~

- ~~Confirm that the API remains responsive.~~

### **Expected Result**

The API should return a controlled 400 Bad Request or 404 Not Found. It should not crash, return an unrelated record, or expose internal server information.

## **TC-PEN-005: Submit an Injection-Like Payload**

**Related Scenario ID:** TS-PEN-005  
**Test Type:** Penetration/Injection Testing  
**Priority:** High  
**Endpoint:** POST /users

### **Objective**

Determine whether injection-like input can alter the intended API behavior, expose records, or cause an internal server error.

### **Test Data**

{

"name": "' OR '1'='1",

"email": "injection-test@example.com"

}

### **Preconditions**

- The initial user collection is recorded.

- The test is performed only against the local API.

- A disposable email address is used.

### **Steps**

- ~~Send GET /users and record the existing users.~~

- ~~Select POST /users.~~

- ~~Enter the test payload.~~

- ~~Click **Send**.~~

- ~~Record the response status and body.~~

- ~~Send GET /users again.~~

- ~~Check whether unrelated users were returned, changed, or deleted.~~

- ~~Check the response for internal storage or server details.~~

- ~~Delete the disposable record if one was created.~~

### **Expected Result**

The input should be rejected by validation or handled only as ordinary text. It must not bypass access controls, expose unrelated data, modify other records, or cause an internal server error.

## **TC-PEN-006: Attempt an HTTP Method Override**

**Related Scenario ID:** TS-PEN-006  
**Test Type:** Penetration/HTTP Method Manipulation  
**Priority:** Medium  
**Endpoint:** POST /books/{id}

### **Objective**

Determine whether an HTTP method override header can cause an unintended deletion.

### **Preconditions**

- A disposable book exists.

- Its ID and original values are recorded.

- The book is not required by another test.

### **Request Header**

X-HTTP-Method-Override: DELETE

### **Steps**

- ~~Create a disposable book.~~

- ~~Record its generated ID.~~

- ~~Select POST.~~

- ~~Enter http://localhost:4000/books/{id}.~~

- ~~Add the header X-HTTP-Method-Override: DELETE.~~

- ~~Click **Send**.~~

- ~~Record the status and response.~~

- ~~Send GET /books/{id}.~~

- ~~Confirm whether the book still exists.~~

### **Expected Result**

The unsupported POST request should be rejected. The override header should not delete or modify the book.

## **TC-PEN-007: Send Repeated Requests**

**Related Scenario ID:** TS-PEN-007  
**Test Type:** Penetration/Rate-Limit Testing  
**Priority:** Medium  
**Endpoint:** GET /books

### **Objective**

Determine whether the API remains stable when it receives repeated requests and whether basic rate limiting is implemented.

### **Preconditions**

- Postman Collection Runner is available.

- The API is running locally.

- Only a small, safe number of requests will be sent.

### **Steps**

- ~~Add GET /books to a Postman collection.~~

- ~~Open Collection Runner.~~

- ~~Configure approximately 30–50 iterations.~~

- ~~Use a short delay between requests when possible.~~

- ~~Run the collection.~~

- ~~Record the returned status codes.~~

- ~~Observe whether any response returns 429 Too Many Requests.~~

- ~~Send one normal GET /books request after the run.~~

- ~~Confirm that the API remains responsive.~~

### **Expected Result**

The API should remain stable and responsive. Ideally, excessive requests should be controlled with 429 Too Many Requests. If no rate limiting exists, record it as a security observation.
