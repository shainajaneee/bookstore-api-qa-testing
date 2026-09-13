# Penetration Test Scenarios

| **Scenario ID** | **Test Scenario**                                                                  | **Test Type**                   | **Priority** |
|-----------------|------------------------------------------------------------------------------------|---------------------------------|--------------|
| TS-PEN-001      | Verify whether API resources can be accessed and modified without authentication.  | Access Control Testing          | High         |
| TS-PEN-002      | Verify whether another user’s record can be accessed by changing the user ID.      | IDOR/Authorization Testing      | High         |
| TS-PEN-003      | Verify that unexpected privileged fields cannot be assigned during user creation.  | Mass Assignment Testing         | High         |
| TS-PEN-004      | Verify that manipulated resource IDs are handled safely                            | Parameter Manipulation          | Medium       |
| TS-PEN-005      | Verify that injection-like payloads cannot alter API behavior or expose records.   | Injection Testing               | High         |
| TS-PEN-006      | Verify that an HTTP method override cannot perform an unintended operation.        | HTTP Method Manipulation        | Medium       |
| TS-PEN-007      | Verify that repeated requests do not cause the API to crash or become unavailable. | Rate-Limit/Availability Testing | Medium       |
