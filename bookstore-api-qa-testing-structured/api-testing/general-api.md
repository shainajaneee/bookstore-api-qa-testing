# General API Testing

TC-METHOD-G001: Send an Unsupported HTTP Method

## **TC-METHOD-G001: Send an Unsupported HTTP Method**

**Description:  
**Verify that the API properly rejects HTTP methods that are not supported by the requested endpoint.

**Key Functionalities:**

- Reject unsupported HTTP methods.

- Return the expected method-related error status.

- Provide an appropriate error response.

- Ensure rejected requests do not modify existing records.

- Confirm that the API remains available after the rejected request.

**Expected Result:  
**The API should reject unsupported methods with the expected 405 Method Not Allowed response. The response should not indicate that the operation succeeded, and no existing data should be changed.

**Actual Result:  
**The tested unsupported HTTP methods were rejected with 405 Method Not Allowed. The response indicated that the selected method was not supported, no stored records were changed, and valid requests continued to work afterward.

![Test evidence](../images/image5.png)

![Test evidence](../images/image28.png)

![Test evidence](../images/image5.png)

**Status:** PASS

TC-JSON-G002: Submit Malformed JSON

## **TC-JSON-G002: Submit Malformed JSON**

**Description:  
**Verify that the API properly handles requests containing malformed or syntactically invalid JSON.

**Key Functionalities:**

- Detect malformed JSON request bodies.

- Reject invalid request syntax.

- Return an appropriate client-error status.

- Avoid creating or updating records using malformed data.

- Continue processing valid requests afterward.

**Expected Result:  
**The API should reject malformed JSON with 400 Bad Request. The response should explain that the request could not be processed, no data should be changed, and the server should remain operational.

**Actual Result:  
**The malformed JSON requests were rejected with 400 Bad Request. No records were created or modified, and subsequent valid requests were processed successfully without an unexpected server error.

![Test evidence](../images/image15.png)

![Test evidence](../images/image70.png)

![Test evidence](../images/image103.png)

TC-ENDPOINT-G003: Request an Incorrect Endpoint

## **TC-ENDPOINT-G003: Request an Incorrect Endpoint**

**Description:  
**Verify that undefined or incorrect API endpoint paths return an appropriate not-found response.

**Key Functionalities:**

- Detect undefined endpoint paths.

- Return an appropriate not-found response.

- Avoid returning unrelated successful data.

- Continue processing valid endpoint requests afterward.

**Tested Endpoints:**

- GET /qa-nonexistent-endpoint

- GET /books/{id}/qa-unknown-route

**Expected Result:  
**Each undefined endpoint should return 404 Not Found. The response should indicate that the requested endpoint or resource could not be found. A subsequent valid GET /books request should return 200 OK.

**Actual Result:  
**Both undefined endpoints returned 404 Not Found, and neither request returned unrelated book or API data. The subsequent valid GET /books request returned 200 OK, confirming that the API remained operational.

![Test evidence](../images/image108.png)

![Test evidence](../images/image102.png)

![Test evidence](../images/image125.png)

TC-CONTENTTYPE-G004: Verify JSON Response Content…

## **TC-CONTENTTYPE-G004: Verify JSON Response Content Type**

**Description:  
**Verify that API responses documented as JSON declare the correct media type and contain valid JSON response bodies.

**Key Functionalities:**

- Return the application/json media type.

- Accept application/json; charset=utf-8 as a valid JSON content type.

- Return response bodies that can be parsed as JSON.

- Avoid returning HTML or unquoted plain text where JSON is required.

- Apply the expected content type across Books, Authors, and Users responses.

**Expected Result:  
**Responses documented as JSON should contain a Content-Type header of application/json or application/json; charset=utf-8. Each corresponding response body should contain syntactically valid JSON.

**Actual Result:  
**The applicable Books, Authors, and Users responses declared the expected JSON content type and contained valid JSON bodies. For example, GET /books returned 200 OK with Content-Type: application/json; charset=utf-8, and both Postman content-type and JSON-parsing assertions passed.

![Test evidence](../images/image53.png)

TC-SECURITY-G005: Check for Sensitive Server Info…

## **TC-SECURITY-G005: Check for Sensitive Server Information**

**Description:  
**Verify that successful and rejected API responses do not expose secrets, private configuration, or detailed internal server information.

**Key Functionalities:**

- Prevent exposure of passwords and secret keys.

- Prevent exposure of database connection strings and private configuration.

- Prevent stack traces and source-code details from appearing in responses.

- Prevent absolute server filesystem paths from being returned.

- Provide useful validation messages without revealing sensitive implementation details.

**Response Categories Tested:**

