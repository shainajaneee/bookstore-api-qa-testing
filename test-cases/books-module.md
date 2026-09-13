# Books Module Test Cases

## **TC-RETBOOKS-B001: Retrieve All Books**

**Related Scenario ID:** TS-B001  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /books

**Objective:  
** Verify that the API retrieves all available books with the correct response structure and details.

**Preconditions:**

- Common preconditions are satisfied.

- A known collection of books exists.

- Expected book IDs and values are available for comparison.

**Test Data:  
** No request body.

**Steps:**

- ~~Open Postman.~~

- ~~Select **GET** and enter http://localhost:4000/books.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the response body is a JSON array.~~

- ~~Verify that each book contains id, title, author, publicationDate, and ISBN.~~

- ~~Compare the returned IDs, values, and count with the prepared dataset.~~

**Expected Result:  
** The API returns 200 OK and a JSON array containing all expected books with the correct fields and values.

## **TC-CREATEBOOK-B002: Create Book Using Valid Data**

**Related Scenario ID:** TS-B002  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** POST /books

**Objective:  
** Verify that valid book information creates a new book that can subsequently be retrieved.

**Preconditions:**

- Common preconditions are satisfied.

- The payload satisfies the API’s validation rules.

- The test data does not conflict with existing records if uniqueness is required.

**Test Data:**

{

"title": "Software Testing Fundamentals",

"author": "QA Test Author",

"publicationDate": "2026-08-27",

"ISBN": "978-1234567897"

}

**Steps:**

- ~~Select **POST** and enter http://localhost:4000/books.~~

- ~~Select **Body → raw → JSON**.~~

- ~~Enter the valid test data.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the response contains a generated ID and the submitted field values.~~

- ~~Record the generated ID.~~

- ~~Send GET /books/{id} using that ID and compare the retrieved values with the submitted data.~~

**Expected Result:  
** The POST request returns 201 Created with a generated ID and the submitted book details. The subsequent GET returns 200 OK with the same book.

## **TC-CREATEBOOK-B003: Create Book With Empty JSON Object**

**Related Scenario ID:** TS-B003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /books

**Objective:  
** Verify that creation is rejected when no required book fields are included in the JSON object.

**Preconditions:**

- Common preconditions are satisfied.

- The initial book collection can be recorded for comparison.

**Test Data:**

{}

**Steps:**

- ~~Send GET /books and record the existing book IDs and count.~~

- ~~Select **POST** and enter http://localhost:4000/books.~~

- ~~Select **Body → raw → JSON** and enter {}.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and validation response.~~

- ~~Send GET /books again.~~

- ~~Compare the collection with the initial records to confirm that no book was created.~~

**Expected Result:  
** The API returns 400 Bad Request with validation errors for the required book information. No new book is created.

## **TC-CREATEBOOK-B004: Create Book With Missing ISBN**

**Related Scenario ID:** TS-B003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /books

**Objective:  
** Verify that creation is rejected when ISBN is omitted while the other required fields contain valid values.

**Preconditions:**

- Common preconditions are satisfied.

- ISBN is required for book creation.

- The other submitted fields satisfy the validation rules.

**Test Data:**

{

"title": "API Testing Guide",

"author": "QA Test Author",

"publicationDate": "2026-08-27"

}

**Steps:**

- ~~Send GET /books and record the initial collection.~~

- ~~Select **POST** and enter http://localhost:4000/books.~~

- ~~Enter the test data with the ISBN field completely omitted.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the validation response identifies the ISBN field.~~

- ~~Verify that the valid fields do not produce unrelated validation errors.~~

- ~~Send GET /books again and confirm that no new record was created.~~

**Expected Result:  
** The API returns 400 Bad Request with an ISBN validation error. The valid fields do not produce validation errors, and no book is created.

## **TC-RETBOOK-B005: Retrieve Existing Book by ID**

**Related Scenario ID:** TS-B004  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** GET /books/{id}

**Objective:  
** Verify that an existing book can be retrieved using its ID and that the returned details are correct.

**Preconditions:**

- Common preconditions are satisfied.

- The target book exists.

- Its ID and expected field values are known.

- The record has not been changed or deleted before this test.

**Test Data:**

