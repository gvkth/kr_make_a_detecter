# Quy Trình Làm Việc Của Kiro: Từ Yêu Cầu Đến Triển Khai

## Tổng Quan

Quy trình làm việc của Kiro tuân theo phương pháp **Spec-Driven Development** (Phát triển hướng đặc tả), một cách tiếp cận có cấu trúc để xây dựng phần mềm. Quy trình này đảm bảo rằng mọi tính năng được suy nghĩ kỹ lưỡng, được thiết kế đầy đủ và có kế hoạch triển khai rõ ràng trước khi viết code.

## Quy Trình 3 Giai Đoạn

```
Yêu Cầu (Requirements) → Thiết Kế (Design) → Nhiệm Vụ (Tasks)
```

### Giai Đoạn 1: Thu Thập và Phân Tích Yêu Cầu (Requirements)

**Mục đích:** Hiểu rõ "CÁI GÌ" cần được xây dựng từ góc nhìn người dùng.

**Đầu vào:**
- Ý tưởng thô từ người dùng (ví dụ: "Phân tích rủi ro phần mềm Gridex")

**Quy trình:**
1. **Làm rõ mục tiêu:** Xác định vấn đề cần giải quyết
2. **Xác định người dùng:** Ai sẽ sử dụng hệ thống này?
3. **Viết User Stories:** Mô tả tính năng từ góc nhìn người dùng
   - Format: "Là một [vai trò], tôi muốn [tính năng], để tôi có thể [lợi ích]"
4. **Định nghĩa Acceptance Criteria:** Tiêu chí chấp nhận cụ thể
   - Sử dụng format EARS (Easy Approach to Requirements Syntax)
   - Format: "WHEN [điều kiện], THE [hệ thống] SHALL [hành động]"
5. **Tạo bảng thuật ngữ:** Định nghĩa các khái niệm quan trọng

**Đầu ra:**
- Tài liệu `requirements.md` chứa:
  - Giới thiệu tổng quan
  - Bảng thuật ngữ
  - 10 yêu cầu với User Stories và Acceptance Criteria

**Ví dụ từ dự án Gridex:**
```markdown
### Yêu Cầu 1: Quét Cấu Trúc Thư Mục

**User Story:** Là một người dùng, tôi muốn quét toàn bộ cấu trúc thư mục 
của Gridex, để tôi có thể biết phần mềm đã cài đặt những gì trên hệ thống.

#### Tiêu Chí Chấp Nhận
1. WHEN THE Risk_Analyzer được khởi động, THE File_Scanner SHALL quét 
   toàn bộ cấu trúc thư mục tại Installation_Path
2. THE File_Scanner SHALL liệt kê tất cả tệp tin và thư mục con với 
   đường dẫn đầy đủ
```

---

### Giai Đoạn 2: Thiết Kế Kỹ Thuật (Design)

**Mục đích:** Xác định "NHƯ THẾ NÀO" hệ thống sẽ được xây dựng.

**Đầu vào:**
- Tài liệu requirements.md đã hoàn thành

**Quy trình:**
1. **Thiết kế kiến trúc tổng thể:**
   - Xác định các thành phần chính (modules/components)
   - Vẽ sơ đồ kiến trúc (architecture diagrams)
   - Định nghĩa luồng xử lý (data flow)

2. **Thiết kế chi tiết từng thành phần:**
   - Định nghĩa giao diện (interfaces) của mỗi module
   - Xác định cấu trúc dữ liệu (data structures)
   - Mô tả thuật toán chính

3. **Thiết kế xử lý lỗi:**
   - Xác định các loại lỗi có thể xảy ra
   - Định nghĩa chiến lược xử lý lỗi

4. **Thiết kế chiến lược kiểm thử:**
   - Xác định loại tests cần viết
   - Định nghĩa Property-Based Testing properties
   - Lập kế hoạch Integration Testing

5. **Định nghĩa Correctness Properties:**
   - Xác định các tính chất đúng đắn mà hệ thống phải thỏa mãn
   - Mỗi property là một đảm bảo về hành vi của hệ thống

