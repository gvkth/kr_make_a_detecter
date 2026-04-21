# User Story (Câu Chuyện Người Dùng)

## Định Nghĩa

**User Story** là một mô tả ngắn gọn về một tính năng từ góc nhìn người dùng cuối. User story tập trung vào giá trị mà người dùng nhận được, không phải chi tiết kỹ thuật.

## Format Chuẩn

```
Là một [vai trò],
Tôi muốn [tính năng/hành động],
Để tôi có thể [lợi ích/giá trị].
```

**Tiếng Anh**:
```
As a [role],
I want [feature/action],
So that [benefit/value].
```

## Ví Dụ Từ Dự Án Gridex

### User Story 1:
```
Là một người dùng lo ngại về bảo mật,
Tôi muốn quét toàn bộ thư mục Gridex,
Để tôi có thể biết phần mềm đã cài đặt những file gì trên máy tôi.
```

### User Story 2:
```
Là một người dùng quan tâm đến quyền riêng tư,
Tôi muốn biết phần mềm Gridex thu thập dữ liệu gì,
Để tôi có thể quyết định có nên tiếp tục sử dụng hay không.
```

### User Story 3:
```
Là một security analyst,
Tôi muốn xem báo cáo chi tiết về các rủi ro được phát hiện,
Để tôi có thể đánh giá mức độ nguy hiểm và đề xuất biện pháp khắc phục.
```

## 3 Thành Phần Của User Story (3 C's)

### 1. Card (Thẻ)
- User story được viết trên thẻ (physical hoặc digital)
- Ngắn gọn, vừa đủ để nhớ
- Không có tất cả chi tiết

### 2. Conversation (Cuộc Trò Chuyện)
- User story là lời nhắc để nói chuyện
- Chi tiết được làm rõ qua discussion
- Không phải tài liệu đầy đủ

### 3. Confirmation (Xác Nhận)
- Acceptance Criteria xác nhận story hoàn thành
- Điều kiện để story được chấp nhận
- Có thể test được

## Acceptance Criteria (Tiêu Chí Chấp Nhận)

Acceptance Criteria định nghĩa "xong" là gì.

### Format 1: Given-When-Then (Gherkin)

```
Given [điều kiện ban đầu]
When [hành động]
Then [kết quả mong đợi]
```

**Ví dụ**:
```
Given người dùng đã nhập đường dẫn hợp lệ
When người dùng nhấn nút "Phân Tích"
Then hệ thống quét tất cả files trong thư mục
And hiển thị danh sách files với metadata đầy đủ
```

### Format 2: Checklist

```
- [ ] Hệ thống quét đệ quy tất cả thư mục con
- [ ] Mỗi file có đầy đủ: path, size, dates, type
- [ ] Files ẩn cũng được phát hiện
- [ ] Thời gian quét < 30 giây cho 1000 files
```

### Format 3: EARS (Easy Approach to Requirements Syntax)

```
WHEN [điều kiện], THE [hệ thống] SHALL [hành động]
```

**Ví dụ**:
```
WHEN THE Risk_Analyzer được khởi động,
THE File_Scanner SHALL quét toàn bộ cấu trúc thư mục tại Installation_Path

THE File_Scanner SHALL liệt kê tất cả tệp tin và thư mục con 
với đường dẫn đầy đủ
```

## INVEST Criteria (Tiêu Chí Tốt Cho User Story)

Một user story tốt phải thỏa mãn INVEST:

### I - Independent (Độc Lập)
- Story có thể phát triển độc lập
- Không phụ thuộc chặt chẽ vào story khác
- Có thể thay đổi thứ tự

❌ **Không tốt**: "Thêm nút Save" (phụ thuộc vào form đã có)
✅ **Tốt**: "Người dùng có thể lưu cấu hình phân tích"

### N - Negotiable (Có Thể Thương Lượng)
- Chi tiết có thể thảo luận
- Không phải hợp đồng cứng nhắc
- Linh hoạt trong implementation

❌ **Không tốt**: "Dùng PostgreSQL database với table users có 15 columns..."
✅ **Tốt**: "Người dùng có thể lưu kết quả phân tích để xem lại sau"

