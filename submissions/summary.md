# Test Summary 


---

## 1. Group information 

| Attributes | Information |
|-----|----------|
| **Group** | `Nhóm 17` |
| **Class** | `STQA2A` |
| **Report date** | `02/06/2026` |
| **Tested system** | https://stqa.rbc.vn — v1.0 |
| **REPO** | https://github.com/USTH-STQA-2026/stqa-automation-testing-stqa_group_17 |

---

## 2. Results overview

| Attribute| Value |
|--------|---------|
| Total test cases| `38` |
| Pass | `28` |
| Fail | `10` |
| Blocked | `0` |
| Not Run | `0` |
| **Pass Rate** | `73.6%` |
| **Bugs Reported** | `9` |

### Distribution by functional group

| Functional Group| TC | Pass | Fail | Bug | Review |
|---------------|-----|------|------|-----|---------|
| Login (REQ-01) | 6 | 6 | 0 | 0 | ✅ Good — working as intended |
| View book list (REQ-02) | 2 | 2 | 0 | 0 | ✅ Good — working as intended |
| Search Function (REQ-03) | 7 | 5 | 2 | 2 | ⚠️ Contain bugs — uppercase/lowercase normalization |
| Borrow book (REQ-04) | 5 | 3 | 2 | 2 | ⚠️ Contains volatile bugs — exceed 3-books limit |
| Return book (REQ-05) | 2 | 1 | 1 | 1 | ⚠️ Contains bug - system does not have an overdue warning |
| Overdue handling (REQ-06) | 5 | 5 | 0 | 0 | ✅ Good — Working as intended |
| Member management (REQ-07) | 7 | 3 | 4 | 3 | ⚠️ Contain bugs - email validation  |
| Record lookup (REQ-08) | 4 | 3 | 1 | 1 | ⚠️ Contain bugs — violates security requirements |
| **Total** | **38** | **28** | **10** | **9** | |

### Distribute bug by severity

| Severity | Quantity | Bug IDs |
|--------|---------|---------|
| High | 7 | BUG-01, BUG-02, BUG-03, BUG-04, BUG-06, BUG-07, BUG-09 |
| Medium | 1 | BUG-05 |
| Low | 1 | BUG-08 |

---

## 3. Techniques used 

| Technique | REQ covered | Application |
|----------|--------------------|------------------------|
| **EP** (Equivalence Partitioning) | REQ-01 → REQ-08 | Divided inputs into equivalence classes: valid / invalid / empty. For example: existing / non-existing email, active / suspended / expired account. |
| **BVA** (Boundary Value Analysis) | REQ-01, REQ-04, REQ-05, REQ-06 | Tested boundary values: empty input fields, number of borrowed books exactly at the 3-book limit, expiration date exactly today / overdue. |
| **Negative Testing** | REQ-01, REQ-03, REQ-07 | Deliberately entered invalid data and violated business constraints to verify the system handles errors correct. Such as empty field, wrong password, invalid email, invalid user name and non existence data |
| **Decision Table** | REQ-04, REQ-05 | Mapped out complex, multi-conditional business logic combining distinct rules. Used to verify combinations like: Account Status (Active/Suspended/Expired) + Book Status (Available/Borrowed/Lost) + Book Borrowed (<3 / =3)  to determine whether the final action (Allow/Reject Borrowing) was executed correctly. |

---

## 4. Software Quality Analysis

### 4.1. Strengths

- **Login** (REQ-01): Email/password authentication functions accurately. Error messages are clear and user-friendly. Empty field validation works properly.
- **View book list (REQ-02)**: All book information (title, author, publication year, status) is fully and accurately displayed.
- **Borrow/Return function (REQ-04)**: Blocks borrowing when a book is already borrowed, the account is suspended, or the account is expired — all work correctly..
- **Overdue Handling (REQ-06)**: Role separation between librarian and member is distinct. The system correctly marks overdue records based on the exact date.
- **Record Lookup (REQ-08)**: Librarians can view all records.

### 4.2. Weakness

