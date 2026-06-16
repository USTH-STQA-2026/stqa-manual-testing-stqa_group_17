# Bug Reports 



| Information | |
|---|---|
| **Group** | `Group 17` |
| **Report Date** | `16/05/2026` |

**Environment:**
- Browser: Firefox `139`
- Operating System: `Windows 11`
- Interface Language: English

---

## BUG-01 - The category feature is case sensitive and does not return results when lower-case texts are entered

| Attributes | Details |
|-----------|---------|
| **Bug-ID** | BUG-01 |
| **Related TC** | `TC-13` |
| **Related REQ** | `REQ-03` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |

**Prerequisites:**
`Logged into the system as "MEM002", in the "Books" page`

**Steps:**
1. Click on the search bar: Filter by category(e.g. Technology, Economics...)
2. Enter all lower-case string `kinh tế` 
3. Press `Enter`


**Expected results:**
`Display books in the category "Kinh tế" (lower-case should not matter)`

**Actual results:**
`Empty book list, only accept when the user uses the exact form of "Kinh tế"`

**Impact:**
`Affects user experience. Users who type in lower-case may not be able to find books and lead to thinking that the system does not have the book or the filter system is broken even though the book exists in the system`

**Proof:**
![TC-13](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-13.png?raw=true)

**Fix suggestions:**
`Developer can normalize the user input in to the same format` 

---

## BUG-02 - The category feature is case sensitive and does not return results when upper-case texts are entered

| Attribute | Details |
|-----------|---------|
| **Bug-ID** | BUG-02 |
| **Related TC** | `TC-14` |
| **Related REQ** | `REQ-03` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |

**Prerequisites:**
`Logged into the system as "MEM002", in the "Books" page`

**Steps:**
1. Click on the search bar: Filter by category(e.g. Technology, Economics...)
2. Enter all lower-case string `KINH TẾ` 
3. Press `Enter`


**Expected results:**
`Display books in the category "Kinh tế" (upper-case should not matter)`

**Actual results:**
`Empty book list, only accept when the user uses the exact form of "Kinh tế"`

**Impact:**
`Affects user experience. Users who type in lower-case may not be able to find books and lead to thinking that the system does not have the book or the filter system is broken even though the book exists in the system`

**Proof:**
![TC-14](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-14.png?raw=true)

**Fix suggestions:**
`Developer can normalize the user input in to the same format` 

---

## BUG-03 - Allow the user to borrow the 4th book

| Attribute | Details |
|-----------|---------|
| **Bug-ID** | BUG-03 |
| **Related TC** | `TC-20` |
| **Related REQ** | `REQ-04` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |
 
**Prerequisites:**
`Logged in the system as "MEM002", having already borrowed 3 books, books have "Available" status`

**Steps:**
1. Log in the system with as `MEM002`
2. Borrow 4 books with the status `Available`
3. Check the system response

**Expected results:**
`Upon reaching the 4th book, the system must display a warning that there is a 3 books limit and reject additional borrowing`

**Actual results:**
`The system allow the user to borrow the 4th book and only show error when the user attempts to borrow the 5th book`

**Impacts:**
`Violates the business requirements`

**Proof:**
![TC-20](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-20.png?raw=true)

**Fix suggestions**
`Adjust the borrow count logic`

---

## BUG-04 - System does not display overdue warning when returning an overdue book

| Attribute | Detail |
|-----------|---------|
| **Bug-ID** | BUG-04 |
| **Related TC** | `TC-22` |
| **Related REQ** | `REQ-05` |
| **Severity** | `Medium` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `16/06/2026` |
| **Status** | `Open` |
 
**Prerequisites:**
`Logged in the system as "MEM002", having an overdue book that is not yet returned`

**Steps:**
1. Log in the system with as `MEM002`
2. Access the borrow/return tab
3. Click `Return book` on ticket `BR001`
4. Observe the pop up message

**Expected results:**
`Upon clicking the "Return book" button there should be 2 messages popping up. 1 for returning the book successfully and 1 for having returning the book later than the due date`

