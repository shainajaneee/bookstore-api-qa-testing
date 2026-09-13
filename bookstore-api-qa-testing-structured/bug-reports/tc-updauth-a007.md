# TC-UPDAUTH-A007 Update Author With Invalid Books Format

**Description:  
** Verify that the Authors API rejects an update when books is supplied as a string instead of an array through PUT /authors/{id}.

**Key Functionalities:**

- Validate that books is an array.

- Reject invalid field types.

- Return an appropriate validation error and HTTP status code.

- Preserve the existing author information when validation fails.

**Expected Result:  
** The API should return 400 Bad Request with a validation error indicating that books must be an array. The stored author record should remain unchanged.

**Actual Result:  
** The API returned 200 OK for author ID 1. The response contained "books": "NOT-AN-ARRAY" instead of an array, and no validation error was returned.

![Test evidence](../images/image58.png)

![Test evidence](../images/image64.png)

Status: Open