- **Member management(REQ-07) — MOST CRITICAL**: The add member function has 3 simultaneous defects:
  - Unable to add a member with a valid email → core functionality is completely broken.
  - Accepts malformed emails (missing a .) → allows bad data into the system.
  - Displays an incorrect error message when an email is duplicated → causes confusion for users.
- **Book borrowing limit (REQ-04) — Critical**: The system allows borrowing a 4th book despite a maximum limit of 3. This is a direct violation of the business rule
- **Searching by category (REQ-03)**: The category filter is case-sensitive. Users entering kinh tế or KINH TẾ get no results — leading to a very poor user experience.
- **Data Security (REQ-08) — Critical**: Members can view other members' loan records simply by entering another member's ID into the search box → violates data privacy.

---

## 5. Fix suggestions


| Order | Bug | Severity | Reason for priority |
|--------|-----|--------|---------------|
| 🔴 1 | **BUG-06** — Cannot add member despite correct input | High | The add member function **does not work at all** — librarians cannot manage the system. |
| 🔴 2 | **BUG-09** — Members can view others' borrowing records | High | **Violates privacy and security** — data leak |
| 🔴 3 | **BUG-04** — Allows borrowing a 4th book (exceeding limit of 3) | High | **Violates business rule** - compromises the integrity of borrow data. |
| 🟠 4 | **BUG-07** — System added member successfully with incorect email syntax | High | Bad data (invalid emails) enters the database, causing long-term consequences. |
| 🟠 5 | **BUG-03** — Incorrect error message when trying to borrow a book as a suspended member | High | **Violate business requirement** Incorrect error message that will lead to bad user experience. |
| 🟠 6 | **BUG-01** — Category search yields no results for lowercase input | High | Directly impacts user experience when searching for books. |
| 🟠 7 | **BUG-02** — Category search yields no results for UPPERCASE input| High | Directly impacts user experience when searching for books. |
| 🟠 8 | **BUG-05** — Overdue message does not pop up correctly| Medium | **Violate business requirement** May lead to bad user experience |
| 🟡 9 | **BUG-06** — Incorrect error message on duplicate email | Low | Confuses the librarian but does not affect data integrity. |

---

## 6. Conclusion

**The system is not ready for release.**

After executing all 34 test cases across 8 major functions, the team recorded a pass rate of **73.6%** with **9 bugs** detected, **7 of which are High severity**. Specifically:

- The **Member management (REQ-07)** function is practically **non-functional** — librarians cannot add valid members to the system, yet the system incorrectly accepts invalid email formats.
- The **Borrow book (REQ-04)** functions violate the 3-book limit — compromising the integrity of transaction data.
- The **Record lookup (REQ-08)** function contains a critical access control vulnerability — violating member privacy.

Functions operating well include: Login, View book list, Overdue handling, and search by title/author.

**Recommendation**: Prioritize immediate fixes for BUG-06, BUG-09, and BUG-04 before deployment. Full regression testing for REQ-07 and REQ-08 is mandatory post-fix.

---

## 7. Lesson learned

- **Designing test cases before execution** ensures even coverage across all paths (happy path, negative, boundary) and prevents overlooking crucial features.
- **BVA is highly effective** for numeric boundaries (the 3-book limit) — without BVA, BUG-04 could easily have been missed.
- **Authorization (permission control)** is easily neglected but has a massive security impact. It is vital to test permissions for every role across each feature.
- **Error messages require dedicated testing** — defects are not just "broken features" but also "misleading notifications" (like BUG-08) that confuse users.
- Utilizing **IDM (Input Domain Modeling)** prior to writing test cases helps the team systematically organize test scenarios and guarantees no major partitions are missed.

---

## 8. AI usage

| AI Tool | Used for | How you verified/edited |
|------------|-------------------|-----------------------------------|
| Gemini | Assisted in compiling the summary report based on actual existing data | All statistics (TCs, Pass/Fail, Bugs) were drawn directly from the team's actual execution results. Double-checked each item before submission. |
