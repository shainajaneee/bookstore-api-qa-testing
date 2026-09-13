# Users Test Scenarios

**Users**

| **Scenario ID** | **Test Scenario**                                                                | **Test Type**         | **Priority** |
|-----------------|----------------------------------------------------------------------------------|-----------------------|--------------|
| TS-U001         | Verify that all users can be retrieved successfully.                             | Functional / Positive | High         |
| TS-U002         | Verify that a user can be created using valid data.                              | Functional / Positive | High         |
| TS-U003         | Verify that user creation rejects missing required data or invalid field values. | Negative / Validation | High         |
| TS-U004         | Verify that an existing user can be retrieved using a valid ID.                  | Functional / Positive | High         |
| TS-U005         | Verify retrieval using a nonexistent user ID.                                    | Functional / Negative | High         |
| TS-U006         | Verify that an existing user can be updated using valid data.                    | Functional / Positive | Medium       |
| TS-U007         | Verify that an existing user can be deleted successfully.                        | Functional / Positive | High         |
| TS-U008         | Verify deletion using a nonexistent user ID without affecting existing records.  | Functional / Negative | Medium       |
| TS-U009         | Verify that user updates reject invalid values or missing required data.         | Negative / Validation | High         |
| TS-U010         | Verify updating a nonexistent user using otherwise valid data.                   | Functional / Negative | Medium       |
