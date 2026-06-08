# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 17` |
| **Ngày tạo** | `17/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng | Thủ thư | `librarian@library.com` | Thấy danh sách sách
| | Thành viên | `ba.nguyen@gmail.com` | Thấy danh sách sách
| Trạng thái sách | Sách đang có sẵn | `"Có sẵn"` | Hiển thị nhãn "Có sẵn"
| | Sách đang được mượn | `"Đang mượn"` | Hiển thị nhãn "Đang mượn"
| Thông tin sách | Sách đầy đủ thông tin | Tên sách, tác giả, năm xuất bản, trạng thái | Hiện đầy đủ thông tin trên giao diện
| Cập nhật trạng thái real-time | Sách đổi trạng thái mượn/trả | `"Có sẵn"`, `"Đang mượn"` | Trạng thái sách được cập nhật ngay lập 
 
### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — Xử lý sách quá hạn (REQ-6)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng ? | Thủ thư | `librarian@library.com` | Thấy nút "Kiểm tra sách quá hạn", có thể ấn |
| | Thành viên | `ba.nguyen@gmail.com` | Không thấy nút "Kiểm tra sách quá hạn" |
| Trạng thái phiếu mượn | Đang mượn, dueDate <= hôm nay | BR001 (hạn 15/09/2024)| Đánh dấu quá hạn sau khi nhấn nút |
| | Đang mượn, dueDate > hôm nay | Phiếu mới tạo hôm nay  | Giữ nguyên trạng thái đang mượn |
| | Đã trả, dueDate <= hôm nay | BR005, BR004 | Giữ nguyên trạng thái đã  |
| Phạm vi hiển thị cho thành viên | Phiếu của chính mình | BR001 (MEM002) | Thấy phiếu quá hạn của mình |
| | Phiếu của người khác  | BR003 (MEM006) | Không thấy phiếu của người khác | 

### IDM — Quản lý thành viên (REQ-7)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng | Thủ thư | `librarian@library.com` | Thấy nút "Thêm thành viên", có thể ấn |
| | Thành viên | `ba.nguyen@gmail.com` | Không thấy nút "Thêm thành viên" | 
| Họ và tên | Có nhập chữ | Name Test | Thêm thành công |
| | Để trống | `để trống` | Báo lỗi `Họ tên không được để trống` |
| Email | Nhập đúng cú pháp | `Emailtest@email.com` | Thêm thành công |
| | Để trống | `để trống` | Báo lỗi `Email không hợp lệ` |
| | Thiếu ký hiệu `@` | `Emailtestemail.com` | Báo lỗi `Email không hợp lệ` |
| | Thiếu ký hiệu `.` ở domain| `Emailtest@emailcom` | Báo lỗi `Email không hợp lệ` | 
| | Trùng email đã tồn tại | `ba.nguyen@gmail.com` | Báo lỗi `Email không hợp lệ` |
### IDM — Tra cứu phiếu mượn (REQ-8)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò thành viên | Thủ thư | `librarian@library.com` | Xem được phiếu mượn của tất cả thành viên  |
| | Thành viên | `ba.nguyen@gmail.com` | Chỉ thấy phiếu mượn của chính mình |
| Tra cứu phiếu mượn | Mã thành viên của chính mình | `MEM002` | Hiển thị các phiếu mượn của chính mình | 
| | Mã thành viên của thành viên khác | `MEM003` | Không hiển thị phiếu mượn của thành viên  | 
| | Mã thành viên không hợp lệ| `MEM99` | Không hiển thị phiếu mượn |
| Thông tin phiếu mượn | Hiển thị đầy đủ thông tin | `MEM002` | Hiển thị mã phiếu, sách mượn, ngày mượn, ngày hết hạn, trạng thái |


> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

---

### Bảng Test Cases — REQ-01: Đăng nhập
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Kiểm tra thành viên có thể đăng nhập với email và mật khẩu hợp lệ | Thành viên đã có tài khoản trong hệ thống và đang ở trang đăng nhập | 1.Điền email hợp lệ vào ô `Email`. 2.Sử dụng mật khẩu đúng vào ô `Mật khẩu`. 3.Ấn Đăng nhập  | Email: `librarian@library.com` , Pass: `admin123` | Đăng nhập thành công, hiển thị trang  | REQ-01  | EP, BVA |
| TC-02 | Kiểm tra thành viên đăng nhập thất bại do sai mật khẩu | Hệ thống ở trang đăng nhập | 1.Điền email hợp lệ vào ô `Email`. 2.Nhập sai mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `librarian@library.com` , Pass: `wrongpass` | Thông báo lỗi sai thông tin đăng nhập. | REQ-01 | EP |
| TC-03 | Kiểm tra thành viên đăng nhập thất bại do email không tồn tại | Hệ thống ở trang đăng nhập | 1.Điền email không có trong database. 2. Nhập đúng mật khẩu vào ô `Mật khẩu`. 3. Nhấn Đăng nhập | Email: `noone@email.com` , Pass: `admin123` | Thông báo lỗi không tìm thấy tài khoản. | REQ-01 | EP |
| TC-04 | Kiểm tra thành viên đăng nhập thất bại khi để trống Email | Hệ thống ở trang đăng nhập | 1.Bỏ trống ô email. 2.Nhập mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `""` , Pass: `admin123` | Hiển thị cảnh báo "Vui lòng nhập email". | REQ-01 | EP, BVA |

---

### Bảng Test Cases — REQ-02: Xem danh sách sách 
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-05 | Kiểm tra danh sách sách hiển thị cho thành viên và thủ thư | Người dùng có tài khoản hợp lệ | 1. Đăng nhập vào hệ thống 2.Vào phần "Sách" 3.Nhìn vào danh sách sách | Tài khoản bất kỳ hợp lệ | Danh sách sách hiện cho cả thủ thư và thành viên | REQ-02 | EP
| TC-06 | Kiểm tra sách hiển thị đầy đủ thông tin | Người dùng đã đăng nhập và đang ở dao diện "Sách" | 1. Vào phần "Sách" 2.Xem phần thông tin sách được hiển thị | Bất kỳ cuốn sách nào | Hiển thị tên sách, tác giả, năm xuất bản và trạng thái| REQ-02 | EP
| TC-07 | Kiểm tra sách hiển thị trạng thái đúng | Người dùng đã đăng nhập và đang nhìn vào danh sách sách | 1. Vào phần "Sách" 2. Kiểm tra trạng thái của sách| Sách có trạng thái khác nhau | Hệ thống hiển thị trạng thái đúng cho từng sách bao gồm "Có sẵn", "Đang mượn", "Thất lạc" | REQ-02 | EP

---

### Bảng Test Cases — REQ-03: Tìm kiếm sách
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-08 | Tìm sách thành công bằng một phần tên sách | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập từ khóa tên sách. 3.Nhấn Tìm kiếm | Từ khóa: `"Flutter"` | Hiển thị danh sách các cuốn sách có chứa từ "Flutter". | REQ-03 | EP |
| TC-09 | Tìm sách thành công bằng tên tác giả | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập tên tác giả. 3.Nhấn Tìm kiếm | Từ khóa: `"Nguyễn"` | Hiển thị danh sách sách của tác giả có tên "Nguyễn". | REQ-03 | EP |
| TC-10 | Tìm sách không tồn tại | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập chuỗi ngẫu nhiên. 3.Nhấn Tìm kiếm | Từ khóa: `"XYZ123"` | Hiển thị danh sách rỗng. | REQ-03 | EP |
| TC-11 | Tìm tên sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"FLUTTER"` | Kết quả hiển thị giống như khi tìm `"Flutter"`. | REQ-03 | EP |
| TC-12 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"Kinh tế"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
| TC-13 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"kinh tế"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
| TC-14 | Tìm thể loại sách không phân biệt chữ hoa hay thường | Đã đăng nhập hệ thống | 1.Vào ô tìm kiếm thể loại. 2.Nhập từ khóa chữ hoa toàn bộ. 3.Nhấn Tìm kiếm | Từ khóa: `"KINH TẾ"` | Hiển thị các sách thuộc thể loại kinh tế | REQ-03 | EP
---