- **Book ID:** A confirmed existing ID.

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/books/{id} using the existing ID.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the response contains a JSON book object.~~

- ~~Verify that the returned ID matches the requested ID.~~

- ~~Compare title, author, publicationDate, and ISBN with the expected record.~~

**Expected Result:  
** The API returns 200 OK with the correct book ID and stored book details.

## **TC-RETBOOK-B006: Retrieve Book Using Nonexistent ID**

**Related Scenario ID:** TS-B005  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** GET /books/99999

**Objective:  
** Verify that retrieving a nonexistent book returns a not-found response.

**Preconditions:**

- Common preconditions are satisfied.

- Book ID 99999 is confirmed absent from the test dataset.

**Test Data:**

- **Book ID:** 99999

- **Request body:** None.

**Steps:**

- ~~Select **GET**.~~

- ~~Enter http://localhost:4000/books/99999.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the response indicates the book does not exist.~~

- ~~Verify that no book record is returned.~~

**Expected Result:  
** The API returns 404 Not Found with a not-found error and no book data for ID 99999.

## **TC-UPDBOOK-B007: Update Existing Book Using Valid Data**

**Related Scenario ID:** TS-B006  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** PUT /books/{id}

**Objective:  
** Verify that valid data updates an existing book and that the updated values are saved.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable book exists with known original values.

- Its ID is known.

- The submitted title differs from its current title.

- The update payload satisfies the validation rules.

**Test Data:**

{

"title": "Advanced Software Testing",

"author": "QA Test Author",

"publicationDate": "2026-08-27",

"ISBN": "978-1234567897"

}

**Steps:**

- ~~Send GET /books/{id} and record the original book values.~~

- ~~Select **PUT** and enter the same book URL.~~

- ~~Enter the valid update payload.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code.~~

- ~~Verify that the response contains the same ID and the submitted field values.~~

- ~~Send GET /books/{id} again.~~

- ~~Verify that the retrieved record contains the updated values.~~

**Expected Result:  
** The PUT request returns 200 OK with the same book ID and the submitted values. A subsequent GET confirms that the updated details were saved.

## **TC-UPDBOOK-B008: Update Book With Invalid ISBN**

**Related Scenario ID:** TS-B007  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /books/{id}

**Objective:  
** Verify that an invalid ISBN is rejected during an update and that the existing record remains unchanged.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable book exists with a valid ISBN.

- Its complete original values are known.

- ISBN validation is required during updates.

- All submitted fields except ISBN are valid.

**Test Data:**

{

"title": "Advanced Software Testing",

"author": "QA Test Author",

"publicationDate": "2026-08-27",

"ISBN": "INVALID-ISBN"

}

**Steps:**

- ~~Send GET /books/{id} and record all original field values.~~

- ~~Select **PUT** and enter the same book URL.~~

- ~~Enter the payload containing INVALID-ISBN.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and ISBN validation response.~~

- ~~Send GET /books/{id} regardless of the PUT response status.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** The API returns 400 Bad Request with an ISBN validation error. The original valid ISBN and all other stored values remain unchanged.

## **TC-DELBOOK-B009: Delete Existing Book**

**Related Scenario ID:** TS-B009  
**Test Type:** Functional / Positive  
**Priority:** High  
**Endpoint:** DELETE /books/{id}

**Objective:  
** Verify that an existing book can be deleted and is no longer retrievable.

**Preconditions:**

- Common preconditions are satisfied.

- The target book exists.

- The record is disposable and is not required by another pending test.

**Test Data:**

- **Book ID:** A confirmed existing disposable book ID.

- **Request body:** None.

**Steps:**

- ~~Send GET /books/{id} and confirm that the intended record exists.~~

- ~~Select **DELETE** and enter the same book URL.~~

- ~~Click **Send**.~~

- ~~Verify the deletion response status.~~

- ~~Send GET /books/{id} afterward.~~

- ~~Verify that the book can no longer be retrieved.~~

**Expected Result:  
** The DELETE request returns 200 OK. A subsequent GET for the same ID returns 404 Not Found with no book data.

## **TC-DELBOOK-B010: Delete Nonexistent Book**

**Related Scenario ID:** TS-B010  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** DELETE /books/99999

