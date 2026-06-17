# Test Cases 


| Attributes | Values |
|---|---|
| **Group** | `Nhóm 17` |
| **Creation Date** | `17/05/2026` |
| **System** | https://stqa.rbc.vn |
| **Reference** | SRS v1.0 |

---

## 1. Input Domain Modeling (IDM)

### IDM — Login (REQ-01)

| Characteristic | Block | Value | Expected Results |
|---|---|---|---|
| Existing Email | Valid librarian account | `librarian@library.com` | Login successful |
| | Valid member account | `ba.nguyen@email.com` | Login successful
| | Non-existing email | `noone@email.com` | Display error message: "Member not found" |
| Password | Correct password | `admin123` | Login succesfully |
| | Incorrect password | `wrongpass` | Display error message: Incorrect password |
| Input fields | Both fields filled | valid email + valid password | Login process continues |
| | Both fields empty | Email: ""<br />  Password: "" | Display error message: "Please enter email and password" |
| | Empty email only | Email: "" <br /> Password: `admin123` | Display error message: "Please enter email"
| | Empty password only | Email: `librarian@library.com` <br /> Password: ""| Display error message: Please enter password


### IDM — View book list (REQ-02)

| Characteristic | Block | Value | Expected Results |
|---|---|---|---|
| User role | Librarian | `librarian@library.com` | Able to view the book list
| | Member | `ba.nguyen@gmail.com` | Able to view the book list
| Book Status | Available | `BOOK001` | Displayed status: "Available"
| | Borrowed | `BOOK003` | Displayed status: "Borrowed"
| | Lost | `BOOK007` | Displayed status: Lost  
| Book Information Display | Complete book information | `BOOK001` | System displays title, author, genre, published year of `BOOK001`
| Real-time update | After borrowing a book  | `BOOK001` | Status changes to "Borrowed" instantly
| | After returning a book | `BOOK003` | Status changes to "Available" instantly  

### IDM — Search Function (REQ-03)

| Characteristic | Block | Value | Expected Results |
|---|---|---|---|
| Keywords exist in DB? | Yes (Book title) | `"Flutter"` | Display books containing "Flutter" |
| | Yes (author name) | `"Nguyễn"` | Display books by Nguyễn |
| | No | `"XYZ123"` | Display error message: Books not found |
| Case sensitivity| Lowercase | `"flutter"` | Display books containing "Flutter" |
| | Uppercase | `"FLUTTER"` | Display books containing "Flutter" |
| | Lowercase | `"kinh tế"` | Same results as "Kinh tế"
| | Uppercase | `"KINH TẾ"` | Same results as "Kinh tế"


### IDM — Borrow (REQ-04)

| Characteristic | Block | Value | Expected results |
|---|---|---|---|
| Book status | Available | BOOK001 | Allow |
| | Borrowed | BOOK003 | Reject |
| | Lost | BOOK007 | Reject |
| Member Status | Active | MEM002 | Allow |
| | Suspended | MEM004 | Reject, display error message |
| | Expired| MEM005 | Reject, display error message |
| Number of borrowed books| < 3 (BVA: 0, 1, 2) | MEM006 (0 book) | Allow|
| | = 3 (BVA: boundary) | MEM has borrowed 3 books | Reject, display "exceeded limit" error |
| | >3 | MEM has borrowed more than 3 books | Reject, display "exceeded limit" error


### IDM — Return (REQ-05)
| Characteristic | Block | Value | Expected results |
|---|---|---|---|
| Borrow record status | Borrowing | `BR001` | Allow return
| | Returned | `BR004` | Can not return
| Due date compared to current date | currentDate < dueDate | `10/09/2024 < 15/09/2024` | Return book sucessfully without warning
| | currentDate = dueDate | `15/09/2024 = 15/09/2024` | Return book sucessfully and display overdue warning
| | currentDate > dueDate | `15/06/2026 > 15/09/2024` | Return book sucessfully and display overdue warning
| Record Owner | Record belongs to current member | `BR001` (`MEM002`) | `MEM002` can view borrowing record and return |
| | Record does not belong to current member  | `BR001` (`MEM002`), current member is: `MEM003` | Can not view the record or return the book 