**Đầu ra:**
- Tài liệu `design.md` chứa:
  - Tổng quan và mục tiêu thiết kế
  - Kiến trúc hệ thống với sơ đồ
  - Chi tiết 10 modules với giao diện và cấu trúc dữ liệu
  - Mô hình dữ liệu
  - Thuật toán phát hiện rủi ro
  - Chiến lược xử lý lỗi
  - Chiến lược kiểm thử
  - 24 Correctness Properties

**Ví dụ từ dự án Gridex:**
```python
### 2. File Scanner

**Trách nhiệm:**
- Quét cấu trúc thư mục đệ quy
- Thu thập metadata của tệp tin
- Tính toán hash SHA256 cho tệp thực thi

**Giao diện:**
class FileScanner:
    def scan_directory(path: str) -> List[FileInfo]
    def calculate_hash(file_path: str) -> str
    def check_digital_signature(file_path: str) -> SignatureInfo

**Cấu trúc dữ liệu:**
@dataclass
class FileInfo:
    path: str
    size: int
    created_date: datetime
    modified_date: datetime
```

---

### Giai Đoạn 3: Lập Kế Hoạch Triển Khai (Tasks)

**Mục đích:** Chia nhỏ công việc thành các nhiệm vụ cụ thể có thể thực hiện.

**Đầu vào:**
- Tài liệu requirements.md và design.md đã hoàn thành

**Quy trình:**
1. **Chia nhỏ thành tasks:**
   - Mỗi module trong design → nhiều tasks
   - Mỗi property → 1 property test task
   - Thêm tasks cho setup, integration, documentation

2. **Sắp xếp thứ tự:**
   - Tasks phụ thuộc lẫn nhau được sắp xếp đúng thứ tự
   - Thêm checkpoints để kiểm tra tiến độ

3. **Đánh dấu tasks tùy chọn:**
   - Tasks bắt buộc: không có dấu `*`
   - Tasks tùy chọn: có dấu `*` (có thể bỏ qua cho MVP)

4. **Thêm tham chiếu:**
   - Mỗi task tham chiếu đến requirements tương ứng
   - Đảm bảo traceability (truy vết được)

**Đầu ra:**
- Tài liệu `tasks.md` chứa:
  - Danh sách tasks có cấu trúc
  - Sub-tasks chi tiết
  - Checkpoints
  - Tham chiếu đến requirements

**Ví dụ từ dự án Gridex:**
```markdown
- [ ] 3. Implement File Scanner module
  - [ ] 3.1 Create FileScanner class with directory scanning
    - Implement scan_directory() to recursively traverse directories
    - Collect file metadata (path, size, dates, type, hidden status)
    - _Requirements: 1.1, 1.2, 1.3, 1.4, 7.1_

  - [ ]* 3.2 Write property test for directory traversal
    - **Property 1: Directory Traversal Completeness**
    - **Validates: Requirements 1.1, 1.2, 1.3, 1.4**
```

---

## Mapping Với Quy Trình Phần Mềm Truyền Thống

### So Sánh Với Software Development Life Cycle (SDLC)

| Giai Đoạn SDLC Truyền Thống | Giai Đoạn Kiro | Tài Liệu Tương Ứng |
|------------------------------|----------------|---------------------|
| **1. Requirements Analysis** | Requirements Phase | requirements.md |
| **2. System Design** | Design Phase | design.md |
| **3. Implementation Planning** | Tasks Phase | tasks.md |
| **4. Implementation** | Task Execution | Source code |
| **5. Testing** | Integrated in Tasks | Test files |
| **6. Deployment** | Manual/Separate | - |
| **7. Maintenance** | Iterative updates | Updated specs |

### So Sánh Với Agile/Scrum

| Khái Niệm Agile | Tương Đương Trong Kiro |
|-----------------|------------------------|
| **Epic** | Một spec hoàn chỉnh (requirements + design + tasks) |
| **User Story** | Mỗi requirement với user story |
| **Acceptance Criteria** | Tiêu chí chấp nhận trong requirements |
| **Sprint Planning** | Tasks phase - chia nhỏ công việc |
| **Sprint Backlog** | Danh sách tasks trong tasks.md |
| **Definition of Done** | Acceptance criteria + property tests pass |
| **Technical Design** | Design document |