### Bảng Test Cases — REQ-04, REQ-05: Mượn sách
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-15 | Mượn sách thành công (Điều kiện lý tưởng) | Đăng nhập với tài khoản Thành viên Hoạt động (`MEM002`) | 1.Chọn sách có trạng thái "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Sách đang mượn: 0 | Hệ thống cho phép mượn, tạo phiếu mượn thành công. | REQ-04, 05 | EP, BVA |  
| TC-16 | Chặn mượn sách đang được người khác mượn | Đăng nhập tài khoản Thành viên Hoạt động | 1.Tìm sách đang có trạng thái "Đang mượn". 2.Nhấn Mượn sách | Sách: `BOOK003` | Nút mượn bị mờ hoặc hệ thống báo lỗi không cho phép. | REQ-04, 05 | EP |
| TC-17 | Chặn mượn sách khi tài khoản bị Tạm ngưng | Đăng nhập tài khoản Tạm ngưng (`cu.le@email.com`) | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Tài khoản: Tạm ngưng | Từ chối mượn, thông báo lỗi tài khoản đang bị tạm ngưng. | REQ-04, 05 | EP |
| TC-18 | Chặn mượn sách khi tài khoản đã Hết hạn | Đăng nhập tài khoản Hết hạn (`binh.pham@email.com`) | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Tài khoản: Hết hạn | Từ chối mượn, thông báo lỗi tài khoản đã hết hạn. | REQ-04, 05 | EP |
| TC-19 | Chặn mượn sách khi đã đạt giới hạn tối đa (3 cuốn) | Đăng nhập tài khoản đã mượn đủ 3 cuốn | 1.Chọn sách "Có sẵn". 2.Nhấn Mượn sách | Sách: `BOOK001` Sách đang mượn: 3 | Từ chối, thông báo số lượng sách mượn vượt quá giới hạn. | REQ-04, 05 | BVA |

