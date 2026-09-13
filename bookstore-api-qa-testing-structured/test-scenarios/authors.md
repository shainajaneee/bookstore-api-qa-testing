# Authors Test Scenarios

**Authors**

| **Scenario ID** | **Test Scenario**                                                                  | **Test Type**         | **Priority** |
|-----------------|------------------------------------------------------------------------------------|-----------------------|--------------|
| TS-A001         | Verify that all authors can be retrieved successfully.                             | Functional / Positive | High         |
| TS-A002         | Verify a new author can be created using valid data                                | Functional / Positive | High         |
| TS-A003         | Verify author creation using invalid or missing data                               | Negative / Validation | High         |
| TS-A004         | Verify that author creation rejects missing required data or invalid field values. | Negative / Validation | High         |
| TS-A005         | Verify retrieval using a nonexistent author ID.                                    | Functional / Negative | Medium       |
| TS-A006         | Verify an existing author can be updated using valid data                          | Functional / Positive | High         |
| TS-A007         | Verify that author updates reject invalid values or missing required data.         | Negative / Validation | High         |
| TS-A008         | Verify updating a nonexistent author using otherwise valid data.                   | Functional / Negative | Medium       |
| TS-A009         | Verify that an existing author can be deleted successfully.                        | Functional / Positive | High         |
| TS-A010         | Verify deletion using a nonexistent author ID without affecting existing records.  | Functional / Negative | Medium       |