### So Sánh Với Waterfall Model

Kiro workflow giống Waterfall ở chỗ:
- Tuần tự: Requirements → Design → Tasks
- Mỗi giai đoạn phải hoàn thành trước khi chuyển sang giai đoạn tiếp theo
- Tài liệu hóa đầy đủ ở mỗi giai đoạn

Kiro workflow khác Waterfall ở chỗ:
- Linh hoạt hơn: có thể quay lại giai đoạn trước nếu cần
- Tích hợp testing ngay từ đầu (property-based testing)
- Checkpoints thường xuyên thay vì testing ở cuối

---

## Lợi Ích Của Quy Trình Này

### 1. Traceability (Khả Năng Truy Vết)

Mỗi dòng code có thể truy vết ngược lại:
```
Code → Task → Design Component → Requirement → User Need
```

**Ví dụ:**
- Code: `FileScanner.scan_directory()`
- Task: "3.1 Create FileScanner class with directory scanning"
- Design: "File Scanner module - scan_directory() method"
- Requirement: "Yêu Cầu 1: Quét Cấu Trúc Thư Mục"
- User Need: "Tôi muốn biết phần mềm đã cài đặt những gì"

### 2. Clarity (Rõ Ràng)

- **Requirements:** Rõ ràng về "cái gì" cần xây dựng
- **Design:** Rõ ràng về "như thế nào" xây dựng
- **Tasks:** Rõ ràng về "làm gì" tiếp theo

### 3. Quality Assurance (Đảm Bảo Chất Lượng)

- **Acceptance Criteria:** Định nghĩa rõ "xong" là gì
- **Property Tests:** Đảm bảo tính đúng đắn toàn diện
- **Checkpoints:** Phát hiện lỗi sớm

### 4. Collaboration (Cộng Tác)

- Tài liệu rõ ràng giúp team hiểu dự án
- Stakeholders có thể review requirements
- Developers có thể review design
- QA có thể viết test cases từ acceptance criteria

### 5. Maintainability (Dễ Bảo Trì)

- Tài liệu đầy đủ giúp hiểu hệ thống sau này
- Dễ dàng thêm tính năng mới
- Dễ dàng fix bugs với context đầy đủ

---

## Chi Tiết Về Các Loại Tài Liệu

### Requirements Document (Tài Liệu Yêu Cầu)

**Mục đích:** Mô tả "cái gì" cần xây dựng từ góc nhìn người dùng.

**Cấu trúc:**
1. **Giới Thiệu:** Tổng quan về hệ thống
2. **Bảng Thuật Ngữ:** Định nghĩa các khái niệm quan trọng
3. **Yêu Cầu:** Mỗi yêu cầu bao gồm:
   - User Story (câu chuyện người dùng)
   - Acceptance Criteria (tiêu chí chấp nhận)

**Đặc điểm:**
- Không có technical details
- Tập trung vào business value
- Viết bằng ngôn ngữ người dùng hiểu được
- Sử dụng format EARS cho acceptance criteria

**Người đọc chính:**
- Product Owner
- Stakeholders
- Business Analysts
- QA Engineers

---

### Design Document (Tài Liệu Thiết Kế)

**Mục đích:** Mô tả "như thế nào" hệ thống sẽ được xây dựng.

**Cấu trúc:**
1. **Tổng Quan:** Mục tiêu thiết kế, phạm vi
2. **Kiến Trúc:** Sơ đồ tổng thể, luồng xử lý
3. **Các Thành Phần:** Chi tiết từng module
   - Trách nhiệm
   - Giao diện (interfaces)
   - Cấu trúc dữ liệu
4. **Mô Hình Dữ Liệu:** Entities và relationships
5. **Thuật Toán:** Các thuật toán quan trọng
6. **Xử Lý Lỗi:** Chiến lược error handling
7. **Chiến Lược Kiểm Thử:** Testing approach
8. **Correctness Properties:** Các tính chất đúng đắn

