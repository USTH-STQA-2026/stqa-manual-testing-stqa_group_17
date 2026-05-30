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

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Đăng nhập thành công | Đăng nhập thành công | Pass| | |
| TC-02 | Login | Báo lỗi mật khẩu không đúng | Báo lỗi mật khẩu không đúng | Pass | | |
| TC-03 | Login | Báo lỗi không tìm thấy tài khoản |Báo lỗi không tìm thấy tài khoản | Pass | | |
| TC-04 | Login | Hiện cảnh báo "Vui lòng nhập email" | Hiện cảnh báo "Vui lòng nhập email" | Pass | | |
| TC-05 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |
| TC-06 | Search Function | Hiển thị sách có tác giả tên "Nguyễn" | Hiển thị sách có tác giả tên "Nguyễn" | Pass | | |
| TC-07 | Search Function | Hiển thị danh sách rỗng | Hiển thị danh sách rỗng  | Pass | | |
| TC-08 | Search Function | Hiển thị sách chứa từ "Flutter" | Hiển thị sách chứa từ "Flutter" | Pass | | |
| TC-09 | Book Borrow | Mượn thành công | Mượn thành công | Pass | | |
| TC-10 | Book Borrow | Không cho phép mượn | Không cho phép mượn| Pass | | |
| TC-11 | Book Borrow | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Không cho phép mượn, thông báo tài khoản bị tạm ngưng | Pass | | |
| TC-12 | Book Borrow | Không cho phép mượn, thông báo tài khoản hết hạn | Không cho phép mượn, thông báo tài khoản hết hạn | Pass | | |
| TC-13 | Book Borrow | Từ chối mượn, thông báo số sách mượn vượt giới hạn | Có thể mượn cuốn sách thứ 4 | Fail | | |
| TC-14 | Overdue Handling | Thấy nút "kiểm tra sách quá hạn" | Thấy nút "kiểm tra sách quá hạn"  | Pass | | |
| TC-15 | Overdue Handling | Không thấy nút "kiểm tra sách quá hạn" | Không thấy nút "kiểm tra sách quá hạn" | Pass | | |
| TC-16 | Overdue Handling | Phiếu BR001 cập nhật trạng thái "quá hạn" | Phiếu BR001 cập nhật trạng thái "quá hạn" | Pass | | |
| TC-17 | Overdue Handling | Phiếu mới giữ trạng thái "Đang mượn" | Phiếu mới giữ trạng thái "Đang mượn" | Pass | | |
| TC-18 | Overdue Handling | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Nhìn thấy phiếu mượn có trạng thái "quá hạn" | Pass | | |
| TC-19 | Member Management | Nhìn thấy nút "thêm thành viên" | Nhìn thấy nút "thêm thành viên" | Pass | | |
| TC-20 | Member Management | Báo lỗi họ tên không được để trống | Báo lỗi họ tên không được để trống | Pass | | |
| TC-21 | Member Management | Báo lỗi email không hợp lệ | Báo lỗi email không hợp lệ | Pass | | |
| TC-22 | Member Management | Báo lỗi email đã tồn tại trong hệ thống | Báo lỗi email không hợp lệ | Fail | | |
| TC-23 | Ticket Lookup | Xem được phiếu mượn của tất cả thành  | Xem được phiếu mượn của tất cả thành viên | Pass | | |
| TC-24 | Ticket Lookup | Chỉ hiển thị phiếu mượn của chính mình | Chỉ hiển thị phiếu mượn của chính mình | Pass | | |
| TC-25 | Ticket Lookup | Chặn hiển thị dữ liệu | Hiển thị dữ liệu của thành viên `MEM003` | Fail | | |
| TC-26 | Ticket Lookup | Hiển thị thông tin phiếu | Hiển thị thông tin phiếu | Blocked | | |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `26` |
| Pass | `22` |
| Fail | `3` |
| Blocked | `1` |
| Not Run | `0` |
| **Tỷ lệ Pass** | `84%` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