**Actual results:**
`Only 1 message regarding returning the book successfully, missing the 2nd pop up message`

**Impacts:**
`Violates the business requirements`

**Proof:**
![TC-22](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-22.png?raw=true)

**Fix suggestions:**
`Implement a check on whether the return date is later than the due date and have the warning accordingly`

---

## BUG-05 - System failed to add member with valid information

| Attribute | Detail |
|-----------|---------|
| **Bug-ID** | BUG-05 |
| **Related TC** | `TC-29` |
| **Related REQ** | `REQ-07` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |

**Prerequisites:**
`Logged in as the Librarian, member information are valid`

**Steps:**
1. Log in the system with the librarian account
2. Click on the `Add member` at the top right corner
3. Fill the boxes with valid information

**Expected results:**
`The system adds the member sucessfully`

**Actual results:**
`The system displays an error regarding incorrect email syntax`

**Impacts:**
`The add member button functionality is no longer met`

**Proof:**
![TC-29](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-29.png?raw=true)

**Fix suggestions**
`Adjust the correct syntax for email`

---

## BUG-06 - System added member successfully with incorect email syntax

| Attribute | Details |
|-----------|---------|
| **Bug-ID** | BUG-06 |
| **Related TC** | `TC-32` |
| **Related REQ** | `REQ-07` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |

**Prerequisites:**
`Logged in as the Librarian, member's email address is invalid, name and phone number is valid`

**Steps:**
1. Log in the system with the librarian account
2. Click on the `Add member` at the top right corner
3. Fill the boxes with `tester@emailcom` as email information and valid name and phone number

**Expected results:**
`The system reject the request and display an error regarding incorrect email syntax`

**Actual results:**
`The system added the member successfully`

**Impacts:**
`The add member button functionality is no longer met`

**Proof:**
![TC-32](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-32.png?raw=true)

**Fix suggestions**
`Adjust the correct syntax for email`

---

## BUG-07 - The system displays incorrect message regarding email that has already existed in the database

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Bug-ID** | BUG-07 |
| **Related TC** | `TC-33` |
| **Related REQ** | `REQ-07` |
| **Severity** | `Low` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged in as the Librarian, member's email address match with one that exists in side the database, name and phone number is valid`

**Steps:**
1. Log in the system with the librarian account
2. Click on the `Add member` at the top right corner
3. Fill the boxes with `ba.nguyen@email.com` as email and valid name and phone numbe

**Expected results:**
`The system reject the request and display "Email already exists" error`

**Actual results:**
`The system reject the request and display "Email invalid" error`

**Impacts:**
`May cause the librarian to mistakenly think that the email is invalid instead of thinking it is already in the system database`

**Proof:**
![TC-33](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-33.png?raw=true)

**Fix suggestions**
`Give repeated email its own error`

---

## BUG-08 - Member can lookup other member's borrowing records

| Attribute | Details|
|-----------|---------|
| **Bug-ID** | BUG-08 |
| **Related TC** | `TC-37` |
| **Related REQ** | `REQ-08` |
| **Severity** | `High` |
| **Bug reporter** | `Nguyễn Ngọc Minh Hiếu` |
| **Date reported** | `30/05/2026` |
| **Status** | `Open` |

**Prerequisites:**
`Logged in as an "MEM002"`

**Steps:**
1. Log in the system as `MEM002`
2. Enter the `Borrow/Return` page
3. Click `Search borrow records` on top-right corner
4. Enter another member's ID in to the search bar
5. Click `Enter`


**Expected results:**
`The system denies the user's request to lookup other member's record or returns a blank borrowing records with an error message`

**Actual results:**
`The system allows the user to look up other member's borrowing records`

**Impacts:**
`Privacy and access control violation`

**Proof:**
![TC-37](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-37.png?raw=true)

**Fix suggestions**
`Adjust member permission or make sure that the member's ID matches the searched member's ID`

---
