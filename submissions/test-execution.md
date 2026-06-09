# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

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

### REQ-02 - Book list
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-05 | Book list | Danh sách hiển thị thành công và đầy đủ thông tin| Danh sách hiển thị thành công và đầy đủ thông tin | Pass | | |
| TC-06 | Book list | Trạng thái sách cập nhật trong real-time | Trạng thái sách cập nhật trong real-time | Pass | | |

### REQ-03 - Search Function
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-07 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |
| TC-08 | Search Function | Hiển thị sách có tác giả tên "Nguyễn" | Hiển thị sách có tác giả tên "Nguyễn" | Pass | | |
| TC-09 | Search Function | Hiển thị danh sách rỗng | Hiển thị danh sách rỗng  | Pass | | |
| TC-10 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị sách thuộc thể loại kinh tế | Pass | | |
| TC-11 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị danh sách rỗng | Fail | | |
| TC-12 | Search Function | Hiển thị sách thuộc thể loại kinh tế | Hiển thị danh sách rỗng | Fail | | |
| TC-13 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |

### REQ-04, 05 - Book Borrow
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-14 | Book Borrow | Mượn thành công | Mượn thành công | Pass | | |
| TC-15 | Book Borrow | Không cho phép mượn | Không cho phép mượn| Pass | | |
| TC-16 | Book Borrow | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Pass | | |
| TC-17 | Book Borrow | Không cho phép mượn, thông báo tài khoản hết hạn | Không cho phép mượn, thông báo tài khoản hết hạn | Pass | | |
| TC-18 | Book Borrow | Từ chối mượn, thông báo số sách mượn vượt giới hạn | Có thể mượn cuốn sách thứ 4 | Fail | | |

### REQ-06 - Overdue Handling
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-19 | Overdue Handling | Thấy nút "kiểm tra sách quá hạn" | Thấy nút "kiểm tra sách quá hạn"  | Pass | | |
| TC-20 | Overdue Handling | Không thấy nút "kiểm tra sách quá hạn" | Không thấy nút "kiểm tra sách quá hạn" | Pass | | |
| TC-21 | Overdue Handling | Phiếu BR001 cập nhật trạng thái "quá hạn" | Phiếu BR001 cập nhật trạng thái "quá hạn" | Pass | | |
| TC-22 | Overdue Handling | Phiếu mới giữ trạng thái "Đang mượn" | Phiếu mới giữ trạng thái "Đang mượn" | Pass | | |
| TC-23| Overdue Handling | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Pass | | |

### REQ-07 - Member Management
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-24 | Member Management | Nhìn thấy nút "thêm thành viên" | Nhìn thấy nút "thêm thành viên" | Pass | | |
| TC-25 | Member Management | Thêm thành viên thành công | Hệ thống báo email không hợp lệ | Fail | | |
| TC-26 | Member Management | Báo lỗi họ tên không được để trống | Báo lỗi họ tên không được để trống | Pass | | |
| TC-27 | Member Management | Báo lỗi email không hợp lệ | Báo lỗi email không hợp lệ | Pass | | |
| TC-28 | Member Management | Báo lỗi email không hợp lệ | Thêm thành viên thành công | Fail | | |
| TC-29 | Member Management | Báo lỗi email đã tồn tại trong hệ thống | Báo lỗi email không hợp lệ | Fail | | |

### REQ-08 Ticket Lookup
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-30 | Ticket Lookup | Xem được phiếu mượn của tất cả thành  | Xem được phiếu mượn của tất cả thành viên | Pass | | |
| TC-31 | Ticket Lookup | Chỉ hiển thị phiếu mượn của chính mình | Chỉ hiển thị phiếu mượn của chính mình | Pass | | |
| TC-32 | Ticket Lookup | Chặn hiển thị dữ liệu | Hiển thị dữ liệu của thành viên `MEM003` | Fail | | |
| TC-33 | Ticket Lookup | Hiển thị thông tin phiếu | Hiển thị thông tin phiếu | Pass | | |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `33` |
| Pass | `26` |
| Fail | `7` |
| Blocked | `0` |
| Not Run | `0` |
| **Tỷ lệ Pass** | `79%` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Login | 4 | 4 | 0 | 100% |
| Search Function | 7 | 5 | 2 | 71%
| Book List | 2 | 2 | 0 | 100% |
| Book Borrow| 5 | 4 | 1 | 80% | 
| Overdue Handling | 5 | 5 | 0 | 100%
| Member Management | 6 | 3 | 3| 50%
| Ticket Lookup | 4 | 3 | 1 | 75%