### IDM — Overdue Handling (REQ-6)

| Characteristic | Block | Value | Expected Results |
|---|---|---|---|
| User Role | Librarian| `librarian@library.com` | Have access to the "Check Overdue" function | 
| | Member | `ba.nguyen@gmail.com` | Does not have access to the "Check Overdue" function |
| Due date compared to current date | dueDate <= currentDate | 15/09/2024 <= 15/06/2026| Record marked as "Overdue" |
| | dueDate > currentDate | 31/06/2026 > 15/06/2026  | Record is not marked as "Overdue" |
| Record Owner | Record belongs to current member | `BR001` (`MEM002`) | `MEM002` can view borrowing record and return |
| | Record does not belong to current member  | `BR001` (`MEM002`), current member is: `MEM003` | Can not view the record or return the book | 

### IDM — Member Management (REQ-7)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| User Role | Librarian | `librarian@library.com` | Able to view "Add member" button |
| | User | `ba.nguyen@gmail.com` | Unable to view "Add Member" button | 
| User Name | Valid | Tester | Accept |
| | Empty field | " " | Display error message "Please enter your username" |
| Email | valid | `Tester@email.com` | Acccept |
| | Empty field | " " | Display error "Please enter your email" |
| | Missing "@" | `Emailtestemail.com` | Display error message "Please enter your email" |
| | Missing "." | `Emailtest@emailcom` | Display error message "Please enter your email" | 
| | Email already exists in DB | `ba.nguyen@gmail.com` | Display error message: "User already exists" |
| Phone number | Valid phone number (contains exactly 10 digits) | 0123456789 | Accept
| | Invalid phone number (does not contain exactly 10 digits) | 012345678 | Reject, display error message "Please enter valid phone number"

### IDM — Record Lookup (REQ-8)

| Characteristic | Block | Value | Expected Results |
|---|---|---|---|
| User Role | Librarian | `librarian@library.com` | Displays all tickets  |
| | Member | `ba.nguyen@gmail.com` | Only display MEM002 records |
| Member ID Lookup | Member search self | `MEM002` search `MEM002` | Display self records | 
| | Member search other member's record | `MEM002` search `MEM003` | No tickets displayed, display "Not Found"  | 
| | ID does not exist| `MEM99` | Display "Not exist" or "Not found" |
| Ticket information | Contains correct information of the ticket | `MEM002` search `MEM002` | Display ticket ID, book name, borrow date, due date and current status | 

## 2. Decision Table - Borrow Book Function
| Rule| Book available| Active Member | Borrowed Book < 3 | Result |
|-----|---------------|---------------|-------------------|--------|
| R1 | YES | YES | YES | Allow borrowing |
| R2 | NO | - | - |  Reject, book is not available
| R3 | YES | Suspended | - | Reject, member is suspeneded |
| R4 | YES | Expired | - | Reject, member is expired 
| R5 | YES | YES | NO | Reject, member exceeds the 3-books limit
  

---

## 3. Test Cases


---

### Test Cases Table — REQ-01: Login
| TC-ID | Test Objective | Preconditions | Test steps | Input values | Exptected Results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Verify successful login with valid account | User have a valid account in the system | 1. Enter `Email`. 2.Enter `Mật khẩu`. 3.Click `Login`  | Email: `librarian@library.com` , Pass: `admin123` | Login successfully | REQ-01  | EP, BVA |
| TC-02 | Verify login with incorrect password | User on the login page | 1.Enter valid email. 2.Enter incorrect password. 3.Click Login | Email: `librarian@library.com` , Pass: `wrongpass` | Display error message: `Incorrect password` | REQ-01 | EP, Negative Testing |
| TC-03 | Verify login with non-existing email | User on the login page | 1.Enter non-existing email 2. Enter password. 3. Click login | Email: `noone@email.com` , Pass: `admin123` | Display error message: "Member not found". | REQ-01 | EP, Negative Testing |
| TC-04 | Verify login with empty email field | User on the login page | 1.Leave email field empty. 2.Enter password. 3.Click Login | Email: `""` , Pass: `admin123` | Display error message:"Please enter email". | REQ-01 | EP, BVA, Negative Testing |
| TC-05 | Verify login with empty password | User on the login page | 1.Enter valid email. 2.Leave password field empty. 3.Click login | Email: `librarian@library.com` <br />Password:`" "`  | Display message: "Please enter passwordd" | REQ-01 | EP,BVA, Negative Testing
| TC-06 | Verify login failure when leaving both fields empty | User is on the login page | 1. Leave both email and password fields empty. 2. Click Login. | Email: `" "` <br />Password: `" "` | Display warning messages: "Please enter email" and "Please enter password". |REQ-01 | EP,BVA, Negative Testing 
---

