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
| Vai trò người dùng | Thủ thư | `librarian@library.` | Thấy nút "Thêm thành viên", có thể ấn |
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
| Thông tin phiếu mượn | Hiển thị đầy đủ thông tin | `BR001` | Hiển thị mã phiếu, sách mượn, ngày mượn, ngày hết hạn, trạng thái |


> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Kiểm tra thành viên có thể đăng nhập với email và mật khẩu hợp lệ | Thành viên đã có tài khoản trong hệ thống và đang ở trang đăng nhập | 1.Điền email hợp lệ vào ô `Email`. 2.Sử dụng mật khẩu đúng vào ô `Mật khẩu`. 3.Ấn nút Đăng nhập  | Email đăng nhập: `librarian@library.com` , mật khẩu: `admin123` | Đăng nhập thành công, hiển thị trang  | REQ-01  | EP, BVA |
| TC-02 | Kiểm tra thành viên đăng nhập thất bại do sai mật khẩu | Hệ thống ở trang đăng nhập | 1. Điền email hợp lệ vào ô `Email`. 2.Nhập sai mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `librarian@library.com` , Pass: `wrongpass` | Thông báo lỗi sai thông tin đăng nhập. | REQ-01 | EP |
| TC-03 | Kiểm tra thành viên đăng nhập thất bại do email không tồn tại | Hệ thống ở trang đăng nhập | 1.Điền email không có trong database. 2.Nhập đúng mật khẩu vào ô `Mật khẩu`. 3.Nhấn Đăng nhập | Email: `noone@email.com` , Pass: `admin123` | Thông báo lỗi không tìm thấy tài khoản. | REQ-01 | EP |
| TC-04 | Kiểm tra thành viên đăng nhập thất bại khi để trống Email | Hệ thống ở trang đăng nhập | 1.Bỏ trống ô email. 2.Nhập mật khẩu. 3.Nhấn Đăng nhập | Email: `""` , Pass: `admin123` | Hiển thị cảnh báo "Vui lòng nhập email". | REQ-01 | EP, BVA |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
