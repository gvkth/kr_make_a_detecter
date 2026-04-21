# HLD - High-Level Design (Thiết Kế Mức Cao)

## Định Nghĩa

**HLD (High-Level Design)** là tài liệu mô tả kiến trúc tổng thể của hệ thống ở mức cao. HLD tập trung vào "big picture" - các thành phần chính, cách chúng tương tác, và công nghệ sử dụng.

## Mục Đích

- Cung cấp cái nhìn tổng quan về kiến trúc hệ thống
- Xác định các modules/components chính
- Định nghĩa giao tiếp giữa các components
- Chọn công nghệ và platform
- Làm cơ sở cho Low-Level Design

## Nội Dung HLD

### 1. System Architecture (Kiến Trúc Hệ Thống)
- Architectural pattern (MVC, Microservices, Layered, etc.)
- Major components/modules
- Component diagram

### 2. Technology Stack (Ngăn Xếp Công Nghệ)
- Programming languages
- Frameworks
- Databases
- Third-party services

### 3. Component Interaction (Tương Tác Giữa Components)
- How components communicate
- APIs, interfaces
- Data flow

### 4. Data Architecture (Kiến Trúc Dữ Liệu)
- Database schema (high-level)
- Data models
- Data storage strategy

### 5. Deployment Architecture (Kiến Trúc Triển Khai)
- Servers, cloud services
- Network topology
- Scalability strategy

### 6. Security Architecture (Kiến Trúc Bảo Mật)
- Authentication/Authorization
- Data encryption
- Security measures

### 7. Non-Functional Requirements (Yêu Cầu Phi Chức Năng)
- Performance targets
- Scalability
- Availability
- Maintainability

## Ví Dụ HLD Cho Dự Án Gridex

### 1. System Architecture

**Architectural Pattern**: Pipeline Architecture

**Lý do chọn**:
- Phù hợp với quy trình phân tích tuần tự
- Mỗi stage xử lý một khía cạnh
- Dễ mở rộng thêm analysis modules

**Architecture Diagram**:

```
┌─────────────────────────────────────────────────────────────┐
│                    Gridex Risk Analyzer                     │
│                                                             │
│  ┌──────────────────────────────────────────────────────┐  │
│  │           Risk Analyzer Core (Orchestrator)          │  │
│  └────────────────────┬─────────────────────────────────┘  │
│                       │                                     │
│         ┌─────────────┼─────────────┐                      │
│         │             │             │                      │
│         ▼             ▼             ▼                      │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                │
│  │  File    │  │  Config  │  │ Network  │                │
│  │ Scanner  │  │ Analyzer │  │ Monitor  │                │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘                │
│       │             │             │                        │
│       │             │             │                        │
│  ┌────┴─────┐  ┌────┴─────┐  ┌────┴─────┐                │
│  │ Update   │  │Permission│  │   Log    │                │
│  │ Analyzer │  │ Checker  │  │ Analyzer │                │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘                │
│       │             │             │                        │
│       └─────────────┼─────────────┘                        │
│                     ▼                                       │
│            ┌─────────────────┐                             │
│            │ Risk Aggregator │                             │
│            └────────┬─────────┘                            │
│                     ▼                                       │
│            ┌─────────────────┐                             │
│            │  Risk Scorer    │                             │
│            └────────┬─────────┘                            │
│                     ▼                                       │
│            ┌─────────────────┐                             │
│            │Report Generator │                             │
│            └─────────────────┘                             │
└─────────────────────────────────────────────────────────────┘
```

**Major Components**:

1. **Risk Analyzer Core**: Orchestrator điều phối toàn bộ quy trình
2. **Analysis Modules** (6 modules):
   - File Scanner: Quét files và metadata
   - Configuration Analyzer: Phân tích config files
   - Network Monitor: Phân tích network connections
   - Update Analyzer: Phân tích update mechanism
   - Permission Checker: Kiểm tra permissions
   - Log Analyzer: Phân tích log files
3. **Risk Aggregator**: Tổng hợp risks từ tất cả modules
4. **Risk Scorer**: Tính điểm và phân loại rủi ro
5. **Report Generator**: Tạo báo cáo Markdown

### 2. Technology Stack

**Programming Language**:
- **Python 3.8+**
  - Lý do: Rich ecosystem, easy to read, good for scripting

**Core Libraries**:
- `pathlib`: Modern path handling
- `hashlib`: SHA256 hashing
- `json`: JSON parsing
- `re`: Regex for pattern matching
- `dataclasses`: Data models
- `typing`: Type hints