### Test Cases — REQ-02: View book list 
| TC-ID | Test Objective | Preconditions | Test steps | Input data | Expected Results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-07 | Verify book list displays complete information for both members and librarians | User has a valid account | 1. Log in to the system. 2. Navigate to the "Books" section. 3. View the book list. | Any valid account | The list correctly displays book title, author, publication year, and status. | REQ-02 | EP
| TC-08 | Verify book status updates correctly in real-time | User has a valid account | 1. Log in to the system. 2. Navigate to the "Books" section. 3. View the book list. 4. Click "Confirm". 5. Observe the status.| User has a valid account | The book status updates from "Available" to "Borrowed" instantly. | REQ-02 | EP 
---

### Test Cases — REQ-03: Search Function
| TC-ID | Test objective | Preconditions | Test steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-09 | Find book successfully using a partial book title | Logged into the system | 1. Go to the search bar. 2. Enter the partial title keyword. 3. Click Search. | Keyword:`"Flutter"` | Displays a list of books containing the word "Flutter". | REQ-03 | EP |
| TC-10 | Find book successfully using the author's name | Logged into the system | 1. Go to the search bar. 2. Enter the author's name. 3. Click Search. | Keyword: `"Nguyễn"` | Displays a list of books written by authors named "Nguyễn". | REQ-03 | EP |
| TC-11 | Handle searching for a non-existing book | Logged into the system | 1. Go to the search bar. 2. Enter a random string. 3. Click Search. | Keyword: `"XYZ123"` | Displays an empty list | REQ-03 | EP, Negative Testing |
| TC-12 | Verify search is case-insensitive for book titles | Logged into the system | 1. Go to the search bar. 2. Enter an all-uppercase title. 3. Click Search. | Keyword: `"FLUTTER"` | The displayed result is identical to searching for `"Flutter"`. | REQ-03 | EP |
| TC-13 | Verify search is case-sensitive for genre | Logged into the system | 1. Go to the genre search filter. 2.Enter the genre with mixed lowercase and uppercase. 3.Click search| Keyword: `"Kinh tế"` | Displays all books belonging to the `"Kinh tế"` category. | REQ-03 | EP
| TC-14 | Verify search is case-sensitive for genre | Logged into the system | 1. Go to the genre search filter. 2.Enter the genre with all lowercase. 3.Click search | Keyword: `"kinh tế"` | Displayed search result is identical to searching for `"Kinh tế"` | REQ-03 | EP
| TC-15 | Verify search is case-sensitive for genre | Logged into the system | 1. Go to the genre search filter. 2.Enter the genre with all uppercase 3.Click search | Keyword: `"KINH TẾ"` | Displayed search result is identical to searching for `"Kinh tế"` | REQ-03 | EP
---

