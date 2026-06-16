# Test Cases — Bảng trường hợp kiểm thử


| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 17` |
| **Ngày tạo** | `17/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## 1. Input Domain Modeling (IDM)

### IDM — Đăng nhập (REQ-01)

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


### IDM — Xem danh sách sách (REQ-02)

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
### IDM — Tìm kiếm sách (REQ-03)

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

### Bảng Test Cases — REQ-01: Đăng nhập
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Kiểm tra thành viên có thể đăng nhập với email và mật khẩu hợp lệ | Thành viên đã có tài khoản trong hệ thống và đang ở trang đăng nhập | 1.Điền email hợp lệ vào ô `Email`. 2.Sử dụng mật khẩu đúng vào ô `Mật khẩu`. 3.Ấn Đăng nhập  | Email: `librarian@library.com` , Pass: `admin123` | Đăng nhập thành công, hiển thị trang  | REQ-01  | EP, BVA |
| TC-02 | Kiểm tra thành viên đăng nhập thất bại do sai mật khẩu | Hệ thống ở trang đăng nhập | 1.Điền email hợp lệ vào ô `Email`. 2.Nhập sai mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `librarian@library.com` , Pass: `wrongpass` | Thông báo lỗi sai thông tin đăng nhập. | REQ-01 | EP |
| TC-03 | Kiểm tra thành viên đăng nhập thất bại do email không tồn tại | Hệ thống ở trang đăng nhập | 1.Điền email không có trong database. 2. Nhập đúng mật khẩu vào ô `Mật khẩu`. 3. Nhấn Đăng nhập | Email: `noone@email.com` , Pass: `admin123` | Thông báo lỗi không tìm thấy tài khoản. | REQ-01 | EP |
| TC-04 | Kiểm tra thành viên đăng nhập thất bại khi để trống Email | Hệ thống ở trang đăng nhập | 1.Bỏ trống ô email. 2.Nhập mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `""` , Pass: `admin123` | Hiển thị cảnh báo "Vui lòng nhập email". | REQ-01 | EP, BVA |
| TC-05 | Kiểm tra thành viên đăng nhập thất bại khi để trống mật khẩu | Hệ thống ở trang đăng nhập | 1.Nhập email hợp lệ. 2.Bỏ trống ô mật khẩu. 3.Nhấn Đăng nhập | Email: `librarian@library.com` <br />Password:`" "`  | Hiển thị cảnh báo "Vui lòng nhập mật khẩu" | REQ-01 | EP,BVA
| TC-06 | Kiểm tra thành viên đăng nhập thất bại khi để trống cả ô email và mật khẩu | Hệ thống ở trang đăng nhập | 1.Bỏ trống email. 2.Bỏ trống ô mật khẩu. 3.Nhấn Đăng nhập  | Email: `" "` <br />Password: `" "` | Hiện cảnh báo "Vui lòng nhập email" và "Vui lòng nhập mật khẩu" |REQ-01 | EP,BVA 
---

### Bảng Test Cases — REQ-02: Xem danh sách sách 
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-07 | Kiểm tra danh sách sách hiển thị đầy đủ thông tin cho thành viên và thủ thư | Người dùng có tài khoản hợp lệ | 1. Đăng nhập vào hệ thống 2.Vào phần "Sách" 3.Nhìn vào danh sách sách | Tài khoản bất kỳ hợp lệ | Danh sách hiển thị tên sách, tên tác giả, năm xuất bản và trạng thái | REQ-02 | EP
| TC-08 | Kiểm tra sách cập nhật trạng thái đúng trong real-time | Người dùng có tài khoản hợp lệ | 1. Đăng nhập vào hệ thống bằng tài khoản người dùng 2.Vào phần "Sách" 3. Nhấn nút `Mượn sách này` trên sách có trạng thái `Có sẵn` 4. Nhấn "Mượn" để xác nhận mượn sách 5. Quan sát trạng thái sách thay đổi| Tài khoản người dùng hợp lệ | Trạng thái sách thay đổi từ "Có sẵn" sang "Đang mượn" ngay lập tức | REQ-02 | EP 
---