**Objective:  
** Verify that deleting a nonexistent book returns a not-found response without affecting existing records.

**Preconditions:**

- Common preconditions are satisfied.

- Book ID 99999 is confirmed absent.

- At least one other book exists for checking unintended changes.

**Test Data:**

- **Book ID:** 99999

- **Request body:** None.

**Steps:**

- ~~Send GET /books and record the existing book IDs and values.~~

- ~~Select **DELETE** and enter http://localhost:4000/books/99999.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and not-found response.~~

- ~~Send GET /books again.~~

- ~~Compare the records by ID and values, ignoring array order.~~

- ~~Verify that no existing book was removed or changed.~~

**Expected Result:  
** The API returns 404 Not Found. Existing book records remain unchanged.

## **TC-UPDBOOK-B011: Update Nonexistent Book**

**Related Scenario ID:** TS-B008  
**Test Type:** Functional / Negative  
**Priority:** Medium  
**Endpoint:** PUT /books/99999

**Objective:  
** Verify that updating a nonexistent book is rejected without creating a new record or changing existing records.

**Preconditions:**

- Common preconditions are satisfied.

- Book ID 99999 is confirmed absent.

- The API requirements specify that this endpoint updates existing books only.

- The request body satisfies all unrelated validation rules.

**Test Data:**

{

"title": "Advanced Software Testing",

"author": "QA Test Author",

"publicationDate": "2026-08-27",

"ISBN": "978-1234567897"

}

**Steps:**

- ~~Send GET /books and record the initial collection.~~

- ~~Select **PUT** and enter http://localhost:4000/books/99999.~~

- ~~Enter the valid payload.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and not-found response.~~

- ~~Send GET /books/99999 and verify that the target remains absent.~~

- ~~Send GET /books and confirm that no records were created or changed.~~

**Expected Result:  
** Under the update-only requirement, the API returns 404 Not Found. The target remains absent, and existing records are unchanged.

## **TC-CREATEBOOK-B012: Create Book With Invalid ISBN**

**Related Scenario ID:** TS-B003  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** POST /books

**Objective:  
** Verify that creation rejects an invalid ISBN while the other required fields contain valid values.

**Preconditions:**

- Common preconditions are satisfied.

- The ISBN validation rule is confirmed.

- All other submitted values satisfy the API requirements.

**Test Data:**

{

"title": "API Testing Guide",

"author": "QA Test Author",

"publicationDate": "2026-08-27",

"ISBN": "INVALID-ISBN"

}

**Steps:**

- ~~Send GET /books and record the initial collection.~~

- ~~Select **POST** and enter http://localhost:4000/books.~~

- ~~Enter the payload containing INVALID-ISBN.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and ISBN validation error.~~

- ~~Verify that the valid fields do not produce unrelated validation errors.~~

- ~~Send GET /books again and confirm that no new book was created.~~

**Expected Result:  
** The API returns 400 Bad Request with an ISBN validation error. No book is created, and the existing collection remains unchanged.

## **TC-UPDBOOK-B013: Update Book With Missing ISBN**

**Related Scenario ID:** TS-B007  
**Test Type:** Negative / Validation  
**Priority:** High  
**Endpoint:** PUT /books/{id}

**Objective:  
** Verify that an update is rejected when ISBN is omitted, where the update requirements make ISBN mandatory.

**Preconditions:**

- Common preconditions are satisfied.

- A disposable book exists with a valid ISBN.

- Its original values are known.

- **The API requirements confirm that ISBN must be included in every PUT request.**

**Test Data:**

{

"title": "Advanced Software Testing",

"author": "QA Test Author",

"publicationDate": "2026-08-27"

}

**Steps:**

- ~~Send GET /books/{id} and record the original values.~~

- ~~Select **PUT** and enter the same book URL.~~

- ~~Enter the payload with ISBN completely omitted—not blank or null.~~

- ~~Click **Send**.~~

- ~~Verify the HTTP status code and ISBN validation error.~~

- ~~Send GET /books/{id} again.~~

- ~~Compare every stored field with the original record.~~

**Expected Result:  
** If ISBN is mandatory during updates, the API returns 400 Bad Request with an ISBN validation error. The existing ISBN and all other stored values remain unchanged.
