# TC-CREATEBOOK-B002 Create Book Regression

**Description:**  
Re-verify that a new book can be successfully created through the POST /books endpoint when valid book information is provided.  
**Key Functionalities:**

- Create a new book record.

- Generate a new book ID.

- Return the created book information with the appropriate status code.

**Expected Result:**  
The API should create the book and return a success status with a generated ID, consistent with original execution.  
**Actual Result:**  
Re-executed via automated Jest/Supertest suite. Returned 201 Created with a generated ID and matching submitted data, consistent with original result.

![Test evidence](../images/image60.png)

Status: Passed
