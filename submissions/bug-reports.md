# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 17` |
| **Ngày báo cáo** | `16/05/2026` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-12,13` |
| **REQ liên quan** | `REQ-03` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
`Hệ thống không hiển thị sách thuộc thể loại "Kinh tế" khi sử dụng "kinh tế" thay vì "Kinh tế"`


**Environment:**
- Trình duyệt: Firefox `139`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

**Prerequisites:**
`Đã đăng nhập vào hệ thống, dữ liệu đã reset, ở trong giao diện "Sách"`

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
``

**Fix suggestions:**
`Developer can normalize the user input in to the same format` 

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `TC-19` |
| **REQ liên quan** | `REQ-04,05` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Title:**
`Allow the user to borrow the 4th book`


**Environment**
- Trình duyệt: Firefox `139`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

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
`<!-- -->`

**Fix suggestions**
`Adjust the borrow count logic`

---

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-26` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Title:**
`System failed to add member with valid information`


**Môi trường:**
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
`<!-- -->`

**Fix suggestions**
`Adjust the correct syntax for email`

---

## BUG-04

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | `TC-29` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Ngọc Minh Hiếu` |
| **Ngày phát hiện** | `30/05/2026` |
| **Trạng thái** | `Open` |

**Title:**
`System failed to add member with valid information`


**Môi trường:**
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
`<!-- -->`

**Fix suggestions**
`Adjust the correct syntax for email`

---