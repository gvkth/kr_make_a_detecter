# Hướng Dẫn Tài Liệu Phần Mềm

## Giới Thiệu

Thư mục này chứa các tài liệu hướng dẫn chi tiết về các loại tài liệu phần mềm phổ biến trong Software Engineering. Mỗi file giải thích một khái niệm cụ thể với ví dụ thực tế từ dự án Gridex Risk Analysis.

## Danh Sách Tài Liệu

### 1. [SRS - Software Requirements Specification](./01_SRS_Software_Requirements_Specification.md)
**Đặc Tả Yêu Cầu Phần Mềm**

Tài liệu chính thức mô tả đầy đủ các yêu cầu chức năng và phi chức năng của hệ thống.

**Nội dung chính**:
- Định nghĩa và mục đích
- Cấu trúc theo IEEE 830
- So sánh với requirements.md của Kiro
- Khi nào nên dùng SRS
- Best practices

**Phù hợp cho**: Product Owners, Business Analysts, QA Engineers

---

### 2. [Use Case - Trường Hợp Sử Dụng](./02_Use_Case.md)
**Mô tả cách người dùng tương tác với hệ thống**

Kỹ thuật mô tả chi tiết các tương tác giữa người dùng (actor) và hệ thống để đạt được mục tiêu.

**Nội dung chính**:
- Thành phần của Use Case (Actor, Flows, Pre/Post conditions)
- Template Use Case chi tiết
- Use Case Diagram
- Relationships (Include, Extend, Generalization)
- So sánh Use Case vs User Story

**Phù hợp cho**: Business Analysts, System Analysts, Developers

---

### 3. [URD - User Requirements Document](./03_URD_User_Requirements_Document.md)
**Tài Liệu Yêu Cầu Người Dùng**

Tài liệu mô tả yêu cầu từ góc nhìn người dùng cuối, viết bằng ngôn ngữ nghiệp vụ.

**Nội dung chính**:
- Sự khác biệt URD vs SRS
- Cấu trúc URD (User Profiles, Goals, Scenarios)
- Ví dụ URD cho dự án Gridex
- Mapping URD → SRS → Design
- Quy trình tạo URD

**Phù hợp cho**: Product Owners, Business Analysts, Stakeholders

---

### 4. [User Story - Câu Chuyện Người Dùng](./04_User_Story.md)
**Mô tả ngắn gọn tính năng từ góc nhìn người dùng**

Format Agile phổ biến để mô tả yêu cầu một cách ngắn gọn và tập trung vào giá trị.

