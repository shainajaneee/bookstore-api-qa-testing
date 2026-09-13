# Unit Test Cases

## **TC-UNIT-B001: Retrieve All Books**

**Related Scenario ID:** TS-UNIT-B001  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** GET /books

**Objective:  
** Verify that the Books endpoint returns a successful response containing an array.

**Preconditions:**

- Jest and Supertest are installed and configured.

- The test environment is available.

- The application can be imported into the test file.

**Test Data:  
** No request body.

**Automated Test Steps:**

- ~~Import the application and Supertest.~~

- ~~Send a GET request to /books.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the response body is an array.~~

- ~~If records exist, assert that the required book fields are present.~~

**Expected Result:  
** The endpoint returns 200 OK, and the response body is an array of book records.

## **TC-UNIT-B002: Create a Book Using Valid Data**

**Related Scenario ID:** TS-UNIT-B002  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** POST /books

**Objective:  
** Verify that valid book information creates a new book.

**Preconditions:**

- Jest and Supertest are configured.

- The payload satisfies the Books API validation rules.

- The test data does not conflict with existing records.

- Created test data can be removed during cleanup.

**Test Data:**

{

"title": "Automated Test Book",

"author": "Automated Test Author",

"publicationDate": "2026-08-29",

"ISBN": "978-1234567897"

}

**Automated Test Steps:**

- ~~Send a POST request to /books.~~

- ~~Include the valid book payload.~~

- ~~Assert the documented successful creation status.~~

- ~~Assert that the response contains a generated ID.~~

- ~~Assert that the returned values match the submitted values.~~

- ~~Record the generated ID.~~

- ~~Remove the disposable record during cleanup.~~

**Expected Result:  
** The API creates a book and returns the documented success status, a generated ID, and the submitted book information.

## **TC-UNIT-B003: Update an Existing Book**

**Related Scenario ID:** TS-UNIT-B003  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** PUT /books/{id}

**Objective:  
** Verify that valid information updates an existing book.

**Preconditions:**

- A disposable book is created during test setup.

- Its ID and original values are recorded.

- The update payload satisfies all validation requirements.

**Test Data:**

{

"title": "Updated Automated Test Book",

"author": "Automated Test Author",

"publicationDate": "2026-08-29",

"ISBN": "978-1234567897"

}

**Automated Test Steps:**

- ~~Create a disposable book during test setup.~~

- ~~Record its generated ID.~~

- ~~Send a PUT request to /books/{id}.~~

- ~~Include the valid update payload.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the returned ID matches the original ID.~~

- ~~Assert that the returned fields match the submitted update values.~~

- ~~Retrieve the book and verify that the update was saved.~~

- ~~Remove the disposable record during cleanup.~~

**Expected Result:  
** The API returns 200 OK, retains the same book ID, and saves the updated information.

## **TC-UNIT-B004: Delete an Existing Book**

**Related Scenario ID:** TS-UNIT-B004  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** DELETE /books/{id}

**Objective:  
** Verify that an existing disposable book can be deleted.

**Preconditions:**

- A disposable book is created during test setup.

- Its generated ID is recorded.

- The record is not required by another test.

**Test Data:  
** The ID of the disposable book.

**Automated Test Steps:**

- ~~Create a disposable book during test setup.~~

- ~~Record its generated ID.~~

- ~~Send a DELETE request to /books/{id}.~~

- ~~Assert that the response status is 200.~~

- ~~Send a GET request using the deleted ID.~~

- ~~Assert that the second request returns 404.~~

**Expected Result:  
** The API deletes the book successfully, and the deleted record can no longer be retrieved.

## **TC-UNIT-A001: Retrieve All Authors**

**Related Scenario ID:** TS-UNIT-A001  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** GET /authors

**Objective:  
** Verify that the Authors endpoint returns an array.

**Preconditions:**

- Jest and Supertest are installed and configured.

- The test environment is available.

**Test Data:  
** No request body.

**Automated Test Steps:**

- ~~Send a GET request to /authors.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the response body is an array.~~

- ~~If records exist, assert that expected author fields are present.~~

**Expected Result:  
** The endpoint returns 200 OK, and the response body is an array of author records.

## **TC-UNIT-A002: Create an Author Using Valid Data**

**Related Scenario ID:** TS-UNIT-A002  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** POST /authors

**Objective:  
** Verify that valid author information creates a new author.

**Preconditions:**

- Jest and Supertest are configured.

- The payload satisfies the Authors API requirements.

- Created test data can be removed during cleanup.

**Test Data:**

{

"name": "Automated Test Author",

"books": \[\]

}

**Automated Test Steps:**

- ~~Send a POST request to /authors.~~

- ~~Include the valid author payload.~~

- ~~Assert the documented successful creation status.~~

- ~~Assert that the response contains a generated ID.~~

- ~~Assert that the returned values match the payload.~~

- ~~Record the generated ID.~~

- ~~Delete the disposable record during cleanup.~~

**Expected Result:  
** The API creates a new author and returns the documented success status, generated ID, and submitted author information.

