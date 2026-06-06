# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | `Nhóm 17` |
| **Lớp** | `STQA2A` |
| **Ngày báo cáo** | `02/06/2026` |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `34` |
| Pass | `27` |
| Fail | `7` |
| Blocked | `0` |
| Not Run | `0` |
| **Tỷ lệ Pass** | `79.4%` |
| **Số bug phát hiện** | `7` |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|---------------|-----|------|------|-----|---------|
| Đăng nhập (REQ-01) | 4 | 4 | 0 | 0 | ✅ Tốt — hoạt động đúng theo yêu cầu |
| Xem danh sách sách (REQ-02) | 3 | 3 | 0 | 0 | ✅ Tốt — hiển thị đầy đủ, đúng trạng thái |
| Tìm kiếm sách (REQ-03) | 7 | 5 | 2 | 2 | ⚠️ Có lỗi — tìm theo thể loại phân biệt hoa/thường |
| Mượn sách (REQ-04, 05) | 5 | 4 | 1 | 1 | ⚠️ Có lỗi nghiêm trọng — vượt giới hạn 3 sách |
| Xử lý sách quá hạn (REQ-06) | 5 | 5 | 0 | 0 | ✅ Tốt — phân quyền và xử lý đúng |
| Quản lý thành viên (REQ-07) | 6 | 3 | 3 | 3 | ❌ Yếu — nhiều lỗi validate email nghiêm trọng |
| Tra cứu phiếu mượn (REQ-08) | 4 | 3 | 1 | 1 | ⚠️ Có lỗi — vi phạm quyền riêng tư dữ liệu |
| **Tổng** | **34** | **27** | **7** | **7** | |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
|--------|---------|---------|
| High | 6 | BUG-01, BUG-02, BUG-03, BUG-04, BUG-05, BUG-07 |
| Medium | 0 | — |
| Low | 1 | BUG-06 |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
|----------|---------------------|---------------|------------------------|
| **EP** (Equivalence Partitioning — Phân lớp tương đương) | REQ-01 → REQ-08 (tất cả) | 34 | Phân chia đầu vào thành các lớp tương đương: hợp lệ / không hợp lệ / rỗng. Ví dụ: email tồn tại / không tồn tại, tài khoản hoạt động / tạm ngưng / hết hạn |
| **BVA** (Boundary Value Analysis — Phân tích giá trị biên) | REQ-01, REQ-04, REQ-05, REQ-06 | 8 | Kiểm tra các giá trị biên: ô nhập rỗng (TC-04), số sách mượn tại đúng giới hạn 3 cuốn (TC-15, TC-19), ngày hết hạn đúng ngày hôm nay / vượt ngày (TC-22, TC-23) |
| **IDM** (Input Domain Modeling — Mô hình hóa miền đầu vào) | REQ-01 → REQ-08 (tất cả) | 34 | Phân tích đặc tính (Characteristic), phân vùng (Block), và giá trị đại diện (Value) trước khi thiết kế TC. Áp dụng cho tất cả 8 chức năng |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh

- **Đăng nhập (REQ-01)**: Xác thực email/mật khẩu hoạt động chính xác. Các thông báo lỗi rõ ràng, thân thiện với người dùng. Kiểm tra ô trống hoạt động đúng.
- **Hiển thị danh sách sách (REQ-02)**: Toàn bộ thông tin sách (tên, tác giả, năm xuất bản, trạng thái) được hiển thị đầy đủ và chính xác.
- **Tìm kiếm theo tên/tác giả (REQ-03)**: Tìm kiếm theo tên sách và tác giả không phân biệt hoa/thường — hoạt động tốt.
- **Kiểm soát mượn sách cơ bản (REQ-04, 05)**: Chặn mượn khi sách đang được mượn, tài khoản tạm ngưng, tài khoản hết hạn — tất cả hoạt động đúng.
- **Xử lý sách quá hạn (REQ-06)**: Phân quyền giữa thủ thư và thành viên rõ ràng. Hệ thống đánh dấu quá hạn đúng ngày. Thành viên chỉ thấy phiếu của mình.
- **Tra cứu phiếu mượn cơ bản (REQ-08)**: Thủ thư xem được tất cả phiếu. Thành viên chỉ thấy phiếu của mình khi truy cập bình thường.

### 4.2. Điểm yếu

- **Quản lý thành viên (REQ-07) — Nghiêm trọng nhất**: Chức năng thêm thành viên có 3 lỗi cùng lúc:
  - Không thể thêm thành viên với email hợp lệ (BUG-04) → chức năng cốt lõi bị gãy hoàn toàn.
  - Chấp nhận email sai định dạng (thiếu dấu `.`) (BUG-05) → dữ liệu bẩn vào hệ thống.
  - Thông báo lỗi sai khi email trùng (BUG-06) → gây nhầm lẫn cho người dùng.