### V - Valuable (Có Giá Trị)
- Mang lại giá trị cho người dùng
- Người dùng sẵn sàng trả tiền cho nó
- Giải quyết vấn đề thực sự

❌ **Không tốt**: "Refactor FileScanner class"
✅ **Tốt**: "Người dùng nhận được kết quả phân tích nhanh hơn 50%"

### E - Estimable (Có Thể Ước Lượng)
- Team có thể ước lượng effort
- Đủ rõ ràng để estimate
- Không quá mơ hồ

❌ **Không tốt**: "Cải thiện hiệu năng"
✅ **Tốt**: "Quét 1000 files trong < 30 giây"

### S - Small (Nhỏ)
- Có thể hoàn thành trong 1 sprint
- Thường 1-5 ngày
- Không quá lớn

❌ **Không tốt**: "Xây dựng hệ thống phân tích rủi ro hoàn chỉnh"
✅ **Tốt**: "Quét và liệt kê tất cả files trong thư mục Gridex"

### T - Testable (Có Thể Kiểm Thử)
- Có acceptance criteria rõ ràng
- Có thể verify hoàn thành
- Pass/Fail rõ ràng

❌ **Không tốt**: "Giao diện đẹp và dễ dùng"
✅ **Tốt**: "Người dùng có thể hoàn thành phân tích trong 3 clicks"

## Story Points (Điểm Story)

Story Points đo độ phức tạp/effort của user story.

### Fibonacci Scale (Phổ Biến Nhất)
```
1, 2, 3, 5, 8, 13, 21, 34, 55, 89
```

### Ý Nghĩa:
- **1-2**: Rất đơn giản, vài giờ
- **3-5**: Đơn giản, 1-2 ngày
- **8**: Trung bình, 3-4 ngày
- **13**: Phức tạp, 1 tuần
- **21+**: Quá lớn, cần chia nhỏ

### Ví Dụ Estimation:

**Story 1**: "Quét thư mục và liệt kê files"
- **Points**: 3
- **Lý do**: Đơn giản, dùng thư viện có sẵn

**Story 2**: "Tính hash SHA256 cho tất cả executables"
- **Points**: 5
- **Lý do**: Cần xử lý files lớn, tối ưu performance

**Story 3**: "Phát hiện sensitive data trong config files"
- **Points**: 8
- **Lý do**: Cần viết regex patterns phức tạp, nhiều edge cases

**Story 4**: "Xây dựng hệ thống phân tích rủi ro hoàn chỉnh"
- **Points**: 89
- **Lý do**: Quá lớn! Cần chia thành nhiều stories nhỏ

## Epic vs Story vs Task

### Epic (Sử Thi)
- Tính năng lớn, nhiều sprints
- Chứa nhiều user stories
- High-level

**Ví dụ**: "Hệ thống phân tích rủi ro Gridex"

### User Story (Câu Chuyện)
- Tính năng nhỏ, 1 sprint
- Có thể demo được
- Mang giá trị cho người dùng

**Ví dụ**: "Quét và phân tích thư mục Gridex"

### Task (Nhiệm Vụ)
- Công việc kỹ thuật cụ thể
- Không nhất thiết có giá trị trực tiếp cho user
- Vài giờ đến 1 ngày

**Ví dụ**: 
- "Viết FileScanner class"
- "Viết unit tests cho FileScanner"
- "Tạo database migration"

### Hierarchy (Phân Cấp):
```
Epic
  ├── User Story 1
  │     ├── Task 1.1
  │     ├── Task 1.2
  │     └── Task 1.3
  ├── User Story 2
  │     ├── Task 2.1
  │     └── Task 2.2
  └── User Story 3
        └── Task 3.1
```

## User Story Trong Dự Án Gridex

### Epic: Phân Tích Rủi Ro Gridex

#### Story 1: Quét Cấu Trúc Thư Mục
```
Là một người dùng,
Tôi muốn quét toàn bộ cấu trúc thư mục của Gridex,
Để tôi có thể biết phần mềm đã cài đặt những gì trên hệ thống.

Acceptance Criteria:
- Hệ thống quét đệ quy tất cả thư mục con
- Mỗi file có: path, size, created date, modified date, type
- Files ẩn được phát hiện
- Kết quả hiển thị trong < 5 giây cho 1000 files

Story Points: 3
```