## **TC-UNIT-A003: Update an Existing Author**

**Related Scenario ID:** TS-UNIT-A003  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** PUT /authors/{id}

**Objective:  
** Verify that valid information updates an existing author.

**Preconditions:**

- A disposable author is created during test setup.

- Its ID and original values are recorded.

- The update payload satisfies the validation requirements.

**Test Data:**

{

"name": "Updated Automated Test Author",

"books": \[\]

}

**Automated Test Steps:**

- ~~Create a disposable author.~~

- ~~Record its generated ID.~~

- ~~Send a PUT request to /authors/{id}.~~

- ~~Include the valid update payload.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the author ID remains unchanged.~~

- ~~Assert that the response contains the updated values.~~

- ~~Retrieve the author and verify that the changes were saved.~~

- ~~Delete the disposable author during cleanup.~~

**Expected Result:  
** The API returns 200 OK, retains the same author ID, and saves the updated information.

## **TC-UNIT-A004: Delete an Existing Author**

**Related Scenario ID:** TS-UNIT-A004  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** DELETE /authors/{id}

**Objective:  
** Verify that an existing disposable author can be deleted.

**Preconditions:**

- A disposable author is created during test setup.

- Its generated ID is recorded.

- The record is not required by another test.

**Test Data:  
** The ID of the disposable author.

**Automated Test Steps:**

- ~~Create a disposable author.~~

- ~~Record its generated ID.~~

- ~~Send a DELETE request to /authors/{id}.~~

- ~~Assert that the response status is 200.~~

- ~~Send a GET request using the deleted ID.~~

- ~~Assert that the GET request returns 404.~~

**Expected Result:  
** The API deletes the author successfully, and the record can no longer be retrieved.

## **TC-UNIT-U001: Retrieve All Users**

**Related Scenario ID:** TS-UNIT-U001  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** GET /users

**Objective:  
** Verify that the Users endpoint returns an array.

**Preconditions:**

- Jest and Supertest are installed and configured.

- The test environment is available.

**Test Data:  
** No request body.

**Automated Test Steps:**

- ~~Send a GET request to /users.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the response body is an array.~~

- ~~If records exist, assert that expected user fields are present.~~

**Expected Result:  
** The endpoint returns 200 OK, and the response body is an array of user records.

## **TC-UNIT-U002: Create a User Using Valid Data**

**Related Scenario ID:** TS-UNIT-U002  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** POST /users

**Objective:  
** Verify that valid user information creates a new user.

**Preconditions:**

- Jest and Supertest are configured.

- The payload satisfies the Users API validation requirements.

- The test email does not conflict with an existing user.

- Created test data can be removed during cleanup.

**Test Data:**

{

"name": "Automated Test User",

"email": "automated-test@example.com"

}

**Automated Test Steps:**

- ~~Send a POST request to /users.~~

- ~~Include the valid user payload.~~

- ~~Assert the documented successful creation status.~~

- ~~Assert that the response contains a generated ID.~~

- ~~Assert that the returned name and email match the payload.~~

- ~~Record the generated ID.~~

- ~~Delete the disposable record during cleanup.~~

**Expected Result:  
** The API creates a new user and returns the documented success status, generated ID, and submitted user information.

## **TC-UNIT-U003: Update an Existing User**

**Related Scenario ID:** TS-UNIT-U003  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** PUT /users/{id}

**Objective:  
** Verify that valid information updates an existing user.

**Preconditions:**

- A disposable user is created during test setup.

- Its ID and original values are recorded.

- The updated email does not conflict with another user.

**Test Data:**

{

"name": "Updated Automated Test User",

"email": "updated-automated-test@example.com"

}

**Automated Test Steps:**

- ~~Create a disposable user.~~

- ~~Record its generated ID.~~

- ~~Send a PUT request to /users/{id}.~~

- ~~Include the valid update payload.~~

- ~~Assert that the response status is 200.~~

- ~~Assert that the user ID remains unchanged.~~

- ~~Assert that the response contains the updated name and email.~~

- ~~Retrieve the user and verify that the changes were saved.~~

- ~~Delete the disposable user during cleanup.~~

**Expected Result:  
** The API returns 200 OK, retains the same user ID, and saves the updated user information.

## **TC-UNIT-U004: Delete an Existing User**

**Related Scenario ID:** TS-UNIT-U004  
**Test Type:** Automated Unit/Integration  
**Priority:** High  
**Target:** DELETE /users/{id}

**Objective:  
** Verify that an existing disposable user can be deleted.

**Preconditions:**

- A disposable user is created during test setup.

- Its generated ID is recorded.

- The record is not required by another test.

**Test Data:  
** The ID of the disposable user.

**Automated Test Steps:**

- ~~Create a disposable user.~~

- ~~Record its generated ID.~~

- ~~Send a DELETE request to /users/{id}.~~

- ~~Assert that the response status is 200.~~

- ~~Send a GET request using the deleted ID.~~

- ~~Assert that the GET request returns 404.~~

**Expected Result:  
** The API deletes the user successfully, and the deleted record can no longer be retrieved.