- **Giới hạn mượn sách (REQ-04, 05) — Nghiêm trọng**: Hệ thống cho phép mượn cuốn sách thứ 4 trong khi giới hạn là 3 (BUG-03). Vi phạm trực tiếp quy tắc nghiệp vụ.
- **Tìm kiếm theo thể loại (REQ-03)**: Bộ lọc thể loại phân biệt hoa/thường (BUG-01, BUG-02). Người dùng nhập `kinh tế` hoặc `KINH TẾ` đều không ra kết quả — trải nghiệm rất tệ.
- **Bảo mật dữ liệu (REQ-08) — Nghiêm trọng**: Thành viên có thể xem phiếu mượn của thành viên khác bằng cách nhập mã thành viên vào ô tìm kiếm (BUG-07) → vi phạm quyền riêng tư.

---

## 5. Đề xuất ưu tiên sửa lỗi

> 💡 Tiêu chí ưu tiên: **Severity** (mức độ nghiêm trọng kỹ thuật) kết hợp **Priority** (tác động nghiệp vụ). Ưu tiên cao = ảnh hưởng đến tính toàn vẹn dữ liệu, quyền truy cập, hoặc chức năng cốt lõi bị gãy hoàn toàn.

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 🔴 1 | **BUG-04** — Không thêm được thành viên dù nhập đúng | High | Chức năng thêm thành viên **hoàn toàn không hoạt động** — thủ thư không thể quản lý hệ thống |
| 🔴 2 | **BUG-07** — Thành viên xem được phiếu mượn của người khác | High | **Vi phạm bảo mật và quyền riêng tư** — dữ liệu cá nhân bị lộ |
| 🔴 3 | **BUG-03** — Cho mượn sách thứ 4 (vượt giới hạn 3) | High | **Vi phạm quy tắc nghiệp vụ** — ảnh hưởng đến tính toàn vẹn dữ liệu mượn trả |
| 🟠 4 | **BUG-05** — Thêm thành viên thành công dù email sai định dạng | High | Dữ liệu bẩn (email không hợp lệ) vào database, gây hậu quả lâu dài |
| 🟠 5 | **BUG-01** — Tìm thể loại không ra kết quả khi nhập chữ thường | High | Ảnh hưởng trực tiếp đến trải nghiệm người dùng khi tìm sách |
| 🟠 6 | **BUG-02** — Tìm thể loại không ra kết quả khi nhập chữ HOA | High | Cùng gốc với BUG-01, sửa một lần giải quyết cả hai |
| 🟡 7 | **BUG-06** — Thông báo lỗi sai khi email trùng | Low | Gây nhầm lẫn cho thủ thư nhưng không ảnh hưởng đến dữ liệu |

---

## 6. Kết luận

**Hệ thống chưa sẵn sàng phát hành (Not Ready for Release).**

Sau khi kiểm thử toàn bộ 34 test case trên 8 chức năng chính, nhóm ghi nhận tỷ lệ pass đạt **79.4%** với **7 lỗi** được phát hiện, trong đó **6 lỗi mức High**. Cụ thể:

- Chức năng **Quản lý thành viên (REQ-07)** gần như **không hoạt động được** — thủ thư không thể thêm thành viên hợp lệ vào hệ thống trong khi hệ thống lại chấp nhận email sai định dạng.
- Chức năng **Mượn sách (REQ-04, 05)** vi phạm giới hạn 3 sách — dữ liệu mượn trả mất tính toàn vẹn.
- Chức năng **Tra cứu phiếu mượn (REQ-08)** có lỗ hổng quyền truy cập nghiêm trọng — vi phạm quyền riêng tư của thành viên.

Các chức năng hoạt động tốt gồm: Đăng nhập, Hiển thị danh sách sách, Xử lý sách quá hạn, và tìm kiếm theo tên/tác giả.

**Khuyến nghị**: Ưu tiên sửa ngay BUG-04, BUG-07, BUG-03 trước khi triển khai. Cần kiểm thử lại (regression testing) toàn bộ REQ-07 và REQ-08 sau khi sửa.

---

## 7. Bài học rút ra

- **Thiết kế test case trước khi chạy** giúp phủ đều các luồng (happy path, negative, boundary) và tránh bỏ sót chức năng quan trọng.
- **BVA cực kỳ hiệu quả** cho các giới hạn số (giới hạn 3 sách mượn) — nếu không áp dụng BVA, có thể bỏ qua BUG-03.
- **Phân quyền (authorization)** là một trong những điểm dễ bị bỏ qua nhưng có tác động bảo mật cao. Cần test phân quyền cho từng vai trò ở từng tính năng.
- **Thông báo lỗi cần được kiểm thử riêng** — lỗi không chỉ là "chức năng bị gãy" mà còn là "thông báo sai" (như BUG-06) gây nhầm lẫn cho người dùng.
- Sử dụng **IDM (Input Domain Modeling)** trước khi viết test case giúp nhóm hệ thống hóa các trường hợp kiểm thử và không bỏ sót phân vùng quan trọng.

---

## 8. Khai báo sử dụng AI

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| Gemini | Hỗ trợ tổng hợp báo cáo summary dựa trên dữ liệu thực tế đã có | Toàn bộ số liệu (TC, Pass/Fail, Bug) lấy từ kết quả thực thi thực tế của nhóm. Hỗ trợ kiểm tra lại từng mục trước khi nộp |