---

### Bảng Test Cases — REQ-06: Xử lý sách quá hạn
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-20 | Phân quyền hiển thị nút Xử lý quá hạn (Thủ thư) | Đăng nhập tài khoản Thủ thư (`librarian@library.com`) | 1.Truy cập trang Quản lý mượn trả | - | Nhìn thấy nút "Kiểm tra sách quá hạn". | REQ-06 | EP |
| TC-21 | Phân quyền hiển thị nút Xử lý quá hạn (Thành viên) | Đăng nhập tài khoản Thành viên (`ba.nguyen@email.com`) | 1.Truy cập trang Quản lý mượn trả / Phiếu mượn | - | Không nhìn thấy nút "Kiểm tra sách quá hạn". | REQ-06 | EP |
| TC-22 | Đánh dấu phiếu mượn quá hạn | Thủ thư nhấn nút Kiểm tra sách quá hạn | 1.Hệ thống quét các phiếu mượn đang có | Phiếu: `BR001` Hạn trả: 15/09/2024 (<= Hôm nay) | Phiếu BR001 được cập nhật trạng thái thành "Quá hạn". | REQ-06 | EP, BVA |
| TC-23 | Không thay đổi trạng thái phiếu chưa đến hạn | Thủ thư nhấn nút Kiểm tra sách quá hạn | 1.Hệ thống quét các phiếu mượn đang có | Phiếu: Mới tạo hôm nay (Hạn trả > Hôm nay) | Phiếu giữ nguyên trạng thái "Đang mượn". | REQ-06 | EP, BVA |
| TC-24 | Hiển thị phiếu quá hạn cho chính thành viên đó | Đăng nhập Thành viên `MEM002` (có phiếu quá hạn) | 1.Truy cập danh sách phiếu mượn của tôi | - | Nhìn thấy phiếu mượn của mình bị đánh dấu đỏ hay quá hạn. | REQ-06 | EP |
---