**Nội dung chính**:
- Format chuẩn: "Là một [role], tôi muốn [feature], để [benefit]"
- 3 C's: Card, Conversation, Confirmation
- Acceptance Criteria (Given-When-Then, EARS)
- INVEST Criteria (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- Story Points và Estimation
- Epic vs Story vs Task

**Phù hợp cho**: Product Owners, Scrum Masters, Agile Teams

---

### 5. [FLD - Functional Level Design](./05_FLD_Functional_Level_Design.md)
**Thiết Kế Mức Chức Năng**

Thiết kế mô tả các chức năng của hệ thống ở mức trung bình, nằm giữa HLD và LLD.

**Nội dung chính**:
- Vị trí trong quy trình thiết kế
- Module Description và Functional Decomposition
- Interface Specification
- Data Flow Diagrams
- Business Logic
- So sánh FLD vs HLD vs LLD

**Phù hợp cho**: Senior Developers, Technical Leads

---

### 6. [HLD - High-Level Design](./06_HLD_High_Level_Design.md)
**Thiết Kế Mức Cao**

Tài liệu mô tả kiến trúc tổng thể của hệ thống ở mức cao.

**Nội dung chính**:
- System Architecture (Architectural patterns)
- Technology Stack
- Component Interaction
- Data Architecture
- Deployment Architecture
- Security Architecture
- Non-Functional Requirements
- Architectural Patterns phổ biến (Layered, Microservices, Pipeline, etc.)

**Phù hợp cho**: Software Architects, Technical Leads, Senior Developers

---

### 7. [LLD - Low-Level Design](./07_LLD_Low_Level_Design.md)
**Thiết Kế Mức Thấp**

Thiết kế chi tiết nhất, mô tả cách implement từng component ở mức code.

**Nội dung chính**:
- Class Diagrams chi tiết
- Detailed Algorithms với Pseudocode
- Data Structures và Memory Layout
- Method Specifications với Complexity Analysis
- Error Handling Strategy
- Logging Strategy
- Flowcharts và Implementation details

**Phù hợp cho**: All Developers

---

## Mối Quan Hệ Giữa Các Tài Liệu

### Quy Trình Phát Triển Phần Mềm

```
┌─────────────────────────────────────────────────────────┐
│                  REQUIREMENTS PHASE                     │
├─────────────────────────────────────────────────────────┤
│  URD (User Requirements)                                │
│    ↓                                                    │
│  User Stories (Agile) / Use Cases (Waterfall)          │
│    ↓                                                    │
│  SRS (System Requirements Specification)                │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│                    DESIGN PHASE                         │
├─────────────────────────────────────────────────────────┤
│  HLD (High-Level Design)                                │
│    ↓                                                    │
│  FLD (Functional Level Design)                          │
│    ↓                                                    │
│  LLD (Low-Level Design)                                 │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│                 IMPLEMENTATION PHASE                    │
├─────────────────────────────────────────────────────────┤
│  Source Code                                            │
│  Unit Tests                                             │
│  Integration Tests                                      │
└─────────────────────────────────────────────────────────┘
```

### Mapping Với Quy Trình Kiro

| Giai Đoạn Kiro | Tài Liệu Tương Đương | Mô Tả |
|----------------|----------------------|-------|
| **requirements.md** | URD + User Stories + SRS | Kết hợp user requirements và system requirements |
| **design.md** | HLD + FLD + một phần LLD | Kiến trúc tổng thể + thiết kế chức năng + properties |
| **tasks.md** | Implementation Plan | Chia nhỏ design thành tasks cụ thể |

---

## So Sánh Nhanh

### Theo Mức Độ Chi Tiết

```
High-Level (Tổng Quan)
    ↓
URD - Yêu cầu người dùng
    ↓
User Story - Yêu cầu ngắn gọn
    ↓
Use Case - Tương tác chi tiết
    ↓
SRS - Đặc tả hệ thống
    ↓
HLD - Kiến trúc tổng thể
    ↓
FLD - Thiết kế chức năng
    ↓
LLD - Thiết kế code chi tiết
    ↓
Low-Level (Chi Tiết)
```

### Theo Người Đọc

| Tài Liệu | Người Đọc Chính |
|----------|-----------------|
| **URD** | Stakeholders, Business Users |
| **User Story** | Product Owner, Scrum Team |
| **Use Case** | Business Analysts, QA |
| **SRS** | All stakeholders, Developers, QA |
| **HLD** | Architects, Tech Leads, Managers |
| **FLD** | Senior Developers, Tech Leads |
| **LLD** | All Developers |

### Theo Phương Pháp Phát Triển

| Phương Pháp | Tài Liệu Thường Dùng |
|-------------|----------------------|
| **Waterfall** | SRS, Use Case, HLD, FLD, LLD (đầy đủ) |
| **Agile/Scrum** | User Story, HLD (nhẹ), LLD (khi cần) |
| **RUP** | Use Case, SRS, HLD, LLD |
| **Kiro Workflow** | requirements.md, design.md, tasks.md |

---

## Khi Nào Dùng Tài Liệu Nào?

### Dự Án Nhỏ (1-3 developers, < 3 tháng)
✅ **Cần**:
- User Stories
- HLD (ngắn gọn)
- Code comments

❌ **Không cần**:
- SRS chính thức
- FLD
- LLD chi tiết

### Dự Án Trung Bình (4-10 developers, 3-12 tháng)
✅ **Cần**:
- User Stories hoặc Use Cases
- SRS (đơn giản hóa)
- HLD
- LLD (cho phần phức tạp)

❌ **Không cần**:
- URD chính thức
- FLD (trừ khi hệ thống phức tạp)

### Dự Án Lớn (>10 developers, >12 tháng)
✅ **Cần tất cả**:
- URD
- Use Cases
- SRS
- HLD
- FLD
- LLD

### Dự Án Tuân Thủ Chuẩn (Compliance)
✅ **Bắt buộc**:
- SRS theo IEEE 830
- HLD và LLD đầy đủ
- Traceability matrix
- Review và approval chính thức

---

## Công Cụ Đề Xuất

### Viết Tài Liệu:
- **Markdown + Git**: Version control, dễ review
- **Confluence**: Wiki-based, collaboration
- **Google Docs**: Simple, real-time collaboration
- **Notion**: Modern, flexible

### Vẽ Sơ Đồ:
- **PlantUML**: Text-based, version control friendly
- **Draw.io**: Free, powerful
- **Lucidchart**: Professional, online
- **Mermaid**: Markdown-based diagrams

### Quản Lý Requirements:
- **Jira**: Agile, User Stories
- **Azure DevOps**: Microsoft ecosystem
- **IBM DOORS**: Enterprise requirements management

---

## Best Practices Chung

### 1. Chọn Tài Liệu Phù Hợp
- Không phải dự án nào cũng cần tất cả tài liệu
- Cân nhắc: quy mô, phương pháp, compliance

### 2. Giữ Tài Liệu Cập Nhật
- Tài liệu lỗi thời còn tệ hơn không có tài liệu
- Version control
- Regular reviews

### 3. Viết Cho Người Đọc
- URD: Ngôn ngữ người dùng
- SRS: Ngôn ngữ nghiệp vụ + kỹ thuật
- HLD: Kiến trúc, không quá chi tiết
- LLD: Chi tiết code, cho developers

### 4. Sử Dụng Sơ Đồ
- Một hình vẽ thay nghìn lời
- Architecture diagrams
- Data flow diagrams
- Class diagrams

### 5. Review và Approval
- Stakeholders review URD, SRS
- Architects review HLD
- Developers review LLD
- Formal sign-off cho dự án lớn

---

## Tài Liệu Tham Khảo

### Standards:
- IEEE 830: Software Requirements Specification
- IEEE 1016: Software Design Descriptions
- ISO/IEC/IEEE 29148: Requirements Engineering

### Books:
- "Software Requirements" - Karl Wiegers
- "Writing Effective Use Cases" - Alistair Cockburn
- "User Stories Applied" - Mike Cohn
- "Software Architecture in Practice" - Bass, Clements, Kazman
- "Clean Architecture" - Robert C. Martin

### Online Resources:
- [IEEE Computer Society](https://www.computer.org/)
- [INCOSE - International Council on Systems Engineering](https://www.incose.org/)
- [Agile Alliance](https://www.agilealliance.org/)

---

## Liên Hệ và Đóng Góp

Nếu bạn có câu hỏi hoặc muốn đóng góp cải thiện tài liệu này, vui lòng tạo issue hoặc pull request trên repository.

---

**Lưu ý**: Tất cả ví dụ trong các tài liệu đều dựa trên dự án thực tế "Gridex Risk Analysis" để dễ hiểu và áp dụng.
