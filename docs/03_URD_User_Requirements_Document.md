# URD - User Requirements Document (Tài Liệu Yêu Cầu Người Dùng)

## Định Nghĩa

**URD (User Requirements Document)** là tài liệu mô tả yêu cầu từ góc nhìn người dùng cuối, tập trung vào "người dùng cần gì" thay vì "hệ thống làm gì". URD được viết bằng ngôn ngữ nghiệp vụ, không có thuật ngữ kỹ thuật.

## Mục Đích

- Nắm bắt nhu cầu thực sự của người dùng
- Làm cầu nối giữa business và technical team
- Đảm bảo phần mềm giải quyết đúng vấn đề
- Làm cơ sở để viết SRS (System Requirements Specification)

## Sự Khác Biệt: URD vs SRS

| Khía Cạnh | URD | SRS |
|-----------|-----|-----|
| **Góc nhìn** | Người dùng | Hệ thống |
| **Ngôn ngữ** | Nghiệp vụ, dễ hiểu | Kỹ thuật |
| **Người viết** | Business Analyst, Product Owner | System Analyst, Architect |
| **Người đọc** | Stakeholders, người dùng | Developers, testers |
| **Nội dung** | Nhu cầu, mục tiêu | Chức năng, constraints |
| **Chi tiết** | High-level | Chi tiết kỹ thuật |

**Ví dụ:**

**URD**: "Tôi cần biết phần mềm Gridex có an toàn không, có thu thập dữ liệu cá nhân của tôi không."

**SRS**: "Hệ thống phải quét file settings.json, phát hiện các trường chứa API key, email, user ID bằng regex patterns, và đánh dấu là Privacy Risk nếu được lưu dưới dạng plaintext."

## Cấu Trúc URD

### 1. Executive Summary (Tóm Tắt Điều Hành)
- Tổng quan về dự án
- Vấn đề cần giải quyết
- Lợi ích mong đợi

### 2. Business Context (Bối Cảnh Nghiệp Vụ)
- Tình huống hiện tại
- Vấn đề đang gặp phải
- Tại sao cần giải pháp mới

### 3. User Profiles (Hồ Sơ Người Dùng)
- Ai sẽ dùng hệ thống?
- Đặc điểm của họ (kỹ năng, kinh nghiệm)
- Môi trường làm việc

### 4. User Goals (Mục Tiêu Người Dùng)
- Người dùng muốn đạt được gì?
- Thành công được đo lường như thế nào?

### 5. User Requirements (Yêu Cầu Người Dùng)
- Danh sách các nhu cầu cụ thể
- Viết dưới dạng "Người dùng cần..."
- Không có chi tiết kỹ thuật

### 6. User Scenarios (Kịch Bản Người Dùng)
- Mô tả cách người dùng sẽ dùng hệ thống
- Câu chuyện thực tế
- Ngữ cảnh sử dụng

### 7. Constraints (Ràng Buộc)
- Giới hạn từ phía người dùng
- Môi trường, thiết bị
- Thời gian, ngân sách

## Ví Dụ URD Cho Dự Án Gridex

### 1. Executive Summary

**Vấn đề**: Người dùng tải phần mềm miễn phí Gridex từ internet nhưng không biết phần mềm này có an toàn không, có thu thập dữ liệu cá nhân không, có kết nối đến đâu.

**Giải pháp**: Công cụ phân tích tự động để đánh giá rủi ro bảo mật và quyền riêng tư của phần mềm Gridex.

**Lợi ích**: 
- Người dùng biết được phần mềm có an toàn không
- Quyết định có nên tiếp tục sử dụng hay gỡ bỏ
- Hiểu rõ dữ liệu nào đang được thu thập

### 2. Business Context

**Tình huống hiện tại**:
- Người dùng đã cài đặt Gridex vào máy tính
- Gridex là phần mềm miễn phí, nguồn gốc không rõ ràng
- Người dùng lo ngại về bảo mật và quyền riêng tư

