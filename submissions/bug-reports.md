# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 17` |
| **Ngày báo cáo** | `16/05/2026` |

**Environment:**
- Trình duyệt: Firefox `139`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

---

## BUG-01 - The category feature is case sensitive and does not return results when lower-case texts are entered

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-13` |
| **REQ liên quan** | `REQ-03` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged into the system as an active member, in the "Books" page`

**Steps:**
1. Click on the search bar: Filter by category(e.g. Technology, Economics...)
2. Enter all lower-case string `kinh tế` 
3. Press `Enter`


**Expected results:**
`Display books in the category "Kinh tế" (lower-case should not matter)`

**Actual results:**
`Empty book list, only accept when the user uses the exact form of "Kinh tế"`

**Impact**
`Affects user experience. Users who type in lower-case may not be able to find books and lead to thinking that the system does not have the book or the filter system is broken even though the book exists in the system`

**Proof:**
![TC-13](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-013.png?raw=true)

**Fix suggestions:**
`Developer can normalize the user input in to the same format` 

---

## BUG-02 - The category feature is case sensitive and does not return results when upper-case texts are entered

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-14` |
| **REQ liên quan** | `REQ-03` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged into the system as an active member, in the "Books" page`

**Steps:**
1. Click on the search bar: Filter by category(e.g. Technology, Economics...)
2. Enter all lower-case string `KINH TẾ` 
3. Press `Enter`


**Expected results:**
`Display books in the category "Kinh tế" (upper-case should not matter)`

**Actual results:**
`Empty book list, only accept when the user uses the exact form of "Kinh tế"`

**Impact**
`Affects user experience. Users who type in lower-case may not be able to find books and lead to thinking that the system does not have the book or the filter system is broken even though the book exists in the system`

**Proof:**
![TC-13](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-14.png?raw=true)

**Fix suggestions:**
`Developer can normalize the user input in to the same format` 

---

## BUG-03 - Allow the user to borrow the 4th book

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-19` |
| **REQ liên quan** | `REQ-04,05` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |
 
**Prerequisites:**
`Active member, having already borrowed 3 books, books have "Available" status`

**Steps:**
1. `Log in the system with an active account`
2. `Borrow 4 books with the status "Available"`
3. `Check the system response`

**Expected results:**
`Upon reaching the 4th book, the system must display a warning that there is a 3 books limit and reject additional borrowing`

**Actual results:**
`The system allow the user to borrow the 4th book and only show error when the user attempts to borrow the 5th book`

**Impacts:**
`Violates the business requirements`

**Proof:**
![TC-14](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-14.png?raw=true)

**Fix suggestions**
`Adjust the borrow count logic`

---

## BUG-04 - System failed to add member with valid information

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | `TC-26` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Environment**
- Trình duyệt: Firefox `139`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

**Prerequisites:**
`Logged in as Librarian, member information are valid`

**Steps:**
1. `Log in the system with the librarian account`
2. `Click on the "Add member" at the top right corner`
3. `Fill the boxes with valid information`

**Expected results:**
`The system adds the member sucessfully`

**Actual results:**
`The system displays an error regarding incorrect email syntax`

**Impacts:**
`The add member button functionality is no longer met`

**Proof:**
![TC-26](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-26.png?raw=true)

**Fix suggestions**
`Adjust the correct syntax for email`

---

## BUG-05 - System added member successfully with incorect email syntax

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-05 |
| **TC liên quan** | `TC-29` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged in as Librarian, member's email address is invalid, name and phone number is valid`

**Steps:**
1. `Log in the system with the librarian account`
2. `Click on the "Add member" at the top right corner`
3. `Fill the boxes with invalid email information and valid name and phone number`

**Expected results:**
`The system reject the request and display an error regarding incorrect email syntax`

**Actual results:**
`The system added the member successfully`

**Impacts:**
`The add member button functionality is no longer met`

**Proof:**
![TC-29](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-29.png?raw=true)

**Fix suggestions**
`Adjust the correct syntax for email`

---

## BUG-06 - The system displays incorrect message regarding email that has already existed in the database

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-06 |
| **TC liên quan** | `TC-30` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `Low` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged in as Librarian, member's email address match with one that exists in side the database, name and phone number is valid`

**Steps:**
1. `Log in the system with the librarian account`
2. `Click on the "Add member" at the top right corner`
3. `Fill the boxes with repeated email information and valid name and phone number`

**Expected results:**
`The system reject the request and display "Email already exists" error`

**Actual results:**
`The system reject the request and display "Email invalid" error`

**Impacts:**
`May cause the librarian to mistakenly think that the email is invalid instead of thinking it is already in the system database`

**Proof:**
![TC-30](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-30.png?raw=true)

**Fix suggestions**
`Give repeated email its own error`

---

## BUG-07 - Member can lookup other member's borrowing records

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-07 |
| **TC liên quan** | `TC-33` |
| **REQ liên quan** | `REQ-08` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Prerequisites:**
`Logged in as an "MEM002"`

**Steps:**
1. `Log in the system as "MEM002"`
2. `Enter the "Borrow/Return" page`
3. `Click "Search borrow records" on top-right corner`
4. `Enter another member's ID in to the search bar`
5. `Click "Enter"`


**Expected results:**
`The system denies the user's request to lookup other member's record or returns a blank borrowing records with an error message`

**Actual results:**
`The system allows the user to look up other member's borrowing records`

**Impacts:**
`Privacy and access control violation`

**Proof:**
![TC-33](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_17/blob/main/Screenshots/TC-33.png?raw=true)

**Fix suggestions**
`Adjust member permission or make sure that the member's ID matches the searched member's ID`

---