**Đặc điểm:**
- Có technical details đầy đủ
- Bao gồm code interfaces và data structures
- Có sơ đồ minh họa
- Định nghĩa properties cho testing

**Người đọc chính:**
- Software Architects
- Senior Developers
- Technical Leads
- DevOps Engineers

---

### Tasks Document (Tài Liệu Nhiệm Vụ)

**Mục đích:** Chia nhỏ công việc thành các bước cụ thể có thể thực hiện.

**Cấu trúc:**
1. **Overview:** Tổng quan về implementation plan
2. **Tasks:** Danh sách tasks có cấu trúc
   - Main tasks (tasks cấp cao)
   - Sub-tasks (tasks chi tiết)
   - Checkpoints (điểm kiểm tra)
3. **Notes:** Ghi chú về optional tasks, dependencies

**Đặc điểm:**
- Actionable (có thể hành động ngay)
- Có thứ tự rõ ràng
- Tham chiếu đến requirements
- Phân biệt required vs optional
- Bao gồm cả implementation và testing tasks

**Người đọc chính:**
- Developers (người triển khai)
- Project Managers
- Scrum Masters

---

## Property-Based Testing: Khái Niệm Quan Trọng

### Property Là Gì?

**Property** (tính chất) là một đặc điểm hoặc hành vi mà hệ thống phải thỏa mãn với MỌI đầu vào hợp lệ.

**Ví dụ:**
- **Property:** "Với mọi danh sách files, khi quét thư mục, kết quả phải bao gồm tất cả files"
- **Không phải property:** "Khi quét thư mục X, kết quả có 5 files"

### So Sánh Property Test vs Unit Test

| Khía Cạnh | Unit Test | Property Test |
|-----------|-----------|---------------|
| **Đầu vào** | Cố định, do developer chọn | Ngẫu nhiên, tự động generate |
| **Số lượng test cases** | Ít (5-10 examples) | Nhiều (100-1000 cases) |
| **Phát hiện edge cases** | Phụ thuộc developer nghĩ ra | Tự động tìm edge cases |
| **Mục đích** | Kiểm tra ví dụ cụ thể | Kiểm tra tính chất tổng quát |

**Ví dụ Unit Test:**
```python
def test_scan_directory():
    # Test với 1 ví dụ cụ thể
    files = scanner.scan_directory("/test/folder")
    assert len(files) == 3
    assert files[0].name == "file1.txt"
```

**Ví dụ Property Test:**
```python
@given(directory_structure())  # Generate random directories
def test_scan_completeness(directory):
    # Test với nhiều directories ngẫu nhiên
    expected_files = count_all_files(directory)
    actual_files = scanner.scan_directory(directory)
    assert len(actual_files) == expected_files
```

### Lợi Ích Của Property-Based Testing

1. **Phát hiện bugs ẩn:** Tìm ra edge cases mà developer không nghĩ đến
2. **Tự động hóa:** Không cần viết nhiều test cases thủ công
3. **Tài liệu hóa:** Properties mô tả rõ hành vi mong đợi
4. **Confidence cao:** Test với hàng trăm cases thay vì vài cases

---

## Quy Trình Làm Việc Thực Tế

### Bước 1: Nhận Yêu Cầu Từ Người Dùng

**Input:** "Phân tích rủi ro phần mềm Gridex"

**Kiro thực hiện:**
1. Hỏi làm rõ: "Đây là feature mới hay bugfix?"
2. Hỏi workflow: "Bắt đầu từ requirements hay design?"
3. Xác định feature name: "gridex-risk-analysis"

---

### Bước 2: Tạo Requirements Document

**Kiro thực hiện:**
1. Phân tích yêu cầu thô
2. Xác định 10 yêu cầu chính
3. Viết user story cho mỗi yêu cầu
4. Viết acceptance criteria chi tiết
5. Tạo bảng thuật ngữ
6. Lưu vào `.kiro/specs/gridex-risk-analysis/requirements.md`

**Thời gian:** ~5-10 phút

---

### Bước 3: Tạo Design Document

