# General API Module Test Cases

## **TC-METHOD-G001: Send an Unsupported HTTP Method**

**Related Scenario:** TS-G001  
**Test Type:** Negative Test Case  
**Priority:** Medium

**Objective:  
** To verify that an unsupported method on an existing endpoint is rejected without changing stored records.

**Preconditions:**

- The /users collection supports GET and POST.

- PUT /users is not a supported operation. This is different from the supported PUT /users/{id} operation.

**Test Data:**

**Request:** PUT /users

{

"name": "QA General API User",

"email": "qa.general@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users and save the returned records for comparison.~~

- ~~Create a new request using PUT.~~

- ~~Enter http://localhost:4000/users, without an ID.~~

- ~~Enter the test data as the JSON body.~~

- ~~Click **Send**.~~

- ~~Verify the response status and the Allow response header.~~

- ~~Send GET /users again.~~

- ~~Verify that no records were added, changed, or deleted.~~

**Expected Result:**

- The API returns 405 Method Not Allowed.

- The Allow header identifies methods supported by the endpoint.

- No stored records change.

- Subsequent valid requests remain functional.

**Requirement note:** This is the standards-based acceptance target for a recognized method disallowed on the target resource. Confirm it with the project requirements before execution. RFC 9110

## **TC-JSON-G002: Submit Malformed JSON**

**Related Scenario:** TS-G002  
**Test Type:** Negative Test Case  
**Priority:** High

**Objective:  
** To verify that malformed JSON is rejected without creating or modifying records.

**Preconditions:**

- An existing disposable user is available for the update variation.

- The user’s original information has been saved for comparison.

**Test Data:**

The comma after name is intentionally missing:

{

"name": "QA General API User"

"email": "qa.general@example.com",

"purchasedBooks": \[\]

}

**Requests:**

| **Method** | **Endpoint** |
|------------|--------------|
| POST       | /users       |
| PUT        | /users/{id}  |

**Steps:**

- ~~Retrieve the current users or target user and save the response.~~

- ~~Create the request being tested.~~

- ~~Select **Body → raw → JSON**.~~

- ~~Paste the malformed payload without correcting it.~~

- ~~Click **Send**.~~

- ~~Verify the status code and error message.~~

- ~~Retrieve the collection or target user again.~~

- ~~Confirm that the rejected request did not create or modify a record.~~

- ~~Repeat for the second request.~~

**Expected Result:**

- The API returns 400 Bad Request.

- The response indicates invalid JSON or a request-syntax problem.

- No record is created or modified.

- Subsequent valid requests continue to work.

**Note:** {} is valid JSON. It tests missing fields, not malformed JSON.

## **TC-ENDPOINT-G003: Request an Incorrect Endpoint**

**Related Scenario:** TS-G003  
**Test Type:** Negative Test Case  
**Priority:** Medium

**Objective:  
** To verify that undefined endpoint paths return an appropriate not-found response.

**Preconditions:**

- The paths below are not implemented.

- The book ID used in the second request belongs to an existing record.

**Test Data:**

| **Method** | **Endpoint**                 |
|------------|------------------------------|
| GET        | /qa-nonexistent-endpoint     |
| GET        | /books/{id}/qa-unknown-route |

**Steps:**

- ~~Open Postman and select GET.~~

- ~~Enter the first endpoint.~~

- ~~Click **Send**.~~

- ~~Verify the response status and body.~~

- ~~Repeat using the second endpoint.~~

- ~~Send a valid GET /books request afterward.~~

**Expected Result:**

- Each undefined endpoint returns 404 Not Found.

- The response indicates that the requested path or resource was not found.

- The API does not return an unrelated successful response.

- The subsequent valid request returns 200 OK.

## **TC-CONTENTTYPE-G004: Verify JSON Response Content Type**

**Related Scenario:** TS-G004  
**Test Type:** API Test Case  
**Priority:** Medium

**Objective:  
** To verify that responses documented as JSON declare the correct content type and contain valid JSON.

**Preconditions:**

- The expected response media types are available in the API documentation.

- Valid payloads and existing IDs are available from the Books, Authors, and Users test cases.

**Test Data:**

Run the applicable checks for each module:

| **Request**                        | **Required Data**                        |
|------------------------------------|------------------------------------------|
| GET collection                     | No request body                          |
| GET existing record                | Existing record ID                       |
| POST valid record                  | Valid module payload                     |
| PUT existing record                | Existing ID and valid updated payload    |
| DELETE response documented as JSON | Disposable record ID                     |
| Error response documented as JSON  | Input that triggers the documented error |

**Steps:**

- ~~Create the selected request in Postman.~~

- ~~Add Accept: application/json.~~

- ~~Supply the required ID and body.~~

- ~~Click **Send**.~~

- ~~Open the **response Headers** section.~~

- ~~Inspect the response’s Content-Type header.~~

- ~~Verify that the response body can be parsed as JSON.~~

- ~~Repeat for the applicable requests in each module.~~

**Expected Result:**

- Responses documented as JSON declare application/json.

- A header such as application/json; charset=utf-8 is acceptable.

- The body contains valid JSON.

- HTML or unquoted plain text is not returned where JSON is required.

**Exclusions:** Swagger’s HTML interface, the welcome page, and responses defined to have no body are excluded. Error responses should only be required to use JSON when the agreed contract specifies it.

## **TC-SECURITY-G005: Check for Sensitive Server Information**

**Related Scenario:** TS-G005  
**Test Type:** Security Test Case  
**Priority:** High

**Objective:  
** To verify that the tested responses do not expose server secrets or internal debugging information.

**Preconditions:**

- Only synthetic test data is used.

- Testing does not require crashing the server or changing server files and permissions.

**Test Data:**

| **Response Category** | **Request**                  |
|-----------------------|------------------------------|
| Successful response   | GET /users                   |
| Validation error      | POST /users with {}          |
| Malformed JSON error  | Request from TC-JSON-G002    |
| Missing record        | GET /users/{missingId}       |
| Undefined endpoint    | GET /qa-nonexistent-endpoint |
| Unsupported method    | Request from TC-METHOD-G001  |

**Steps:**

- ~~Send each request.~~

- ~~Inspect the complete response body and headers.~~

- ~~Check for server passwords, secret keys, connection strings, and private configuration.~~

- ~~Check for stack traces, internal source code, and absolute server filesystem paths.~~

- ~~Verify that error messages explain the request problem without exposing server internals.~~

- ~~Repeat equivalent success and error checks for Books and Authors.~~

**Expected Result:**

- No server secrets or private configuration appear in the response.

- Error messages do not expose stack traces, internal source code, or server filesystem paths.

- Validation messages may identify invalid fields without revealing internal implementation details.

- Detailed server diagnostics are not returned to the client. [<u>OWASP Error Handling guidance</u>](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html?utm_source=chatgpt.com)

**Scope:** This case checks the responses exercised above. Testing unexpected server failures requires a controlled failure fixture; this case alone is not a complete security assessment.

## **TC-STATUS-G006: Verify HTTP Status Codes**

**Related Scenario:** TS-G006  
**Test Type:** API Test Case  
**Priority:** High

**Objective:  
** To verify that response status codes correctly represent successful operations and rejected requests.

**Preconditions:**

- Expected status codes have been confirmed against the project requirements.

- Existing and nonexistent IDs are available for each module.

- Disposable records are used for creation, update, and deletion.

- Existing module test cases may be reused for these assertions.

**Test Data and Expected Results:**

Replace {resource} with books, authors, or users.

| **Request / Condition**                      | **Expected Status**    |
|----------------------------------------------|------------------------|
| GET /{resource}                              | 200 OK                 |
| GET /{resource}/{id} using an existing ID    | 200 OK                 |
| POST /{resource} with valid data             | 201 Created            |
| POST /{resource} with {}                     | 400 Bad Request        |
| PUT /{resource}/{id} with valid updated data | 200 OK                 |
| PUT /{resource}/{id} with {}                 | 400 Bad Request        |
| GET /{resource}/{missingId}                  | 404 Not Found          |
| PUT /{resource}/{missingId} with valid data  | 404 Not Found          |
| DELETE /{resource}/{id} using an existing ID | 200 OK                 |
| DELETE /{resource}/{missingId}               | 404 Not Found          |
| Malformed JSON request                       | 400 Bad Request        |
| Undefined endpoint                           | 404 Not Found          |
| Disallowed method on an existing endpoint    | 405 Method Not Allowed |

The CRUD codes reflect this project’s documented expectations, rather than universal requirements for every API. Confirm against your local version’s [<u>Swagger definition</u>](https://github.com/Xmwo3i/Bookstore-API/blob/main/swagger-definition.json?utm_source=chatgpt.com).

**Steps:**

- ~~Execute the applicable requests for each module.~~

- ~~Use the corresponding module’s valid payload for successful creation and update.~~

- ~~Use a valid payload when updating a nonexistent ID, so missing-field validation does not obscure the not-found check.~~

- ~~Compare each status code with the expected value.~~

- ~~Verify that the response body agrees with the status.~~

- ~~Retrieve records after successful creation or update to confirm the operation.~~

- ~~Retrieve a deleted record and confirm that it is no longer available.~~

- ~~Verify that rejected writes did not change stored records.~~

- ~~Run deletion after other tests requiring the same record.~~

**Expected Result:**

- Each request returns the expected status.

- Successful statuses correspond to successful operations.

- Rejected requests do not return misleading success codes.

- Client input errors do not produce unexpected 500 Internal Server Error responses.

- Stored data and response bodies agree with the reported outcome.

## **TC-SWAGGER-G007: Verify Consistency With Swagger Documentation**

**Related Scenario:** TS-G007  
**Test Type:** Documentation / API Test Case  
**Priority:** Medium

**Objective:  
** To verify that Swagger accurately describes implemented endpoints, accepted requests, and returned responses.

**Preconditions:**

- Swagger is accessible at http://localhost:4000/api-docs.

- Swagger and the application represent the same version.

- An independent endpoint inventory is available from the approved requirements or application routes.

- Valid and invalid module test data is available.

**Endpoint Inventory:**

| **Module** | **Collection Operations**   | **Record Operations**          |
|------------|-----------------------------|--------------------------------|
| Books      | GET /books, POST /books     | GET, PUT, DELETE /books/{id}   |
| Authors    | GET /authors, POST /authors | GET, PUT, DELETE /authors/{id} |
| Users      | GET /users, POST /users     | GET, PUT, DELETE /users/{id}   |

**Test Data:**

- Valid creation and update payloads from each module.

- Missing-field and invalid-field payloads.

- Existing IDs.

- Confirmed nonexistent IDs.

**Steps:**

- ~~Open Swagger documentation.~~

- ~~Compare documented paths and methods with the independent endpoint inventory.~~

- ~~Verify that implemented endpoints are documented and documented endpoints exist.~~

- ~~Review path parameters, required fields, field types, formats, and request content types.~~

- ~~Execute valid requests in Postman.~~

- ~~Compare response status codes, content types, fields, and data types with Swagger.~~

- ~~Check whether response bodies are objects or arrays as documented.~~

- ~~Execute applicable validation and nonexistent-record requests.~~

- ~~Compare their status codes and error structures with the documentation.~~

- ~~Check that examples agree with their referenced schemas.~~

- ~~Include GET /users/{id} explicitly in the endpoint comparison.~~

- ~~Remove disposable records created during testing.~~

**Expected Result:**

- All in-scope implemented endpoints and methods are documented.

- Documented operations exist.

- Request requirements match the approved behavior.

- Response statuses, content types, structures, and field types match Swagger.

- Examples are consistent with their schemas.

- Missing documentation and behavior mismatches are identified for resolution.