**Testing**:
- `pytest`: Unit testing framework
- `hypothesis`: Property-based testing
- `pytest-cov`: Code coverage

**Optional Libraries**:
- `win32api`: Windows-specific operations
- `cryptography`: Digital signature verification

**Development Tools**:
- `black`: Code formatting
- `mypy`: Static type checking
- `pylint`: Linting

**Documentation**:
- `Markdown`: Documentation format
- `PlantUML`: Diagrams

### 3. Component Interaction

**Communication Pattern**: Direct method calls (monolithic)

**Data Flow**:
```
User Input (Path)
    ↓
Risk Analyzer Core
    ↓
[Parallel Execution]
    ├→ File Scanner → FileInfo[]
    ├→ Config Analyzer → SensitiveData[], Risks[]
    ├→ Network Monitor → NetworkConnection[], Risks[]
    ├→ Update Analyzer → UpdateInfo, Risks[]
    ├→ Permission Checker → PermissionInfo, Risks[]
    └→ Log Analyzer → LogEvent[], Anomaly[], Risks[]
    ↓
Risk Aggregator (Collect all risks)
    ↓
Risk Scorer (Calculate total score)
    ↓
Report Generator (Create Markdown report)
    ↓
Output: Report file
```

**Interface Style**: 
- Synchronous function calls
- Return values for data passing
- Exceptions for error handling

### 4. Data Architecture

**Data Storage**: In-memory only (no database)

**Lý do**: 
- Phân tích một lần, không cần persist
- Đơn giản, không cần database setup
- Kết quả lưu vào file Markdown

**Data Models** (High-Level):

```
AnalysisResult
├── FileInfo[]
├── NetworkConnection[]
├── Risk[]
│   ├── SecurityRisk[]
│   └── PrivacyRisk[]
├── UpdateInfo
├── PermissionInfo
└── LogEvent[]
```

**Data Flow Strategy**:
- Immutable data structures (dataclasses with frozen=True)
- Pass by value (copies) để tránh side effects
- Clear ownership (mỗi module owns data nó tạo ra)

### 5. Deployment Architecture

**Deployment Model**: Standalone CLI application

**Target Platform**: Windows 10/11

**Distribution**:
- Python package (pip install)
- Hoặc executable (.exe) dùng PyInstaller

**Deployment Diagram**:

```
┌─────────────────────────────────────┐
│      User's Windows Machine         │
│                                     │
│  ┌───────────────────────────────┐ │
│  │  Gridex Risk Analyzer CLI     │ │
│  │  (Python application)         │ │
│  └───────────┬───────────────────┘ │
│              │                      │
│              ▼                      │
│  ┌───────────────────────────────┐ │
│  │  File System                  │ │
│  │  - Read Gridex files          │ │
│  │  - Write report               │ │
│  └───────────────────────────────┘ │
│                                     │
│  ┌───────────────────────────────┐ │
│  │  Windows Registry (Read-only) │ │
│  └───────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Scalability**: Not applicable (single-user, local analysis)

**Performance Target**:
- Analyze 1000 files in < 30 seconds
- Memory usage < 500MB
- Report generation < 5 seconds

### 6. Security Architecture

**Security Principles**:

1. **Read-Only Operations**:
   - Chỉ đọc, không ghi hoặc sửa đổi files
   - Không thay đổi registry
   - Không thực thi code từ Gridex

2. **No Network Communication**:
   - Phân tích offline
   - Không gửi dữ liệu ra ngoài
   - Không download anything

3. **Least Privilege**:
   - Chạy với quyền user bình thường
   - Không yêu cầu admin rights
   - Chỉ truy cập Gridex folder

4. **Data Privacy**:
   - Sensitive data chỉ hiển thị preview (first/last 4 chars)
   - Không log sensitive data
   - Report lưu local, user control

**Threat Model**:
- **Threat**: Malicious Gridex software
- **Mitigation**: Read-only analysis, no execution
- **Threat**: Data leakage
- **Mitigation**: No network, local storage only

### 7. Non-Functional Requirements

**Performance**:
- File scanning: 1000 files in < 30 seconds
- Hash calculation: 100 MB/s throughput
- Report generation: < 5 seconds
- Memory usage: < 500MB

**Reliability**:
- Graceful degradation: Lỗi 1 module không crash toàn bộ
- Error recovery: Retry với exponential backoff
- Logging: Đầy đủ để debug

**Usability**:
- CLI đơn giản: 1 command để chạy
- Progress indicator: Hiển thị tiến độ
- Clear error messages: Dễ hiểu, actionable

**Maintainability**:
- Modular architecture: Dễ thêm/sửa modules
- Type hints: Đầy đủ type annotations
- Documentation: Docstrings cho tất cả public APIs
- Testing: >80% code coverage

**Portability**:
- Python 3.8+: Tương thích nhiều versions
- Windows 10/11: Target platform
- Minimal dependencies: Dễ install

## Architectural Patterns Phổ Biến

### 1. Layered Architecture (Kiến Trúc Phân Lớp)
```
┌─────────────────────┐
│ Presentation Layer  │ (UI)
├─────────────────────┤
│  Business Layer     │ (Logic)
├─────────────────────┤
│   Data Layer        │ (Database)
└─────────────────────┘
```
**Dùng khi**: Web apps, enterprise apps

### 2. Microservices Architecture
```
[Service 1] ←→ [API Gateway] ←→ [Service 2]
                    ↕
                [Service 3]
