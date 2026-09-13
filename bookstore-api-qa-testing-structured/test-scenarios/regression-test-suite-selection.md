# Regression Test Suite Selection

Selected based on: high-priority core CRUD paths (one per module) + all confirmed defect cases + the concurrency observation.

| **TC ID**          | **Module**   | **Reason for Inclusion**                           |
|--------------------|--------------|----------------------------------------------------|
| TC-RETBOOKS-B001   | Books        | Core read path, high priority                      |
| TC-CREATEBOOK-B002 | Books        | Core write path, high priority                     |
| TC-B007 / TS-B007  | Books        | Previously failed (invalid ISBN accepted)          |
| TC-UPDAUTH-A007    | Authors      | Previously failed (invalid books type accepted)    |
| TC-UPDUSER-U006    | Users        | Previously failed (invalid email accepted)         |
| TC-UNIT-B001–B004  | Books        | Automated regression coverage (Jest)               |
| TC-UNIT-A001–A004  | Authors      | Automated regression coverage (Jest)               |
| TC-UNIT-U001–U004  | Users        | Automated regression coverage (Jest)               |
| OBS-001            | Cross-module | Re-verify concurrency behavior under repeated load |