### Test Cases — REQ-04 - Borrow
| TC-ID | Test objectives | Preconditions | Test steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-16 | Successfully borrow a book under ideal conditions | Logged in with an Active Member account (`MEM002`) | 1. Select a book with "Available" status. 2. Click Borrow Book. | Book: `BOOK001` Currently borrowed: 0 | The system allows borrowing and successfully creates a borrow record. | REQ-04, 05 | EP, BVA, Decision Table |  
| TC-17 | Block borrowing a book that is already borrowed by someone else | Logged in with an Active Member account(`MEM002`) | 1. Find a book with "Borrowed" status. 2. Attempt to click Borrow Book. | Book: `BOOK003` | The borrow button is disabled or the system throws an unavailable error. | REQ-04, 05 | EP, Decision Table |
| TC-18 | Block borrowing when the account status is Suspended | Logged in with a Suspended account (`cu.le@email.com`) | 1. Select an "Available" book. 2. Click Borrow Book. | Book: `BOOK001` Account: Suspended | Borrowing is rejected; system displays a message that the account is suspended. | REQ-04, 05 | EP, Decision Table |
| TC-19 | Block borrowing when the account status is Expired | Logged in with an Expired account (`binh.pham@email.com`) | 1. Select an "Available" book. 2. Click Borrow Book. | Book: `BOOK001` Account: Expired| Borrowing is rejected; system displays a message that the account has expired. | REQ-04, 05 | EP, Decision Table |
| TC-20 | Block borrowing when the member reaches the maximum limit (3 books) | Logged in with a member account that already has 3 books  | 1. Select an "Available" book. 2. Click Borrow Book. | Book: `BOOK001` Sách đang mượn: 3 | Borrowing is rejected; system displays a "borrow limit exceeded" error.| REQ-04, 05 | EP,BVA,Decision Table |

---
### Test Cases — REQ-05: Return
| TC-ID | Test objectives | Preconditions | Test steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-21 | Return a book successfully before the due date | Logged in with an Active Member account (`MEM002`) | 1.Access borrow/return tab. 2.Select an active record that is not overdue. 3.Click return book.  | - | -Book is returned successfully<br />-No overdue warning displayed | REQ-04,05 | EP,BVA,Decision Table
| TC-22 | Return overdue books | 1. Access the borrow/return tab. (`MEM002`) | 1.Access borrow/return tab. 2.Select an active record that is overdue. 3.Click return book. | - | -Book is returned successfully<br />-Overdue warning displayed | REQ-04,05 | EP,BVA,Decision Table 
---

### Test Cases — REQ-06: Overdue Handling
| TC-ID | Test objective | Preconditions | Test Steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-23 | Verify authorization for "Check Overdue" button visibility (Librarian) | Logged in with a Librarian account (`librarian@library.com`) | 1. Access the Borrow/Return Management page. | N/A | The "Check Overdue Books" button is visible. | REQ-06 | EP |
| TC-24 | Verify authorization for "Check Overdue" button visibility (Member) | Logged in with a Member account (`ba.nguyen@email.com`) | 1. Access the Borrow/Return/My Tickets page. | N/A | The "Check Overdue Books" button is hidden. | REQ-06 | EP |
| TC-25 | Automatically mark a borrow record as Overdue | Librarian clicks the "Check Overdue" button | 1. System scans all active borrow records. | Record: `BR001` Due Date: 15/09/2024 (<= Today) | The status of record `BR001` is updated to "Overdue". | REQ-06 | EP, BVA |
| TC-26 | Ensure active valid records remain unaffected by overdue check | Librarian clicks the "Check Overdue" button | 1. System scans all active borrow records. | Record: Created today <br />(Due Date > Current Date) | The record status remains safely as "Borrowing". | REQ-06 | EP, BVA |
| TC-27 | Display overdue status clearly to the respective member | Logged in as Member `MEM002` (who has an overdue book) | 1. Navigate to "My Borrow Records". | Overdue record in database | The user sees their specific record flagged in red or marked as "Overdue". | REQ-06 | EP |
---