### Bảng Test Cases — REQ-03: Tìm kiếm sách
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-09 | Tìm sách thành công bằng một phần tên sách | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập từ khóa tên sách. 3.Nhấn Tìm kiếm | Từ khóa: `"Flutter"` | Hiển thị danh sách các cuốn sách có chứa từ "Flutter". | REQ-03 | EP |
| TC-10 | Tìm sách thành công bằng tên tác giả | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập tên tác giả. 3.Nhấn Tìm kiếm | Từ khóa: `"Nguyễn"` | Hiển thị danh sách sách của tác giả có tên "Nguyễn". | REQ-03 | EP |
| TC-11 | Tìm sách không tồn tại | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập chuỗi ngẫu nhiên. 3.Nhấn Tìm kiếm | Từ khóa: `"XYZ123"` | Hiển thị danh sách rỗng. | REQ-03 | EP |
| TC-12 | Tìm tên sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"FLUTTER"` | Kết quả hiển thị giống như khi tìm `"Flutter"`. | REQ-03 | EP |
| TC-13 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"Kinh tế"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
| TC-14 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"kinh tế"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
| TC-15 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"KINH TẾ"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
---

### Bảng Test Cases — REQ-04 - Borrow
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-16 | Mượn sách thành công (Điều kiện lý tưởng) | Đăng nhập với tài khoản Thành viên Hoạt động (`MEM002`) | 1.Chọn sách có trạng thái "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Sách đang mượn: 0 | Hệ thống cho phép mượn, tạo phiếu mượn thành công. | REQ-04, 05 | EP, BVA, Decision Table |  
| TC-17 | Chặn mượn sách đang được người khác mượn | Đăng nhập tài khoản Thành viên Hoạt động | 1.Tìm sách đang có trạng thái "Đang mượn". 2.Nhấn Mượn sách | Sách: `BOOK003` | Nút mượn bị mờ hoặc hệ thống báo lỗi không cho phép. | REQ-04, 05 | EP, Decision Table |
| TC-18 | Chặn mượn sách khi tài khoản bị Tạm ngưng | Đăng nhập tài khoản Tạm ngưng (`cu.le@email.com`) | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Tài khoản: Tạm ngưng | Từ chối mượn, thông báo lỗi tài khoản đang bị tạm ngưng. | REQ-04, 05 | EP, Decision Table |
| TC-19 | Chặn mượn sách khi tài khoản đã Hết hạn | Đăng nhập tài khoản Hết hạn (`binh.pham@email.com`) | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Tài khoản: Hết hạn | Từ chối mượn, thông báo lỗi tài khoản đã hết hạn. | REQ-04, 05 | EP, Decision Table |
| TC-20 | Chặn mượn sách khi đã đạt giới hạn tối đa (3 cuốn) | Đăng nhập tài khoản đã mượn đủ 3 cuốn | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Sách đang mượn: 3 | Từ chối, thông báo số lượng sách mượn vượt quá giới hạn. | REQ-04, 05 | EP,Decision Table |

---
### Bảng Test Cases — REQ-05: Return
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-21 | Trả sách đúng hạn | Đăng nhập với tài khoản Thành viên Hoạt động (`MEM002`) | 1.Access borrow/return tab. 2.Select an active record that is not overdue. 3.Click return book.  | - | -Book is returned successfully<br />-No overdue warning displayed | REQ-04,05 | EP,BVA,Decision Table
| TC-22 | Return overdue books | Đăng nhập với tài khoản Thành viên Hoạt động (`MEM002`) | 1.Access borrow/return tab. 2.Select an active record that is overdue. 3.Click return book. | - | -Book is returned successfully<br />-Overdue warning displayed | REQ-04,05 | EP,BVA,Decision Table 
---

### Bảng Test Cases — REQ-06: Xử lý sách quá hạn
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-23 | Phân quyền hiển thị nút Xử lý quá hạn (Thủ thư) | Đăng nhập tài khoản Thủ thư (`librarian@library.com`) | 1.Truy cập trang Quản lý mượn trả | - | Nhìn thấy nút "Kiểm tra sách quá hạn". | REQ-06 | EP |
| TC-24 | Phân quyền hiển thị nút Xử lý quá hạn (Thành viên) | Đăng nhập tài khoản Thành viên (`ba.nguyen@email.com`) | 1.Truy cập trang Quản lý mượn trả / Phiếu mượn | - | Không nhìn thấy nút "Kiểm tra sách quá hạn". | REQ-06 | EP |
| TC-25 | Đánh dấu phiếu mượn quá hạn | Thủ thư nhấn nút Kiểm tra sách quá hạn | 1.Hệ thống quét các phiếu mượn đang có | Phiếu: `BR001` Hạn trả: 15/09/2024 (<= Hôm nay) | Phiếu BR001 được cập nhật trạng thái thành "Quá hạn". | REQ-06 | EP, BVA |
| TC-26 | Không thay đổi trạng thái phiếu chưa đến hạn | Thủ thư nhấn nút Kiểm tra sách quá hạn | 1.Hệ thống quét các phiếu mượn đang có | Phiếu: Mới tạo hôm nay (Hạn trả > Hôm nay) | Phiếu giữ nguyên trạng thái "Đang mượn". | REQ-06 | EP, BVA |
| TC-27 | Hiển thị phiếu quá hạn cho chính thành viên đó | Đăng nhập Thành viên `MEM002` (có phiếu quá hạn) | 1.Truy cập danh sách phiếu mượn của tôi | - | Nhìn thấy phiếu mượn của mình bị đánh dấu đỏ hay quá hạn. | REQ-06 | EP |
---

### Bảng Test Cases — REQ-07: Quản lý thành viên
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-28 | Phân quyền hiển thị nút Thêm thành viên | Đăng nhập tài khoản Thủ thư | 1.Truy cập trang chủ| Email: `librarian@library.com` <br />Password: admin123 | Nhìn thấy nút/chức năng "Thêm thành viên". | REQ-07 | EP |
| TC-29 | Thêm thành viên | Đăng nhập tài khoản thủ thư | 1. Truy cập trang chủ 2. Nhấn nút thêm thành viên 3.Điền thông tin thành viên hợp lệ 4.Nhấn nút thêm thành viên | Họ tên: `Tester` Email:`Tester@email.com` SĐT: `0123456789` | Thêm thành viên thành công | REQ-07 | EP 
| TC-30 | Thêm thành viên thất bại do bỏ trống Họ tên | Thủ thư ở trang Thêm TV | 1.Bỏ trống Họ tên. 2.Nhập Email hợp lệ. 3.Nhập số điện thoại hợp lệ 4.Nhấn Lưu | Họ tên: `""` Email: `test@email.com` SĐT: `"0123456789"` | Báo lỗi "Họ tên không được để trống". | REQ-07 | EP, BVA |
| TC-31 | Thêm thành viên thất bại do sai định dạng Email (thiếu @) | Thủ thư ở trang Thêm TV | 1.Nhập Họ tên. 2.Nhập Email thiếu "@". 3.Nhập số điện thoại hợp lệ. 4.Nhấn Lưu | Họ tên:`Tester` Email: `Emailtestemail.com` SĐT: `"0123456789"` | Báo lỗi định dạng email không hợp lệ. | REQ-07 | EP |
| TC-32 | Thêm thành viên thất bại do sai định dạng Email (thiếu ".")  | Thủ thư ở trang thêm thành viên | 1.Nhập Họ tên. 2.Nhập Email thiếu ".". 3.Nhập số điện thoại hợp lệ. 4.Nhấn Lưu | Họ tên:`Tester` Email: `Emailtest@emailcom` SĐT: `"0123456789"` | Báo lỗi định dạng email không hợp lệ | REQ-07 | EP |
| TC-33 | Thêm thành viên thất bại do trùng Email đã có | Thủ thư ở trang Thêm TV | 1.Nhập Họ tên. 2.Nhập Email của TV đang có. 3.Lưu | Họ tên: `Tester` Email: `ba.nguyen@email.com` SĐT:0123456789 | Báo lỗi email đã tồn tại trong hệ thống. | REQ-07 | EP |
| TC-34 | Thêm thành viên thất bại do nhập số điện thoại không hợp lệ | Thủ thư ở trang thêm TV | 1.Nhập họ tên. 2.Nhập email hợp lệ. 3. Nhập số điện thoại không có 10 số 4.Nhấn lưu.| Họ tên: `Tester` Email" `Tester@email.com` SĐT:012345678 | Báo lỗi số điện thoại không hợp lệ | REQ-07 | EP  
---

### Bảng Test Cases — REQ-08: Tra cứu phiếu mượn
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-35 | Tra cứu toàn bộ phiếu mượn (Dành cho Thủ thư) | Đăng nhập tài khoản Thủ thư | 1.Truy cập trang Tra cứu phiếu mượn | - | Xem được danh sách phiếu mượn của tất cả các thành viên. | REQ-08 | EP |
| TC-36 | Thành viên chỉ tra cứu được phiếu của mình | Đăng nhập tài khoản Thành viên `MEM002` | 1.Truy cập trang Tra cứu phiếu mượn | - | Chỉ hiển thị các phiếu mượn thuộc về `MEM002`. | REQ-08 | EP |
| TC-37 | Thành viên cố tình xem phiếu của người khác qua URL/Tìm kiếm | Đăng nhập Thành viên `MEM002` | 1.Cố gắng nhập mã phiếu/mã TV của `MEM003` để tìm kiếm | Mã cần tìm: Phiếu của `MEM003` | Hệ thống báo không tìm thấy hoặc chặn hiển thị dữ liệu. | REQ-08 | EP |
| TC-38 | Kiểm tra hiển thị đầy đủ chi tiết thông tin của phiếu mượn | Đã đăng nhập hệ thống và ở trang Tra cứu phiếu mượn | 1.Nhập mã thành viên hợp lệ vào ô tìm kiếm. 2.Nhấn Tìm kiếm | Mã thành viên : `MEM002` | Hệ thống hiển thị chính xác và đầy đủ các thông tin: mã phiếu, sách mượn, ngày mượn, ngày hết hạn, và trạng thái phiếu. | REQ-08 | EP |
---

## 4. Summary

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Đăng nhập| 6 | REQ-01 | EP, BVA |
| Xem danh sách sách| 2 | REQ-02 | EP
| Tìm kiếm | 7 | REQ-03 | EP
| Mượn sách | 7 | REQ-04, 05 | EP, BVA, Decision Table
| Xử lý sách quá hạn| 5 | REQ-06 | EP, BVA 
| Quản lý thành viên | 7 | REQ-07 | EP, BVA
| Tra cứu phiếu mượn| 4 | REQ-08 | EP
| Tổng | 38 | 8 | EP, BVA, Decision Table |