### Bảng Test Cases — REQ-07: Quản lý thành viên
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-25 | Phân quyền hiển thị nút Thêm thành viên | Đăng nhập tài khoản Thủ thư | 1.Truy cập trang chủ| - | Nhìn thấy nút/chức năng "Thêm thành viên". | REQ-07 | EP |
| TC-26 | Thêm thành viên | Đăng nhập tài khoản thủ thư | 1. Truy cập trang chủ 2. Nhấn nút thêm thành viên 3.Điền thông tin thành viên hợp lệ 4.Nhấn nút thêm thành viên | Họ tên: `Tester` Email:'Tester@email.com' SĐT: `0123456789` | Thêm thành viên thành công | REQ-07 | EP 
| TC-27 | Thêm thành viên thất bại do bỏ trống Họ tên | Thủ thư ở trang Thêm TV | 1.Bỏ trống Họ tên. 2.Nhập Email hợp lệ. 3.Nhập số điện thoại hợp lệ 4.Nhấn Lưu | Họ tên: `""` Email: `test@email.com` SĐT: `"0123456789"` | Báo lỗi "Họ tên không được để trống". | REQ-07 | EP, BVA |
| TC-28 | Thêm thành viên thất bại do sai định dạng Email (thiếu @) | Thủ thư ở trang Thêm TV | 1.Nhập Họ tên. 2.Nhập Email thiếu "@". 3.Nhập số điện thoại hợp lệ. 4.Nhấn Lưu | Họ tên:`Tester` Email: `Emailtestemail.com` SĐT: `"0123456789"` | Báo lỗi định dạng email không hợp lệ. | REQ-07 | EP |
| TC-29 | Thêm thành viên thất bại do sai định dạng Email (thiếu ".")  | Thủ thư ở trang thêm thành viên | 1.Nhập Họ tên. 2.Nhập Email thiếu ".". 3.Nhập số điện thoại hợp lệ. 4.Nhấn Lưu | Họ tên:`Tester` Email: `Emailtest@emailcom` SĐT: `"0123456789"` | Báo lỗi định dạng email không hợp lệ | REQ-07 | EP |
| TC-30 | Thêm thành viên thất bại do trùng Email đã có | Thủ thư ở trang Thêm TV | 1.Nhập Họ tên. 2.Nhập Email của TV đang có. 3.Lưu | Họ tên: `Tester` Email: `ba.nguyen@email.com` SĐT:0123456789 | Báo lỗi email đã tồn tại trong hệ thống. | REQ-07 | EP |

---

### Bảng Test Cases — REQ-08: Tra cứu phiếu mượn
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-31 | Tra cứu toàn bộ phiếu mượn (Dành cho Thủ thư) | Đăng nhập tài khoản Thủ thư | 1.Truy cập trang Tra cứu phiếu mượn | - | Xem được danh sách phiếu mượn của tất cả các thành viên. | REQ-08 | EP |
| TC-32 | Thành viên chỉ tra cứu được phiếu của mình | Đăng nhập tài khoản Thành viên `MEM002` | 1.Truy cập trang Tra cứu phiếu mượn | - | Chỉ hiển thị các phiếu mượn thuộc về `MEM002`. | REQ-08 | EP |
| TC-33 | Thành viên cố tình xem phiếu của người khác qua URL/Tìm kiếm | Đăng nhập Thành viên `MEM002` | 1.Cố gắng nhập mã phiếu/mã TV của `MEM003` để tìm kiếm | Mã cần tìm: Phiếu của `MEM003` | Hệ thống báo không tìm thấy hoặc chặn hiển thị dữ liệu. | REQ-08 | EP |
| TC-34 | Kiểm tra hiển thị đầy đủ chi tiết thông tin của phiếu mượn | Đã đăng nhập hệ thống và ở trang Tra cứu phiếu mượn | 1.Nhập mã thành viên hợp lệ vào ô tìm kiếm. 2.Nhấn Tìm kiếm | Mã thành viên : `MEM002` | Hệ thống hiển thị chính xác và đầy đủ các thông tin: mã phiếu, sách mượn, ngày mượn, ngày hết hạn, và trạng thái phiếu. | REQ-08 | EP |
---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| Tổng | 34 | 8 | EP, BVA |