### Test Cases — REQ-07: Member Management
| TC-ID | Test objective | Preconditions | Test Steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-28 | Verify authorization for "Add Member" button visibility | Logged in with a Librarian account | 1. Access the system homepage/dashboard.| Email: `librarian@library.com` <br />Password: `admin123` | The "Add Member" button/feature is fully visible. | REQ-07 | EP |
| TC-29 | Add a member successfully with valid details | Logged in with a Librarian account | 1. Go to Dashboard. 2. Click "Add Member". 3. Fill in all valid fields. 4.Click "add member" | Full name: `Tester` Email:`Tester@email.com` Phone: `0123456789` | Member account is successfully created. | REQ-07 | EP 
| TC-30 | Prevent member creation due to an empty Name field | Librarian is on the Add Member page | 1. Leave the Full Name field blank. 2. Fill in valid Email and Phone. 3. Click "Save". | Full Name: `""` Email: `test@email.com` Phone: `0123456789` | Registration fails; displays error: "Full name cannot be empty". | REQ-07 | EP, BVA, Negative Testing |
| TC-31 | Prevent member creation due to missing "@" in email | Librarian is on the Add Member page | 11. Enter full name. 2. Enter email missing "@". 3. Fill in valid phone number. 4.Click save | Full Name:`Tester` Email: `Emailtestemail.com` Phone: `0123456789` | Registration fails; displays an invalid email format warning. | REQ-07 | EP, Negative Testing |
| TC-32 | Prevent member creation due to missing "." in email domain  |Librarian is on the Add Member page | 1. Enter full name. 2. Enter email missing ".". 3. Fill in valid phone number. 3.click "Save".| Full Name:`Tester` Email: `Emailtest@emailcom` Phone: `0123456789` | Registration fails; displays an invalid email format warning. | REQ-07 | EP, Negative Testing |
| TC-33 | Prevent member creation due to email duplicate conflict | Librarian is on the Add Member page | 1. Enter a name. 2. Enter an email already registered. 3. Click "Save". | Full Name: `Tester` Email: `ba.nguyen@email.com` Phone:`0123456789` | Registration fails; displays error: "User already exists". | REQ-07 | EP, Negative Testing |
| TC-34 | Prevent member creation due to an invalid phone number length | Librarian is on the Add Member page | 1.Enter full name. 2.Enter valid Email. 3. Enter a phone number with fewer than 10 digits. 4.Click save.| Họ tên: `Tester` Email" `Tester@email.com` Phone:`012345678` | Registration fails; displays error message: "Please enter valid phone number". | REQ-07 | EP, Negative Testing  
---

### Test Cases — REQ-08: Record Lookup
| TC-ID | Test objective | Preconditions | Test Steps | Input value | Expected results | REQ | Techniques |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-35 | Allow full system search access for Librarians | Logged in with a Librarian account | 1. Navigate to the Record Lookup feature | N/A | The librarian can view and lookup borrow records across all members. | REQ-08 | EP |
| TC-36 | Restrict Members to only search their personal records |Logged in with Member account `MEM002` | 1. Navigate to the Record Lookup feature. | N/A | The interface isolates data and only exposes records owned by `MEM002`. | REQ-08 | EP |
| TC-37 | Restrict a Member trying to lookup another member's record explicitly | Logged in with Member account `MEM002` | 1. Force search parameter or ID input field with MEM003. | Target search ID: `MEM003` | HThe system blocks cross-account access and displays "Not Found" or "Unauthorized". | REQ-08 | EP |
| TC-38 | Verify lookup details are exhaustive and correctly rendered | User has performed a successful search entry | 1. Enter a valid member code. 2. Press Search. | Search entry : `MEM002` | The display accurately reveals ticket ID, book name, borrow date, due date, and current status. | REQ-08 | EP |
---

## 4. Summary

| Functional Group | Total TC | REQ Covered | Applied IDM Techniques |
|----------------|-------|---------|----------------------|
| Login| 6 | REQ-01 | EP, BVA, Negative Testing |
| View book list| 2 | REQ-02 | EP
| Search Function| 7 | REQ-03 | EP, Negative Testing
| Book Borrow| 5 | REQ-04 | EP, BVA, Decision Table
| Book Return| 2 | REQ-05 | EP, BVA, Decision Table
| Overdue handling| 5 | REQ-06 | EP, BVA 
| Member management | 7 | REQ-07 | EP, BVA, Negative Testing
| Record lookup| 4 | REQ-08 | EP
| Total | 38 | 8 | EP, BVA, Decision Table, Negative Testing |