- Successful responses

- Validation errors

- Malformed JSON errors

- Missing-record responses

- Undefined-endpoint responses

- Unsupported-method responses

**Expected Result:  
**The tested responses should not contain server passwords, secret keys, connection strings, stack traces, internal source code, absolute filesystem paths, or detailed private configuration. Error responses may identify invalid fields but should not reveal sensitive server information.

**Actual Result:  
**No passwords, secret keys, connection strings, stack traces, source-code content, absolute server paths, or private configuration values were found in the tested Books, Authors, and Users responses.

The X-Powered-By: Express header was observed during testing. This disclosed the framework name but did not expose a framework version, credential, or secret. It may be recorded as a security-hardening observation, but it did not violate the agreed pass criteria for this test case.

![Test evidence](../images/image99.png)

![Test evidence](../images/image61.png)

![Test evidence](../images/image75.png)

![Test evidence](../images/image115.png)

![Test evidence](../images/image69.png)

TC-STATUS-G006: Verify HTTP Status Codes

## **TC-STATUS-G006: Verify HTTP Status Codes**

**Description:  
**Verify that the API returns HTTP status codes that correctly represent successful operations, validation failures, missing resources, invalid endpoints, and unsupported methods.

**Key Functionalities:**

- Return 200 OK for successful retrieval and update operations.

- Return 201 Created for successful creation operations.

- Return 400 Bad Request for validation failures and malformed JSON.

- Return 404 Not Found for missing records and undefined endpoints.

- Return 405 Method Not Allowed for unsupported methods.

- Ensure response bodies and stored data agree with the returned status.

**Expected Result:  
**Each tested operation should return its documented status code. Successful responses should correspond to completed operations, while rejected requests should not return misleading success codes or modify stored records. Client errors should not cause an unexpected 500 Internal Server Error.

**Actual Result:  
**All applicable status-code checks for Books, Authors, and Users returned their expected results:

| **Request Condition**                      | **Actual Status**      |
|--------------------------------------------|------------------------|
| Retrieve Collection                        | 200 OK                 |
| Retrieve existing record                   | 200 OK                 |
| Create valid record                        | 201 Created            |
| Create record with invalid or missing data | 400 Bad Request        |
| Update existing record with valid data     | 200 OK                 |
| Update record with invalid or missing data | 400 Bad Request        |
| Retrieve nonexistent record                | 404 Not Found          |
| Update nonexistent record                  | 404 Not Found          |
| Delete existing record                     | 200 OK                 |
| Delete nonexistent record                  | 404 Not Found          |
| Submit malformed JSON                      | 400 Bad Request        |
| Request undefined endpoint                 | 404 Not Found          |
| Use unsupported HTTP method                | 405 Method Not Allowed |

The response bodies agreed with their status codes, successful changes were confirmed through follow-up retrieval, and rejected writes did not modify stored records. No unexpected 500 Internal Server Error response was encountered.

![Test evidence](../images/image7.png)

![Test evidence](../images/image121.png)

![Test evidence](../images/image76.png)

![Test evidence](../images/image37.png)

![Test evidence](../images/image80.png)

![Test evidence](../images/image81.png)

![Test evidence](../images/image116.png)

![Test evidence](../images/image111.png)

![Test evidence](../images/image34.png)

![Test evidence](../images/image100.png)

![Test evidence](../images/image89.png)

![Test evidence](../images/image94.png)

![Test evidence](../images/image22.png)

![Test evidence](../images/image47.png)

![Test evidence](../images/image122.png)

TC-SWAGGER-G007: Verify Consistency With Swagger …

## **TC-SWAGGER-G007: Verify Consistency With Swagger Documentation**

**Description:  
**Verify that the implemented API endpoints, HTTP methods, request fields, response structures, and status codes are consistent with the Swagger documentation for the tested local version.

**Key Functionalities:**

- Compare implemented routes with documented endpoints.

- Compare supported HTTP methods.

- Compare required request fields and data types.

- Compare documented and actual response fields.

- Compare expected and actual HTTP status codes.

- Verify that the Swagger documentation and API belong to the same application version.

**Expected Result:  
**The implemented Books, Authors, and Users endpoints should be consistent with the corresponding Swagger definitions. The tested methods, payload fields, response structures, and status codes should match the documented API contract.

**Actual Result:  
**The tested Books, Authors, and Users endpoints were consistent with the Swagger documentation for the local API version. The reviewed routes, HTTP methods, request fields, response structures, and status codes matched their documented definitions. No documentation mismatch was identified within the tested scope.

![Test evidence](../images/image50.png)

![Test evidence](../images/image44.png)
