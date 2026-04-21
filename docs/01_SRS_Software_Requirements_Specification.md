# SRS - Software Requirements Specification (Đặc Tả Yêu Cầu Phần Mềm)

## Định Nghĩa

**SRS (Software Requirements Specification)** là tài liệu chính thức mô tả đầy đủ các yêu cầu chức năng và phi chức năng của một hệ thống phần mềm. Đây là "hợp đồng" giữa khách hàng và đội phát triển về những gì phần mềm sẽ làm.

## Mục Đích

- Định nghĩa rõ ràng những gì hệ thống phải làm
- Làm cơ sở cho thiết kế và phát triển
- Làm tiêu chuẩn để kiểm thử và xác nhận
- Làm tài liệu tham khảo cho bảo trì

## Cấu Trúc Theo IEEE 830

### 1. Introduction (Giới Thiệu)
- **Purpose**: Mục đích của tài liệu SRS
- **Scope**: Phạm vi của hệ thống
- **Definitions, Acronyms, Abbreviations**: Bảng thuật ngữ
- **References**: Tài liệu tham khảo
- **Overview**: Tổng quan về cấu trúc tài liệu

### 2. Overall Description (Mô Tả Tổng Quan)
- **Product Perspective**: Vị trí của sản phẩm trong hệ sinh thái
- **Product Functions**: Các chức năng chính
- **User Characteristics**: Đặc điểm người dùng
- **Constraints**: Các ràng buộc
- **Assumptions and Dependencies**: Giả định và phụ thuộc

### 3. Specific Requirements (Yêu Cầu Cụ Thể)
- **Functional Requirements**: Yêu cầu chức năng
  - Mỗi chức năng được mô tả chi tiết
  - Đầu vào, xử lý, đầu ra
  - Điều kiện tiên quyết và hậu quả
- **Non-Functional Requirements**: Yêu cầu phi chức năng
  - Performance (hiệu năng)
  - Security (bảo mật)
  - Usability (khả năng sử dụng)
  - Reliability (độ tin cậy)
  - Maintainability (khả năng bảo trì)

### 4. Appendices (Phụ Lục)
- Sơ đồ, bảng biểu bổ sung
- Mẫu giao diện người dùng

## Ví Dụ Từ Dự Án Gridex

### Functional Requirement Example:

**FR-1: File Scanning**
- **Description**: Hệ thống phải quét toàn bộ cấu trúc thư mục của Gridex
- **Input**: Đường dẫn cài đặt (C:\Users\Admin\AppData\Local\Gridex)
- **Processing**: 
  - Duyệt đệ quy tất cả thư mục con
  - Thu thập metadata của mỗi file
  - Xác định loại file
- **Output**: Danh sách FileInfo objects
- **Preconditions**: Đường dẫn phải tồn tại và có quyền đọc
- **Postconditions**: Tất cả files được liệt kê với metadata đầy đủ

### Non-Functional Requirement Example:

**NFR-1: Performance**
- Hệ thống phải quét được 1000 files trong vòng 5 giây
- Bộ nhớ sử dụng không vượt quá 500MB

**NFR-2: Security**
- Hệ thống chỉ đọc dữ liệu, không ghi hoặc sửa đổi
- Không gửi dữ liệu ra ngoài mà không có sự đồng ý

## So Sánh SRS vs Requirements.md Của Kiro

| Khía Cạnh | SRS (IEEE 830) | Kiro requirements.md |
|-----------|----------------|----------------------|
| **Độ chính thức** | Rất chính thức, theo chuẩn | Linh hoạt hơn |
| **Cấu trúc** | Cố định theo IEEE | Tùy chỉnh theo dự án |
| **Ngôn ngữ** | Kỹ thuật, chính thức | Dễ hiểu, user-friendly |
| **Acceptance Criteria** | Có thể có hoặc không | Luôn có (format EARS) |
| **User Stories** | Không bắt buộc | Luôn có |
| **Độ dài** | Thường rất dài (50-200 trang) | Ngắn gọn hơn (10-30 trang) |

## Khi Nào Dùng SRS?

✅ **Nên dùng SRS khi:**
- Dự án lớn, phức tạp
- Yêu cầu tuân thủ chuẩn (compliance)
- Nhiều stakeholders
- Hợp đồng chính thức với khách hàng
- Dự án outsourcing

❌ **Không cần SRS khi:**
- Dự án nhỏ, nội bộ
- Startup, MVP nhanh
- Agile team nhỏ
- Yêu cầu thay đổi liên tục

## Lợi Ích

✅ Rõ ràng, không mơ hồ
✅ Đầy đủ, bao quát
✅ Có thể kiểm chứng
✅ Làm cơ sở pháp lý
✅ Giảm hiểu lầm giữa các bên

## Nhược Điểm

❌ Mất nhiều thời gian viết
❌ Khó thay đổi khi yêu cầu đổi
❌ Có thể quá chi tiết, cứng nhắc
❌ Không phù hợp với Agile

## Best Practices

1. **Sử dụng ngôn ngữ rõ ràng**: Tránh mơ hồ như "nhanh", "tốt", "dễ dùng"
2. **Đánh số yêu cầu**: FR-1, FR-2, NFR-1 để dễ tham chiếu
3. **Ưu tiên yêu cầu**: Must-have, Should-have, Nice-to-have
4. **Review kỹ**: Để tất cả stakeholders review và approve
5. **Version control**: Quản lý phiên bản của SRS
6. **Traceability matrix**: Liên kết requirements với design và test cases

## Công Cụ Hỗ Trợ

- **IBM DOORS**: Enterprise requirements management
- **Jama Connect**: Requirements và test management
- **Confluence**: Wiki-based documentation
- **Google Docs/Word**: Đơn giản, phổ biến
- **Markdown**: Lightweight, version control friendly

## Tài Liệu Tham Khảo

- IEEE Std 830-1998: IEEE Recommended Practice for Software Requirements Specifications
- ISO/IEC/IEEE 29148:2018: Systems and software engineering — Life cycle processes — Requirements engineering
