# Test Execution — Kết quả thực thi kiểm thử



| Attributes | Value |
|---|---|
| **Group** | `Nhóm 17` |
| **Execution date** | `16/05/2026` |
| **Browser** | Firefox `139.0` |
| **Operating System** | `Linux` |

---

## Detailed Results

### REQ-01 - Login
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-01 | Login | Login successfully | Login successfully | Pass| | |
| TC-02 | Login | Display incorrect password error | Display incorrect password error | Pass | | |
| TC-03 | Login | Display account not found error | Display account not found error | Pass | | |
| TC-04 | Login | Display warning: "Please enter email" | Display warning: "Please enter email" | Pass | | |
| TC-05 | Login | Display warning: "Please enter password" | Display warning: "Please enter password" | Pass | | |
| TC-06 | Login | Display warning: "Please enter email and password" | Display warning: "Please enter email and password" | Pass | | |

### REQ-02 - Book list
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-07 | Book list | List displays successfully with complete information | List displays successfully with complete information | Pass | | |
| TC-08 | Book list | Book status updates in real-time | Book status updates in real-time | Pass | | |

### REQ-03 - Search Function
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-09 | Search Function | Display books containing "Flutter" | Display books containing "Flutter" | Pass | | |
| TC-10 | Search Function | Display books written by authors named "Nguyễn" | Display books written by authors named "Nguyễn" | Pass | | |
| TC-11 | Search Function | Display an empty list | Display an empty list  | Pass | | |
| TC-12 | Search Function | Display books belonging to the `"Kinh tế"` category | Display books belonging to the `"Kinh tế"` category | Pass | | |
| TC-13 | Search Function | Display books belonging to the `"Kinh tế"` category | Displays an empty list | Fail | | BUG-01|
| TC-14 | Search Function | Display books belonging to the `"Kinh tế"` category | Displays an empty list | Fail | | BUG-02 |
| TC-15 | Search Function | Display books containing "Flutter" | Display books containing "Flutter" | Pass | | |

### REQ-04 - Borrow
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-16 | Book Borrow | Borrow book successfully | Borrow book successfully | Pass | | |
| TC-17 | Book Borrow | Block borrowing transaction | Block borrowing transaction| Pass | | |
| TC-18 | Book Borrow | Block borrowing; display account suspended message | Block borrowing; display account expired message | Fail | | BUG-03 |
| TC-19 | Book Borrow | Block borrowing; display account expired message | Block borrowing; display account expired message | Pass | | |
| TC-20 | Book Borrow | Reject transaction; display borrow limit exceeded message | Allowed to borrow the 4th book | Fail | | BUG-04 |

### REQ-05 - Borrow
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-21 | Book Return | Book returned successfully; no overdue warning displayed | Book returned successfully; no overdue warning displayed | Pass | | |
| TC-22 | Book Return | Book returned successfully; system displays overdue warning | Book returned successfully; no overdue warning displayed | Fail | | | BUG-05 |

### REQ-06 - Overdue Handling
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-23 | Overdue Handling | "Check Overdue Books" button is visible | "Check Overdue Books" button is visible | Pass | | |
| TC-24 | Overdue Handling | "Check Overdue Books" button is hidden | "Check Overdue Books" button is hidden | Pass | | |
| TC-25 | Overdue Handling | Record `BR001` status updates to "Overdue" |Record `BR001` status updates to "Overdue" | Pass | | |
| TC-26 | Overdue Handling |New record status remains as "Borrowing" | New record status remains as "Borrowing" | Pass | | |
| TC-27| Overdue Handling | Able to see personal borrow records flagged as "Overdue" |Able to see personal borrow records flagged as "Overdue" | Pass | | |

### REQ-07 - Member Management
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-28 | Member Management | "Add Member" button is visible | "Add Member" button is visible | Pass | | |
| TC-29 | Member Management | Member account successfully created | System throws an invalid email error | Fail | | BUG-06|
| TC-30 | Member Management | Display error: full name field cannot be empty | Display error: full name field cannot be empty | Pass | | |
| TC-31 | Member Management | Display invalid email format warning | Display invalid email format warning | Pass | | |
| TC-32 | Member Management | Display invalid email format warning | Member account successfully created | Fail | | BUG-07 |
| TC-33 | Member Management | Display error: email already exists in the system | Display invalid email format warning | Fail | | BUG-08 |
| TC-34 | Ticket Lookup | Display invalid phone number error | Display invalid email format warning (Blocked by BUG-05) | Failed | | |

### REQ-08 Ticket Lookup
| TC-ID | Functional Group | Expected result | Actual result | Verdict | Proof | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-35 | Ticket Lookup | Able to view borrow records across all members  | Able to view borrow records across all members | Pass | | |
| TC-36 | Ticket Lookup | Isolates data and only exposes personal records| Isolates data and only exposes personal records | Pass | | |
| TC-37 | Ticket Lookup | Blocks cross-account access | Displays data belong to member `MEM003` | Fail | | BUG-09 |
| TC-38 | Ticket Lookup | Correctly reveals exhaustive ticket information | Correctly reveals exhaustive ticket information | Pass | | |


---

## Summary of Results

| Metric | Value |
|--------|---------|
| Total test cases | `38` |
| Pass | `28` |
| Fail | `10` |
| Blocked | `` |
| Not Run | `0` |
| **Pass rate** | `73%` |

### Results by Functional Area

| Group | Total Test Case | Pass | Fail | Pass rate |
|------|---------|------|------|------------|
| Login | 6 | 6 | 0 | 100% |
| Book List | 2 | 2 | 0 | 100% |
| Search Function | 7 | 5 | 2 | 71%
| Book Borrow| 5 | 3 | 2 | 60% | 
| Book Return| 2 | 1 | 1 | 50% |
| Overdue Handling | 5 | 5 | 0 | 100%
| Member Management | 7 | 3 | 3| 42%
| Ticket Lookup | 4 | 3 | 1 | 75%