#### Story 2: Phân Tích Tệp Cấu Hình
```
Là một người dùng quan tâm đến quyền riêng tư,
Tôi muốn biết phần mềm có lưu trữ thông tin nhạy cảm không,
Để tôi có thể đánh giá rủi ro rò rỉ dữ liệu.

Acceptance Criteria:
- Hệ thống phân tích settings.json
- Phát hiện API keys, passwords, tokens, emails
- Đánh dấu rủi ro "Cao" nếu lưu plaintext
- Hiển thị preview (first/last 4 chars) của sensitive data

Story Points: 5
```

#### Story 3: Giám Sát Kết Nối Mạng
```
Là một người dùng,
Tôi muốn biết phần mềm kết nối đến đâu,
Để tôi có thể đánh giá rủi ro rò rỉ dữ liệu.

Acceptance Criteria:
- Hệ thống phân tích log file
- Trích xuất tất cả domains, IPs, ports
- Xác định mục đích: update, API, telemetry
- Đánh dấu rủi ro "Cao" cho unknown domains
- Đánh dấu rủi ro "Trung Bình" cho HTTP (không mã hóa)

Story Points: 8
```

## Story Mapping (Bản Đồ Story)

Story Mapping giúp visualize toàn bộ user journey.

```
User Journey: Phân Tích Rủi Ro Gridex
─────────────────────────────────────────────────────────
Khởi động    Quét hệ thống    Phân tích    Xem kết quả
─────────────────────────────────────────────────────────
│            │                │            │
▼            ▼                ▼            ▼
Nhập path    Quét files       Phân tích    Hiển thị
             Quét config      cấu hình     báo cáo
             Quét logs        Phân tích    
                              logs         Xuất PDF
                              Tính điểm    
```

## Best Practices

### 1. Viết Từ Góc Nhìn Người Dùng
❌ **Không tốt**: "Hệ thống cần có FileScanner class"
✅ **Tốt**: "Người dùng có thể xem danh sách files đã cài đặt"

### 2. Tập Trung Vào Giá Trị
❌ **Không tốt**: "Thêm button vào UI"
✅ **Tốt**: "Người dùng có thể xuất báo cáo ra PDF để chia sẻ"

### 3. Giữ Ngắn Gọn
- 1-2 câu cho story
- Chi tiết trong acceptance criteria
- Không viết specification đầy đủ

### 4. Dùng Ngôn Ngữ Người Dùng
❌ **Không tốt**: "Parse JSON config với regex để extract API keys"
✅ **Tốt**: "Người dùng biết được phần mềm có lưu API key không"

### 5. Có Acceptance Criteria Rõ Ràng
- Mỗi story phải có AC
- AC phải testable
- AC định nghĩa "Done"

### 6. Ưu Tiên Stories
- **Must Have**: Không thể thiếu
- **Should Have**: Quan trọng nhưng không critical
- **Could Have**: Nice to have
- **Won't Have**: Không làm trong version này

## Công Cụ Quản Lý User Stories

### Agile Tools:
- **Jira**: Industry standard, powerful
- **Azure DevOps**: Microsoft ecosystem
- **Trello**: Simple, visual
- **Asana**: User-friendly
- **Linear**: Modern, fast

### Physical:
- **Index Cards**: Traditional, tactile
- **Sticky Notes**: Flexible, easy to move
- **Whiteboard**: Great for story mapping

## User Story vs Use Case

| Khía Cạnh | User Story | Use Case |
|-----------|------------|----------|
| **Độ dài** | 1-3 câu | 1-3 trang |
| **Chi tiết** | High-level | Chi tiết |
| **Luồng xử lý** | Không có | Có đầy đủ |
| **Thời gian viết** | 5-15 phút | 1-4 giờ |
| **Phù hợp** | Agile | Waterfall |
| **Mục đích** | Planning & communication | Detailed specification |

## Tài Liệu Tham Khảo

- "User Stories Applied" - Mike Cohn
- "Agile Estimating and Planning" - Mike Cohn
- "User Story Mapping" - Jeff Patton
- Scrum Guide - Ken Schwaber & Jeff Sutherland
