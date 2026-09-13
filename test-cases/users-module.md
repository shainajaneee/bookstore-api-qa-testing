# Users Module Test Cases

## **Common Preconditions**

These apply to every test case:

- The Bookstore API server is running at http://localhost:4000.

- Postman can access the API.

- For POST and PUT requests, select **Body → raw → JSON** and confirm Content-Type: application/json.

- Replace {id} with the actual ID of the intended test user.

- Use 99999 only after confirming that it does not exist.

- Use disposable test records.

- Avoid concurrent changes during before-and-after comparisons.

- Restore the required starting data or create a fresh record before each case.

- Complete tests that need a user before deleting that record.

## **TC-RETUSER-U001: Retrieve All Users**

**Related Scenario ID:** TS-U001  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /users

**Objective:  
** Verify that the API retrieves all available users with the correct response structure and stored information.

**Preconditions:**

- A known collection of users exists.

- Expected user IDs and field values are available for comparison.

**Test Data:  
** No request body. Use the prepared user collection as the expected dataset.

**Steps:**

- ~~Select **GET** and enter http://localhost:4000/users.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response body is a JSON array.~~

- ~~Compare the returned IDs, names, and email addresses with the prepared dataset.~~

- ~~Compare purchasedBooks with the stored test data.~~

- ~~Verify that all expected users are present without duplicate IDs.~~

**Expected Result:  
** The API returns 200 OK with a JSON array matching the prepared user collection. All expected users and their stored details are returned correctly.

## **TC-CREATEUSER-U002: Create User Using Valid Data**

**Related Scenario ID:** TS-U002  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** POST /users

**Objective:  
** Verify that valid user information creates a new user that can subsequently be retrieved.

**Preconditions:**

- The payload contains a valid name, email address, and purchased-books array.

- The test data satisfies any applicable uniqueness requirements.

**Test Data:**