**Vấn đề**:
- Không biết phần mềm làm gì trong nền
- Không biết phần mềm kết nối đến đâu
- Không biết dữ liệu nào được thu thập
- Không có công cụ để tự kiểm tra

**Tại sao cần giải pháp**:
- Bảo vệ quyền riêng tư cá nhân
- Tránh rủi ro bảo mật
- Đưa ra quyết định có căn cứ

### 3. User Profiles

**Người dùng chính**: Người dùng máy tính cá nhân

**Đặc điểm**:
- Tuổi: 18-60
- Kỹ năng máy tính: Cơ bản đến trung bình
- Không có kiến thức chuyên sâu về bảo mật
- Quan tâm đến quyền riêng tư
- Muốn công cụ đơn giản, dễ dùng

**Môi trường**:
- Windows 10/11
- Máy tính cá nhân tại nhà hoặc văn phòng
- Có kết nối internet

### 4. User Goals

**Mục tiêu chính**:
1. Biết được phần mềm Gridex có an toàn không
2. Hiểu phần mềm thu thập dữ liệu gì
3. Quyết định có nên tiếp tục dùng hay gỡ bỏ

**Tiêu chí thành công**:
- Nhận được báo cáo dễ hiểu về mức độ rủi ro
- Biết được các vấn đề cụ thể (nếu có)
- Có hướng dẫn khắc phục rõ ràng

### 5. User Requirements

**UR-1: Kiểm Tra Phần Mềm Đã Cài Đặt**
- Người dùng cần biết Gridex đã cài đặt những file gì trên máy
- Người dùng cần biết kích thước và vị trí của các file

**UR-2: Phát Hiện Thông Tin Nhạy Cảm**
- Người dùng cần biết phần mềm có lưu trữ mật khẩu, API key không
- Người dùng cần biết thông tin này có được mã hóa không

**UR-3: Kiểm Tra Kết Nối Mạng**
- Người dùng cần biết phần mềm kết nối đến website/server nào
- Người dùng cần biết mục đích của các kết nối này

**UR-4: Đánh Giá Cơ Chế Cập Nhật**
- Người dùng cần biết phần mềm tự động cập nhật như thế nào
- Người dùng cần biết nguồn cập nhật có đáng tin cậy không

**UR-5: Hiểu Quyền Truy Cập**
- Người dùng cần biết phần mềm có quyền truy cập gì
- Người dùng cần biết phần mềm có thể đọc file cá nhân không

**UR-6: Nhận Báo Cáo Dễ Hiểu**
- Người dùng cần báo cáo bằng tiếng Việt
- Người dùng cần đánh giá tổng thể: An toàn / Nguy hiểm
- Người dùng cần giải thích rõ ràng cho mỗi vấn đề

**UR-7: Nhận Hướng Dẫn Khắc Phục**
- Người dùng cần biết nên làm gì tiếp theo
- Người dùng cần hướng dẫn từng bước cụ thể

### 6. User Scenarios

**Scenario 1: Người dùng lo ngại về bảo mật**

*Bối cảnh*: Mai vừa cài đặt Gridex để quản lý công việc. Bạn của Mai nói rằng phần mềm miễn phí thường có rủi ro. Mai muốn kiểm tra.

*Hành động*:
1. Mai mở công cụ phân tích rủi ro
2. Mai nhập đường dẫn cài đặt Gridex
3. Mai nhấn nút "Phân Tích"
4. Công cụ quét và phân tích (Mai thấy progress bar)
5. Sau 30 giây, báo cáo hiển thị

*Kết quả*:
- Mai thấy mức độ rủi ro: "Trung Bình"
- Mai đọc được: "Phần mềm kết nối đến 3 servers, 1 server không rõ nguồn gốc"
- Mai quyết định gỡ bỏ Gridex vì không yên tâm

**Scenario 2: Người dùng muốn hiểu thu thập dữ liệu**

*Bối cảnh*: Hùng dùng Gridex được 1 tháng. Hùng nghi ngờ phần mềm thu thập dữ liệu cá nhân.

