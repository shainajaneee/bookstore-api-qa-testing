# Authors Module Test Cases

## **TC-RETAUTH-A001: Retrieve All Authors**

**Related Scenario ID:** TS-A001  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /authors

**Objective:  
** Verify that the API retrieves all available authors with the correct response structure and stored information.

**Preconditions:**

- Common preconditions are satisfied.

- A known collection of authors exists.

- Expected author IDs and field values are available for comparison.

**Test Data:  
** No request body. Use the prepared author collection as the expected dataset.

**Steps:**

- ~~Open Postman.~~

- ~~Select **GET** and enter http://localhost:4000/authors.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response body is a JSON array.~~

- ~~Verify that the returned author IDs and names match the prepared dataset.~~

- ~~Compare the stored biography and books values where those fields were supplied.~~

- ~~Confirm that all expected authors are present without duplicate IDs.~~

**Expected Result:  
** The API returns 200 OK with a JSON array matching the prepared author collection. All expected authors and their stored details are returned correctly.

## **TC-CREATEAUTH-A002: Create Author Using Valid Data**

**Related Scenario ID:** TS-A002  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** POST /authors

**Objective:  
** Verify that valid author information creates a new author that can subsequently be retrieved.

**Preconditions:**

- Common preconditions are satisfied.

- The test payload contains a valid name, biography, and books array.

**Test Data:**

{

"name": "QA Test Author",

"biography": "Author created for API testing.",

"books": \[\]

}

**Steps:**

- ~~Select **POST** and enter http://localhost:4000/authors.~~

- ~~Select **Body → raw → JSON**.~~

- ~~Enter the valid test data.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 201 Created.~~

- ~~Verify that the response contains a generated author ID.~~

- ~~Compare the returned name, biography, and books with the submitted values.~~

- ~~Record the generated ID.~~

- ~~Send GET /authors/{id} using that ID and verify the saved author details.~~

**Expected Result:  
** The POST request returns 201 Created with a generated ID and the submitted author information. A subsequent GET returns 200 OK with the same author details.

## **TC-CREATEAUTH-A003: Create Author With Missing Name**

**Related Scenario ID:** TS-A003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /authors

**Objective:  
** Verify that author creation is rejected when the required name field is omitted.

**Preconditions:**

- Common preconditions are satisfied.

- The initial author collection is available for comparison.

- The supplied biography and books values are valid.

**Test Data:**

{

"biography": "Author created for API testing.",

"books": \[\]

}

**Steps:**

- ~~Send GET /authors and record the existing author IDs and count.~~

- ~~Select **POST** and enter http://localhost:4000/authors.~~

- ~~Enter the test data with name completely omitted.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the missing author name.~~

- ~~Send GET /authors again.~~

- ~~Compare the collection with the initial records to confirm that no author was created.~~

**Expected Result:  
** The API returns 400 Bad Request with a validation error identifying the required author name. No new author is created.

## **TC-RETAUTH-A004: Retrieve Existing Author by ID**

**Related Scenario ID:** TS-A004  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /authors/{id}

**Objective:  
** Verify that an existing author can be retrieved using its ID and that the returned information is correct.

**Preconditions:**

- Common preconditions are satisfied.

- The target author exists.

- Its ID and expected field values are known.

- The record has not been modified or deleted before this test.

**Test Data:**

- **Author ID:** The actual ID of a known existing author.

- **Expected information:** The stored name, biography, and books values.

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/authors/{id} using the existing author ID.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response contains a JSON author object.~~

- ~~Verify that the returned ID matches the requested ID.~~

- ~~Compare the returned author information with the expected record.~~

**Expected Result:  
** The API returns 200 OK with the correct author ID and stored author information.

## **TC-RETAUTH-A005: Retrieve Nonexistent Author**

**Related Scenario ID:** TS-A005  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** GET /authors/99999

**Objective:  
** Verify that retrieving a nonexistent author returns a not-found response.

**Preconditions:**

- Common preconditions are satisfied.

- Author ID 99999 is confirmed absent from the test dataset.

**Test Data:**

- **Author ID:** 99999

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/authors/99999.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found.~~

- ~~Verify that the response indicates that the author does not exist.~~

- ~~Verify that no author record is returned.~~

**Expected Result:  
** The API returns 404 Not Found with an error indicating that the requested author does not exist. No author data is returned.

## **TC-UPDAUTH-A006: Update Existing Author Using Valid Data**

**Related Scenario ID:** TS-A006  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** PUT /authors/{id}

**Objective:  
** Verify that valid information updates an existing author and that the updated values are saved.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable author exists with known original values.

- Its ID is known.

- The submitted name and biography differ from the existing values.

**Test Data:**

{

"name": "QA Test Author Updated",

"biography": "Updated author biography for API testing.",

"books": \[\]

}

**Steps:**

- ~~Send GET /authors/{id} and record the original author information.~~

- ~~Select **PUT** and enter the same author URL.~~

- ~~Select **Body → raw → JSON** and enter the valid update payload.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response contains the same author ID.~~

- ~~Compare the returned information with the submitted values.~~

- ~~Send GET /authors/{id} again.~~

- ~~Verify that the retrieved record contains the updated name, biography, and books array.~~

**Expected Result:  
** The PUT request returns 200 OK with the same author ID and the submitted values. A subsequent GET confirms that the updated details were saved.

## **TC-UPDAUTH-A007: Update Author With Invalid Books Format**

**Related Scenario ID:** TS-A007  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /authors/{id}

