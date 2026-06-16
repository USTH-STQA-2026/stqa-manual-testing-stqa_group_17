# Test Execution — Kết quả thực thi kiểm thử



| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 17` |
| **Ngày thực thi** | `16/05/2026` |
| **Trình duyệt** | Firefox `139.0` |
| **Hệ điều hành** | `Linux` |

---

## Kết quả chi tiết

### REQ-01 - Login
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Đăng nhập thành công | Đăng nhập thành công | Pass| | |
| TC-02 | Login | Báo lỗi mật khẩu không đúng | Báo lỗi mật khẩu không đúng | Pass | | |
| TC-03 | Login | Báo lỗi không tìm thấy tài khoản |Báo lỗi không tìm thấy tài khoản | Pass | | |
| TC-04 | Login | Hiện cảnh báo "Vui lòng nhập email" | Hiện cảnh báo "Vui lòng nhập email" | Pass | | |
| TC-05 | Login | Hiện cảnh báo "Vui lòng nhập mật khẩu" | Hiện cảnh báo "Vui lòng nhập email và mật khẩu" | Pass | | |
| TC-06 | Login | Hiện cảnh báo "Vui lòng nhập email và mật khẩu" | Hiện cảnh báo "Vui lòng nhập email và mật khẩu" | Pass | | |

### REQ-02 - Book list
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-07 | Book list | Danh sách hiển thị thành công và đầy đủ thông tin| Danh sách hiển thị thành công và đầy đủ thông tin | Pass | | |
| TC-08 | Book list | Trạng thái sách cập nhật trong real-time | Trạng thái sách cập nhật trong real-time | Pass | | |

### REQ-03 - Search Function
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-09 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |
| TC-10 | Search Function | Hiển thị sách có tác giả tên "Nguyễn" | Hiển thị sách có tác giả tên "Nguyễn" | Pass | | |
| TC-11 | Search Function | Hiển thị danh sách rỗng | Hiển thị danh sách rỗng  | Pass | | |
| TC-12 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị sách thuộc thể loại kinh tế | Pass | | |
| TC-13 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị danh sách rỗng | Fail | | BUG-01|
| TC-14 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị danh sách rỗng | Fail | | BUG-02 |
| TC-15 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |

### REQ-04 - Borrow
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-16 | Book Borrow | Mượn thành công | Mượn thành công | Pass | | |
| TC-17 | Book Borrow | Không cho phép mượn | Không cho phép mượn| Pass | | |
| TC-18 | Book Borrow | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Pass | | |
| TC-19 | Book Borrow | Không cho phép mượn, thông báo tài khoản hết hạn | Không cho phép mượn, thông báo tài khoản hết hạn | Pass | | |
| TC-20 | Book Borrow | Từ chối mượn, thông báo số sách mượn vượt giới hạn | Có thể mượn cuốn sách thứ 4 | Fail | | BUG-03 |

### REQ-05 - Borrow

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-21 | Book Return | Trả sách thành công, không có thông báo trả sách muộn | Trả sách thành công, không có thông báo trả sách muộn | Pass | | |
| TC-22 | Book Return | Trả sách thành công, hệ thống hiển thị thông báo trả sách muộn | Trả sách thành công, không có thông báo trả sách muộn | Fail | | | BUG-04 |

### REQ-06 - Overdue Handling
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-23 | Overdue Handling | Thấy nút "kiểm tra sách quá hạn" | Thấy nút "kiểm tra sách quá hạn"  | Pass | | |
| TC-24 | Overdue Handling | Không thấy nút "kiểm tra sách quá hạn" | Không thấy nút "kiểm tra sách quá hạn" | Pass | | |
| TC-25 | Overdue Handling | Phiếu BR001 cập nhật trạng thái "quá hạn" | Phiếu BR001 cập nhật trạng thái "quá hạn" | Pass | | |
| TC-26 | Overdue Handling | Phiếu mới giữ trạng thái "Đang mượn" | Phiếu mới giữ trạng thái "Đang mượn" | Pass | | |
| TC-27| Overdue Handling | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Pass | | |

### REQ-07 - Member Management
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-28 | Member Management | Nhìn thấy nút "thêm thành viên" | Nhìn thấy nút "thêm thành viên" | Pass | | |
| TC-29 | Member Management | Thêm thành viên thành công | Hệ thống báo email không hợp lệ | Fail | | BUG-05|
| TC-30 | Member Management | Báo lỗi họ tên không được để trống | Báo lỗi họ tên không được để trống | Pass | | |
| TC-31 | Member Management | Báo lỗi email không hợp lệ | Báo lỗi email không hợp lệ | Pass | | |
| TC-32 | Member Management | Báo lỗi email không hợp lệ | Thêm thành viên thành công | Fail | | BUG-06 |
| TC-33 | Member Management | Báo lỗi email đã tồn tại trong hệ thống | Báo lỗi email không hợp lệ | Fail | | BUG-07 |
| TC-34 | Ticket Lookup | Báo lỗi số điện thoại không hợp lệ | Báo lỗi email không hợp lệ (Bị chặn do BUG-05) | Blocked | | |

### REQ-08 Ticket Lookup
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-35 | Ticket Lookup | Xem được phiếu mượn của tất cả thành  | Xem được phiếu mượn của tất cả thành viên | Pass | | |
| TC-36 | Ticket Lookup | Chỉ hiển thị phiếu mượn của chính mình | Chỉ hiển thị phiếu mượn của chính mình | Pass | | |
| TC-37 | Ticket Lookup | Chặn hiển thị dữ liệu | Hiển thị dữ liệu của thành viên `MEM003` | Fail | | BUG-08 |
| TC-38 | Ticket Lookup | Hiển thị thông tin phiếu | Hiển thị thông tin phiếu | Pass | | |


---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `38` |
| Pass | `29` |
| Fail | `8` |
| Blocked | `1` |
| Not Run | `0` |
| **Tỷ lệ Pass** | `76%` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Login | 6 | 6 | 0 | 100% |
| Search Function | 7 | 5 | 2 | 71%
| Book List | 2 | 2 | 0 | 100% |
| Book Borrow| 5 | 4 | 1 | 80% | 
| Book Return| 2 | 1 | 1 | 50% |
| Overdue Handling | 5 | 5 | 0 | 100%
| Member Management | 7 | 3 | 3| 42%
| Ticket Lookup | 4 | 3 | 1 | 75%