**Kiro thực hiện:**
1. Nghiên cứu technical details (Velopack, Windows permissions, etc.)
2. Thiết kế kiến trúc với 10 modules
3. Định nghĩa interfaces và data structures
4. Vẽ sơ đồ kiến trúc
5. Phân tích 58 acceptance criteria
6. Consolidate thành 24 properties (loại bỏ trùng lặp)
7. Lưu vào `.kiro/specs/gridex-risk-analysis/design.md`

**Thời gian:** ~10-15 phút

---

### Bước 4: Tạo Tasks Document

**Kiro thực hiện:**
1. Chia mỗi module thành implementation tasks
2. Tạo property test task cho mỗi property
3. Thêm setup, integration, documentation tasks
4. Sắp xếp thứ tự và dependencies
5. Thêm checkpoints
6. Đánh dấu optional tasks
7. Lưu vào `.kiro/specs/gridex-risk-analysis/tasks.md`

**Thời gian:** ~5-10 phút

---

### Bước 5: Thực Hiện Tasks

**Developer (hoặc Kiro) thực hiện:**
1. Chọn task từ tasks.md
2. Đánh dấu task là "in progress"
3. Viết code theo design
4. Viết tests theo property definitions
5. Chạy tests
6. Đánh dấu task là "completed"
7. Lặp lại cho task tiếp theo

**Thời gian:** Phụ thuộc vào độ phức tạp

---

## Best Practices (Thực Hành Tốt Nhất)

### 1. Requirements Phase

✅ **Nên:**
- Viết user stories từ góc nhìn người dùng
- Sử dụng format EARS cho acceptance criteria
- Định nghĩa rõ ràng các thuật ngữ
- Tập trung vào "cái gì" chứ không phải "như thế nào"

❌ **Không nên:**
- Đưa technical details vào requirements
- Viết acceptance criteria mơ hồ
- Bỏ qua user stories

### 2. Design Phase

✅ **Nên:**
- Vẽ sơ đồ kiến trúc
- Định nghĩa rõ interfaces
- Nghiên cứu technical details
- Định nghĩa properties cho testing
- Consolidate properties để tránh trùng lặp

❌ **Không nên:**
- Thiết kế quá phức tạp
- Bỏ qua error handling
- Không định nghĩa data structures
- Viết quá nhiều properties trùng lặp

### 3. Tasks Phase

✅ **Nên:**
- Chia nhỏ tasks thành sub-tasks
- Tham chiếu đến requirements
- Thêm checkpoints
- Đánh dấu optional tasks
- Sắp xếp theo dependencies

❌ **Không nên:**
- Tasks quá lớn (>1 ngày)
- Tasks mơ hồ không actionable
- Quên thêm testing tasks

---

## Kết Luận

Quy trình của Kiro là một cách tiếp cận có cấu trúc để phát triển phần mềm, kết hợp:

1. **Requirements Engineering:** Thu thập và phân tích yêu cầu
2. **Software Architecture:** Thiết kế kiến trúc và components
3. **Project Planning:** Chia nhỏ công việc thành tasks
4. **Quality Assurance:** Property-based testing và checkpoints

Quy trình này đảm bảo:
- ✅ Rõ ràng về mục tiêu
- ✅ Thiết kế đầy đủ trước khi code
- ✅ Kế hoạch triển khai chi tiết
- ✅ Chất lượng cao với testing toàn diện
- ✅ Tài liệu hóa đầy đủ cho bảo trì

---

## Tài Liệu Tham Khảo

### Về Requirements Engineering
- EARS (Easy Approach to Requirements Syntax)
- INCOSE (International Council on Systems Engineering) Guidelines
- IEEE 830 - Software Requirements Specification

### Về Software Design
- Clean Architecture (Robert C. Martin)
- Design Patterns (Gang of Four)
- Domain-Driven Design (Eric Evans)

### Về Property-Based Testing
- Hypothesis (Python library)
- QuickCheck (Haskell library - original PBT tool)
- "Property-Based Testing with PropEr, Erlang, and Elixir" (Fred Hebert)

### Về Software Development Processes
- Agile Manifesto
- Scrum Guide
- Waterfall Model
- V-Model