{

"name": "QA Test User",

"email": "qa.user@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Select **POST** and enter http://localhost:4000/users.~~

- ~~Enter the valid JSON payload.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 201 Created.~~

- ~~Verify that the response contains a generated user ID.~~

- ~~Compare the returned name, email, and purchased-books array with the submitted values.~~

- ~~Record the generated ID.~~

- ~~Send GET /users/{id} using that ID and verify the saved user details.~~

**Expected Result:  
** The POST request returns 201 Created with a generated ID and the submitted user information. A subsequent GET returns 200 OK with the same user details.

## **TC-CREATEUSER-U003: Create User With Missing Name**

**Related Scenario ID:** TS-U003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /users

**Objective:  
** Verify that user creation is rejected when the required name field is omitted.

**Preconditions:**

- The supplied email address and purchased-books array are valid.

- The initial user collection is available for comparison.

**Test Data:**

{

"email": "qa.user@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users and record the existing user IDs and count.~~

- ~~Select **POST** and enter http://localhost:4000/users.~~

- ~~Enter the payload with name completely omitted.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the missing name.~~

- ~~Send GET /users again.~~

- ~~Confirm that no new user was created.~~

**Expected Result:  
** The API returns 400 Bad Request with a validation error identifying the required user name. No user is created.

## **TC-CREATEUSER-U004: Create User With Invalid Email**

**Related Scenario ID:** TS-U003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /users

**Objective:  
** Verify that user creation rejects an email address with an invalid format.

**Preconditions:**

- All submitted fields except email contain valid values.

- The initial user collection is available for comparison.

**Test Data:**

{

"name": "QA Test User",

"email": "invalid-email",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users and record the initial collection.~~

- ~~Select **POST** and enter http://localhost:4000/users.~~

- ~~Enter the payload containing invalid-email.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the invalid email format.~~

- ~~Send GET /users again and confirm that no user was created.~~

**Expected Result:  
** The API returns 400 Bad Request with an email validation error. No user is created, and existing records remain unchanged.

## **TC-UPDUSER-U005: Update Existing User Using Valid Data**

**Related Scenario ID:** TS-U006  
**Test Type:** Functional / Positive  
**Priority:** Medium  
**Endpoint:** PUT /users/{id}

**Objective:  
** Verify that valid information updates an existing user and that the updated values are saved.

**Preconditions:**

- A disposable user exists with known original values.

- Its ID is known.

- The submitted name and email differ from the current values.

- The update data satisfies applicable validation requirements.

**Test Data:**

{

"name": "QA Test User Updated",

"email": "qa.updated@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users/{id} and record the original user information.~~

- ~~Select **PUT** and enter the same user URL.~~

- ~~Enter the valid update payload.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response contains the same user ID and the submitted values.~~

- ~~Send GET /users/{id} again.~~

- ~~Verify that the retrieved record contains the updated information.~~

**Expected Result:  
** The PUT request returns 200 OK with the same user ID and the submitted values. A subsequent GET confirms that the updated details were saved.

## **TC-UPDUSER-U006: Update User With Invalid Email**

**Related Scenario ID:** TS-U009  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /users/{id}

**Objective:  
** Verify that an update rejects an invalid email address and leaves the existing user unchanged.

**Preconditions:**

- A disposable user exists with a valid email address.

- Its original field values are known.

- The current name is QA Test User and purchasedBooks is \` empty, so only the email value is changed.

- The agreed update requirements require a valid email format.

**Test Data:**

{

"name": "QA Test User",

"email": "invalid-email",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users/{id} and record every original field value.~~

- ~~Select **PUT** and enter the same user URL.~~

- ~~Enter the payload containing the invalid email address.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the response identifies the invalid email format.~~

- ~~Send GET /users/{id} regardless of the PUT response status.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** The API returns 400 Bad Request with an email validation error. The original valid email address and all other stored values remain unchanged.

## **TC-DELUSER-U007: Delete Existing User**

**Related Scenario ID:** TS-U007  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** DELETE /users/{id}

**Objective:  
** Verify that an existing user can be deleted and is no longer retrievable.

**Preconditions:**

- The target user exists.

- The user is a disposable test record.

- The record is not required by another pending test.

- Any requirements that could prevent deletion are satisfied.

**Test Data:**

- **User ID:** An existing disposable user ID.

- **Request body:** None.

**Steps:**

- ~~Send GET /users/{id} and confirm that the intended user exists.~~

- ~~Select **DELETE** and enter the same user URL.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Send GET /users/{id} afterward.~~

- ~~Verify that the subsequent request returns 404 Not Found with no user record.~~

**Expected Result:  
** The DELETE request returns 200 OK. A subsequent GET for the same ID returns 404 Not Found, confirming that the user was removed.

## **TC-DELUSER-U008: Delete Nonexistent User**

**Related Scenario ID:** TS-U008  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** DELETE /users/99999

**Objective:  
** Verify that deleting a nonexistent user returns a not-found response without affecting existing users.

**Preconditions:**

- User ID 99999 is confirmed absent.

- At least one other user exists for checking unintended changes.

**Test Data:**

- **User ID:** 99999

- **Request body:** None.

**Steps:**

- ~~Send GET /users and record the existing user IDs and values.~~

- ~~Select **DELETE** and enter http://localhost:4000/users/99999.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found.  
  > 5вроп. Verify that the response indicates the user does not exist.~~

- ~~Send GET /users again.~~

- ~~Compare the records by ID and values, ignoring array order.~~

- ~~Confirm that no existing user was removed or changed.~~

**Expected Result:  
** The API returns 404 Not Found. Existing user records remain unchanged.

## **TC-RETUSER-U009: Retrieve Existing User by ID**

**Related Scenario ID:** TS-U004  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /users/{id}

**Objective:  
** Verify that an existing user can be retrieved using its ID and that the returned information is correct.

**Preconditions:**

- The target user exists.

- Its ID and expected field values are known.

- The user has not been modified or deleted before this test.

**Test Data:**

- **User ID:** The actual ID of a known existing user.

- **Expected information:** The stored name, email, and purchased-books array.

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/users/{id} using the existing user ID.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 200 OK.~~

- ~~Verify that the response contains a JSON user object.~~

- ~~Verify that the returned ID matches the requested ID.~~

- ~~Compare the returned information with the expected record.~~

**Expected Result:  
** The API returns 200 OK with the requested user ID and the correct stored user information.

## **TC-RETUSER-U010: Retrieve Nonexistent User**

**Related Scenario ID:** TS-U005  
**Test Type:** Functional / Negative  
**Priority:** High  
**Endpoint:** GET /users/99999

**Objective:  
** Verify that retrieving a nonexistent user returns a not-found response.

**Preconditions:**

- User ID 99999 is confirmed absent from the test dataset.

**Test Data:**

- **User ID:** 99999

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/users/99999.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found.~~

- ~~Verify that the response indicates that the requested user does not exist.~~

- ~~Verify that no user record is returned.~~

**Expected Result:  
** The API returns 404 Not Found with a user-not-found error and no user data.

## **TC-UPDUSER-U011: Update Nonexistent User**

**Related Scenario ID:** TS-U010  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** PUT /users/99999

**Objective:  
** Verify that updating a nonexistent user is rejected without creating a new user or changing existing records.

**Preconditions:**

- User ID 99999 is confirmed absent.

- The request body contains otherwise valid user information.

- The initial collection is available for comparison.

**Test Data:**

{

"name": "QA Missing User",

"email": "qa.missing@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users and record the initial collection.~~

- ~~2 Lexus. Confirm that ID 99999 is absent.~~

- ~~Select **PUT** and enter http://localhost:4000/users/99999.~~

- ~~Enter the valid payload.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 404 Not Found and the response indicates that the user does not exist.~~

- ~~Send GET /users/99999 and confirm that the target remains absent.~~

- ~~Send GET /users and confirm that no records were created or changed.~~

**Expected Result:  
** The API returns 404 Not Found. No user is created for the nonexistent ID, and existing records remain unchanged.

## **TC-UPDUSER-U012: Update User With Missing Email**

**Related Scenario ID:** TS-U009  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /users/{id}

**Objective:  
** Verify that an update is rejected when the required email field is omitted.

**Preconditions:**

- A disposable user exists with valid information.

- Its ID and original field values are known.

- The supplied name and purchased-books array are valid.

**Test Data:**

{

"name": "QA Test User",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users/{id} and record all original values.~~

- ~~Select **PUT** and enter the same user URL.~~

- ~~Enter the payload with email completely omitted—not blank or null.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the response indicates that required user information is missing.~~

- ~~Send GET /users/{id} again.~~

- ~~Confirm that every stored field matches the original record.~~

**Expected Result:  
** The API returns 400 Bad Request with a required-field error. Thegare existing email address and all other user information remain unchanged.

## **TC-CREATEUSER-U013: Create User With Missing Email**

**Related Scenario ID:** TS-U003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /users

**Objective:  
** Verify that user creation is rejected when the required email field is omitted.

**Preconditions:**

- The supplied name and purchased-books array are valid.

- The initial user collection is available for comparison.

**Test Data:**

{

"name": "QA Test User",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users and record the initial collection.~~

- ~~Select **POST** and enter http://localhost:4000/users.~~

- ~~Enter the payload with email completely omitted.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the validation response identifies the email field.~~

- ~~Send GET /users again.~~

- ~~Confirm that no new user was created.~~

**Expected Result:  
** The API returns 400 Bad Request with an email validation error. No user is created, and existing records remain unchanged.

## **TC-UPDUSER-U014: Update User With Missing Name**

**Related Scenario ID:** TS-U009  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /users/{id}

**Objective:  
** Verify that an update is rejected when the required name field is omitted.

**Preconditions:**

- A disposable user exists with valid information.

- Its ID and original field values are known.

- The supplied email and purchased-books array are valid.

**Test Data:**

{

"email": "qa.user@example.com",

"purchasedBooks": \[\]

}

**Steps:**

- ~~Send GET /users/{id} and record all original field values.~~

- ~~Select **PUT** and enter the same user URL.~~

- ~~Enter the payload with name completely omitted—not blank or null.~~

- ~~Click **Send**.~~

- ~~Verify that the HTTP status is 400 Bad Request.~~

- ~~Verify that the response indicates that required user information is missing.~~

- ~~Send GET /users/{id} again.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** The API returns 400 Bad Request with a required-field error. The existing name, email, and purchased-books values remain unchanged.
