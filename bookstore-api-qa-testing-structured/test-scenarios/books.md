# Books Test Scenarios

### **Books** 

| **Scenario ID** | **Test Scenario**                                                                                       | **Test Type**         | **Priority** |
|-----------------|---------------------------------------------------------------------------------------------------------|-----------------------|--------------|
| TS-B001         | Verify that all available books can be retrieved successfully.                                          | Functional / Positive | High         |
| TS-B002         | Verify that a new book can be created using valid data.                                                 | Functional / Positive | High         |
| TS-B003         | Verify that book creation rejects missing required data or invalid field values.                        | Negative / Validation | High         |
| TS-B004         | Verify that an existing book can be retrieved using a valid ID.                                         | Functional / Positive | High         |
| TS-B005         | Verify retrieval using a nonexistent book ID.                                                           | Functional / Negative | Medium       |
| TS-B006         | Verify that an existing book can be updated using valid data.                                           | Functional / Positive | High         |
| TS-B007         | Verify that book updates reject invalid values or missing fields required by the update specifications. | Negative / Validation | High         |
| TS-B008         | Verify updating a nonexistent book using an otherwise valid request body.                               | Functional / Negative | Medium       |
| TS-B009         | Verify that an existing book can be deleted successfully.                                               | Functional / Positive | High         |
| TS-BO10         | Verify deletion using a nonexistent book ID without affecting existing records.                         | Functional / Negative | Medium       |