**Objective:  
** Verify that an update is rejected when books is supplied as a string instead of an array.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable author exists with valid stored information.

- Its original values are known.

- The author’s current name and biography match the valid values below so that only books is changed.

**Test Data:**

{

"name": "QA Test Author",

"biography": "Author created for API testing.",

"books": "NOT-AN-ARRAY"

}

**Steps:**

- ~~Send GET /authors/{id} and record all original field values.~~

- ~~Select **PUT** and enter the same author URL.~~

- ~~Enter the payload containing the invalid books value.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the invalid books format.~~

- ~~Send GET /authors/{id} regardless of the PUT response status.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** The API rejects the request with 400 Bad Request and a validation error identifying that books must be an array. The stored author remains unchanged.

## **TC-DELAUTH-A008: Delete Existing Author**

**Related Scenario ID:** TS-A009  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** DELETE /authors/{id}

**Objective:  
** Verify that an existing author can be deleted and is no longer retrievable.

**Preconditions:**

- Common preconditions are satisfied.

- The target author exists.

- The author is a disposable test record with no associated books.

- The record is not required by another pending test.

**Test Data:**

- **Author ID:** An existing disposable author ID.

- **Request body:** None.

**Steps:**

- ~~Send GET /authors/{id} and confirm that the intended author exists.~~

- ~~Select **DELETE** and enter the same author URL.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Send GET /authors/{id} afterward.~~

- ~~Verify that the subsequent request returns 404 Not Found.~~

- ~~Verify that no author record is returned.~~

**Expected Result:  
** The DELETE request returns 200 OK. A subsequent GET for the same ID returns 404 Not Found, confirming that the author was removed.

## **TC-DELAUTH-A009: Delete Nonexistent Author**

**Related Scenario ID:** TS-A010  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** DELETE /authors/99999

**Objective:  
** Verify that deleting a nonexistent author returns a not-found response without affecting existing records.

**Preconditions:**

- Common preconditions are satisfied.

- Author ID 99999 is confirmed absent.

- At least one other author exists for checking unintended changes.

**Test Data:**

- **Author ID:** 99999

- **Request body:** None.

**Steps:**

- Send GET /authors and record the existing author IDs and values.

- ~~Select **DELETE** and enter http://localhost:4000/authors/99999.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found.~~

- ~~Verify that the response indicates that the author does not exist.~~

- ~~Send GET /authors again.~~

- ~~Compare the records by ID and values, ignoring array order.~~

- ~~Verify that no existing author was removed or changed.~~

**Expected Result:  
** The API returns 404 Not Found. Existing author records remain unchanged.

## **TC-UPDAUTH-A010: Update Nonexistent Author**

**Related Scenario ID:** TS-A008  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** PUT /authors/99999

**Objective:  
** Verify that updating a nonexistent author is rejected without creating a new author or changing existing records.

**Preconditions:**

- Common preconditions are satisfied.

- Author ID 99999 is confirmed absent.

- The request body contains otherwise valid author information.

**Test Data:**

{

"name": "QA Test Author Updated",

"biography": "Updated author biography for API testing.",

"books": \[\]

}

**Steps:**

- Send GET /authors and record the initial collection.

- ~~Confirm that author ID 99999 is absent.~~

- ~~Select **PUT** and enter http://localhost:4000/authors/99999.~~

- ~~Enter the valid payload.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found.~~

- ~~Verify that the response indicates that the author does not exist.~~

- ~~Send GET /authors/99999 and confirm that the target remains absent.~~

- ~~Send GET /authors and confirm that no records were created or changed.~~

**Expected Result:  
** The API returns 404 Not Found. No author is created for the nonexistent ID, and existing records remain unchanged.

## **TC-CREATEAUTH-A011: Create Author With Invalid Books Format**

**Related Scenario ID:** TS-A003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /authors

**Objective:  
** Verify that author creation rejects a books value that is not an array.

**Preconditions:**

- Common preconditions are satisfied.

- The supplied name and biography contain valid values.

- The initial author collection is available for comparison.

**Test Data:**

{

"name": "QA Test Author",

"biography": "Author created for API testing.",

"books": "NOT-AN-ARRAY"

}

**Steps:**

- ~~Send GET /authors and record the initial collection.~~

- ~~Select **POST** and enter http://localhost:4000/authors.~~

- ~~Enter the payload containing the invalid books value.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the invalid books format.~~

- ~~Verify that the valid name and biography do not produce unrelated validation errors.~~

- ~~Send GET /authors again and confirm that no author was created.~~

**Expected Result:  
** The API returns 400 Bad Request with a validation error identifying that books must be an array. No author is created, and existing records remain unchanged.

## **TC-UPDAUTH-A012: Update Author With Missing Name**

**Related Scenario ID:** TS-A007  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /authors/{id}

**Objective:  
** Verify that an author update is rejected when the required name field is omitted.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable author exists with valid information.

- Its ID and complete original field values are known.

- The supplied biography and books values are valid.

**Test Data:**

{

"biography": "Updated author biography for API testing.",

"books": \[\]

}

**Steps:**

- ~~Send GET /authors/{id} and record all original values.~~

- ~~Select **PUT** and enter the same author URL.~~

- ~~Enter the payload with name completely omitted—not blank or null.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the missing author name.~~

- ~~Send GET /authors/{id} again.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** The API returns 400 Bad Request with an error identifying that the author name is required. The existing name, biography, and books values remain unchanged.