*Hành động*:
1. Hùng chạy công cụ phân tích
2. Hùng xem phần "Thu Thập Dữ Liệu" trong báo cáo

*Kết quả*:
- Hùng thấy: "Phần mềm lưu trữ User ID và API key dưới dạng plaintext"
- Hùng thấy: "Phần mềm gửi dữ liệu sử dụng đến analytics.example.com"
- Hùng quyết định thay đổi mật khẩu và gỡ bỏ phần mềm

### 7. Constraints

**Ràng buộc từ người dùng**:
- Người dùng không có kiến thức kỹ thuật sâu
- Người dùng muốn kết quả nhanh (< 1 phút)
- Người dùng không muốn cài đặt phức tạp
- Người dùng muốn công cụ miễn phí

**Ràng buộc môi trường**:
- Chỉ hỗ trợ Windows
- Cần quyền đọc thư mục Gridex
- Không cần kết nối internet (phân tích offline)

## URD vs User Story

**URD** là tài liệu tổng thể về tất cả yêu cầu người dùng.

**User Story** là một yêu cầu cụ thể, nhỏ, có thể implement trong 1 sprint.

**Quan hệ**: URD chứa nhiều User Stories.

**Ví dụ**:
- **URD**: "Người dùng cần biết phần mềm có an toàn không" (high-level)
- **User Story**: "Là một người dùng, tôi muốn quét thư mục Gridex, để tôi có thể biết phần mềm đã cài đặt những gì" (specific)

## Khi Nào Viết URD?

✅ **Nên viết URD khi:**
- Dự án lớn với nhiều stakeholders
- Cần alignment giữa business và technical
- Người dùng cuối không phải là người yêu cầu dự án
- Cần tài liệu để trình bày với management

❌ **Không cần URD khi:**
- Dự án nhỏ, nội bộ
- Team hiểu rõ người dùng
- Agile team với Product Owner tốt
- Có thể nói chuyện trực tiếp với người dùng

## Quy Trình Tạo URD

1. **Phỏng vấn người dùng**: Hiểu nhu cầu thực sự
2. **Quan sát**: Xem người dùng làm việc như thế nào
3. **Workshop**: Tổ chức buổi làm việc với stakeholders
4. **Viết draft**: Tạo bản nháp URD
5. **Review với người dùng**: Xác nhận đúng nhu cầu
6. **Finalize**: Hoàn thiện và approve

## Best Practices

1. **Viết bằng ngôn ngữ người dùng**: Không dùng thuật ngữ kỹ thuật
2. **Tập trung vào "cái gì" không phải "như thế nào"**: Nhu cầu, không phải giải pháp
3. **Dùng ví dụ thực tế**: Scenarios giúp dễ hiểu
4. **Ưu tiên yêu cầu**: Must-have vs Nice-to-have
5. **Validate với người dùng**: Đảm bảo đúng nhu cầu
6. **Giữ ngắn gọn**: 10-20 trang, không quá dài

## Mapping URD → SRS → Design

```
URD (User Requirements)
  ↓
SRS (System Requirements)
  ↓
Design Document
  ↓
Implementation
```

**Ví dụ**:

**URD**: "Người dùng cần biết phần mềm kết nối đến đâu"

**SRS**: "Hệ thống phải phân tích log file để trích xuất tất cả kết nối mạng với domain, IP, port"

**Design**: "NetworkMonitor class với method parse_log_file() trả về List[NetworkConnection]"

**Implementation**: Code Python thực tế

## Công Cụ Viết URD

- **Microsoft Word**: Phổ biến, dễ dùng
- **Google Docs**: Collaboration tốt
- **Confluence**: Wiki-based, tích hợp Jira
- **Notion**: Modern, flexible
- **Markdown**: Simple, version control

## Tài Liệu Tham Khảo

- "User and Task Analysis for Interface Design" - JoAnn Hackos & Janice Redish
- "The User Experience Team of One" - Leah Buley
- ISO/IEC 25010: Systems and software Quality Requirements and Evaluation (SQuaRE)