```
**Dùng khi**: Large-scale, distributed systems

### 3. Event-Driven Architecture
```
[Producer] → [Event Bus] → [Consumer 1]
                  ↓
              [Consumer 2]
```
**Dùng khi**: Real-time, async processing

### 4. Pipeline Architecture (Gridex dùng)
```
[Stage 1] → [Stage 2] → [Stage 3] → [Output]
```
**Dùng khi**: Sequential processing, data transformation

### 5. Client-Server Architecture
```
[Client] ←→ [Server] ←→ [Database]
```
**Dùng khi**: Web apps, mobile apps

## HLD vs LLD

| Khía Cạnh | HLD | LLD |
|-----------|-----|-----|
| **Mức độ** | Cao, tổng quan | Thấp, chi tiết |
| **Tập trung** | Kiến trúc, components | Algorithms, code |
| **Người viết** | Architect, Tech Lead | Senior/Mid developers |
| **Người đọc** | Stakeholders, managers, architects | Developers |
| **Sơ đồ** | Architecture, component diagrams | Flowcharts, pseudocode |
| **Chi tiết** | Modules, layers, tech stack | Classes, functions, data structures |
| **Ví dụ** | "Hệ thống dùng pipeline architecture với 10 modules" | "FileScanner.scan_directory() dùng os.walk() với depth-first traversal" |

## Best Practices

### 1. Chọn Kiến Trúc Phù Hợp
- Dựa trên requirements
- Xem xét scalability
- Đơn giản nhất có thể

### 2. Vẽ Sơ Đồ Rõ Ràng
- Component diagrams
- Deployment diagrams
- Data flow diagrams

### 3. Justify Decisions
- Giải thích tại sao chọn tech stack
- Trade-offs
- Alternatives considered

### 4. Xem Xét Non-Functional Requirements
- Performance
- Security
- Scalability
- Maintainability

### 5. Review Với Team
- Architects review
- Developers review
- Stakeholders approve

## Template HLD

```markdown
# High-Level Design: [Project Name]

## 1. System Overview
- Purpose
- Scope
- Key features

## 2. System Architecture
- Architectural pattern
- Component diagram
- Justification

## 3. Technology Stack
- Languages
- Frameworks
- Databases
- Third-party services
- Justification for each

## 4. Component Description
### Component 1
- Purpose
- Responsibilities
- Interfaces

### Component 2
...

## 5. Component Interaction
- Communication patterns
- Data flow
- Sequence diagrams

## 6. Data Architecture
- Data models (high-level)
- Storage strategy
- ER diagram (if applicable)

## 7. Deployment Architecture
- Deployment model
- Infrastructure
- Deployment diagram

## 8. Security Architecture
- Authentication/Authorization
- Data protection
- Security measures

## 9. Non-Functional Requirements
- Performance targets
- Scalability strategy
- Availability requirements
- Maintainability considerations

## 10. Risks and Mitigations
- Technical risks
- Mitigation strategies

## 11. Alternatives Considered
- Other architectures considered
- Why not chosen
```

## Công Cụ Tạo HLD

### Diagrams:
- **Lucidchart**: Online, collaborative
- **Draw.io**: Free, powerful
- **Microsoft Visio**: Professional
- **PlantUML**: Text-based, version control
- **Mermaid**: Markdown-based diagrams

### Documentation:
- **Confluence**: Wiki-based
- **Notion**: Modern, flexible
- **Google Docs**: Simple, collaborative
- **Markdown + Git**: Version control friendly

## Tài Liệu Tham Khảo

- "Software Architecture in Practice" - Bass, Clements, Kazman
- "Designing Data-Intensive Applications" - Martin Kleppmann
- "Clean Architecture" - Robert C. Martin
- "Building Microservices" - Sam Newman
- IEEE 1471: Architecture Description Standard
