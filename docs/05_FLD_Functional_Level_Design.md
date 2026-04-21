# FLD - Functional Level Design (Thiết Kế Mức Chức Năng)

## Định Nghĩa

**FLD (Functional Level Design)** là tài liệu thiết kế mô tả các chức năng của hệ thống ở mức trung bình (mid-level). FLD nằm giữa High-Level Design (kiến trúc tổng thể) và Low-Level Design (chi tiết code).

## Vị Trí Trong Quy Trình Thiết Kế

```
Requirements (Yêu cầu)
         ↓
High-Level Design (HLD) - Kiến trúc tổng thể
         ↓
Functional Level Design (FLD) - Thiết kế chức năng
         ↓
Low-Level Design (LLD) - Thiết kế chi tiết code
         ↓
Implementation (Triển khai)
```

## Mục Đích

- Mô tả chi tiết từng chức năng/module
- Định nghĩa interfaces giữa các modules
- Mô tả data flow trong hệ thống
- Làm cầu nối giữa HLD và LLD

## Nội Dung FLD

### 1. Module Description (Mô Tả Module)
- Tên module
- Mục đích/trách nhiệm
- Chức năng chính

### 2. Functional Decomposition (Phân Rã Chức Năng)
- Chia module thành các functions nhỏ hơn
- Mô tả từng function

### 3. Interface Specification (Đặc Tả Giao Diện)
- Input parameters
- Output/Return values
- Exceptions/Errors

### 4. Data Flow Diagrams (Sơ Đồ Luồng Dữ Liệu)
- Dữ liệu đi từ đâu đến đâu
- Transformations

### 5. Business Logic (Logic Nghiệp Vụ)
- Quy tắc xử lý
- Điều kiện
- Validations

### 6. Dependencies (Phụ Thuộc)
- Module phụ thuộc vào modules nào
- External libraries

## Ví Dụ FLD Cho Dự Án Gridex

### Module: File Scanner

#### 1. Module Description

**Tên**: FileScanner

**Mục đích**: Quét cấu trúc thư mục Gridex và thu thập thông tin về tất cả files.

**Trách nhiệm**:
- Duyệt đệ quy tất cả thư mục con
- Thu thập metadata của mỗi file
- Xác định loại file
- Tính hash cho executables
- Kiểm tra digital signature
- Phát hiện files đáng ngờ

#### 2. Functional Decomposition

**Function 1: scan_directory()**
- **Mục đích**: Quét thư mục đệ quy
- **Input**: path (string)
- **Output**: List[FileInfo]
- **Logic**: 
  - Sử dụng os.walk() để duyệt đệ quy
  - Với mỗi file, gọi collect_metadata()
  - Lọc bỏ system files nếu cần

**Function 2: collect_metadata()**
- **Mục đích**: Thu thập metadata của 1 file
- **Input**: file_path (string)
- **Output**: FileInfo object
- **Logic**:
  - Lấy size từ os.path.getsize()
  - Lấy dates từ os.path.getctime(), getmtime()
  - Xác định type từ extension
  - Check hidden attribute

**Function 3: calculate_hash()**
- **Mục đích**: Tính SHA256 hash
- **Input**: file_path (string)
- **Output**: hash_string (string)
- **Logic**:
  - Đọc file theo chunks (để xử lý files lớn)
  - Dùng hashlib.sha256()
  - Return hex digest

**Function 4: check_digital_signature()**
- **Mục đích**: Kiểm tra chữ ký số của executable
- **Input**: file_path (string)
- **Output**: SignatureInfo object
- **Logic**:
  - Dùng Windows API hoặc library
  - Extract signer information
  - Verify signature validity

**Function 5: detect_suspicious_files()**
- **Mục đích**: Phát hiện files đáng ngờ
- **Input**: List[FileInfo]
- **Output**: List[SecurityRisk]
- **Logic**:
  - Check random hex filenames (>16 chars)
  - Check double extensions (.pdf.exe)
  - Check system-like names in wrong locations
  - Check hidden executables

#### 3. Interface Specification

```python
class FileScanner:
    """
    Scanner for analyzing file structure and metadata.
    """
    
    def scan_directory(self, path: str) -> List[FileInfo]:
        """
        Scan directory recursively and collect file information.
        
        Args:
            path: Root directory path to scan
            
        Returns:
            List of FileInfo objects containing metadata
            
        Raises:
            FileNotFoundError: If path doesn't exist
            PermissionError: If no read permission
            
        Example:
            scanner = FileScanner()
            files = scanner.scan_directory("C:/Users/Admin/AppData/Local/Gridex")
        """
        pass
    
    def calculate_hash(self, file_path: str) -> str:
        """
        Calculate SHA256 hash of a file.
        
        Args:
            file_path: Path to file
            
        Returns:
            Hex string of SHA256 hash
            
        Raises:
            FileNotFoundError: If file doesn't exist
            IOError: If file cannot be read
            
        Performance:
            Reads file in 8KB chunks for memory efficiency
        """
        pass
    
    def check_digital_signature(self, file_path: str) -> SignatureInfo:
        """
        Check digital signature of executable file.
        
        Args:
            file_path: Path to executable file
            
        Returns:
            SignatureInfo with is_signed, signer, is_valid, timestamp
            
        Raises:
            ValueError: If file is not an executable
            
        Platform:
            Windows only
        """
        pass
```

#### 4. Data Flow Diagram

```
[User Input: Path]
       ↓
[scan_directory()]
       ↓
[os.walk() - Traverse directories]
       ↓
[For each file] → [collect_metadata()]
       ↓                    ↓
       ↓              [os.path functions]
       ↓                    ↓
       ↓              [FileInfo object]
       ↓                    ↓
[If executable] → [calculate_hash()]
       ↓                    ↓
       ↓              [hashlib.sha256]
       ↓                    ↓
       ↓         [check_digital_signature()]
       ↓                    ↓
       ↓              [Windows API]
       ↓                    ↓
[List[FileInfo]] → [detect_suspicious_files()]
       ↓                    ↓
       ↓              [Pattern matching]
       ↓                    ↓
[Return: Files + Risks]
```

#### 5. Business Logic

**Logic 1: Xác định file đáng ngờ**
```
IF filename matches hex pattern AND length > 16 chars:
    Flag as suspicious (random name)
    
IF filename has double extension (.pdf.exe, .doc.exe):
    Flag as suspicious (disguised executable)
    
IF filename is system-like (svchost.exe, explorer.exe) 
   AND location is not C:\Windows\System32:
    Flag as suspicious (fake system file)
    
IF file is hidden AND is executable:
    Flag as critical risk (hidden malware)
```

**Logic 2: Tính hash có điều kiện**
```
IF file is executable (.exe, .dll, .bat):
    Calculate hash
ELSE:
    Skip hash calculation (performance)
```

**Logic 3: Xử lý lỗi đọc file**
```
TRY:
    Read and process file
CATCH PermissionError:
    Log warning
    Mark as "Access Denied"
    Continue with next file
CATCH IOError:
    Log error
    Skip file
    Continue with next file
```

#### 6. Dependencies

**Internal Dependencies**:
- `FileInfo` dataclass (from data_models module)
- `SignatureInfo` dataclass (from data_models module)
- `SecurityRisk` class (from risk_models module)

**External Dependencies**:
- `os`: File system operations
- `os.path`: Path manipulations
- `hashlib`: SHA256 hashing
- `pathlib`: Modern path handling
- `win32api` (optional): Windows-specific operations
- `cryptography` (optional): Signature verification

**Platform Requirements**:
- Windows 10/11 for full functionality
- Python 3.8+

## FLD vs HLD vs LLD

| Khía Cạnh | HLD | FLD | LLD |
|-----------|-----|-----|-----|
| **Mức độ** | Cao | Trung | Thấp |
| **Tập trung** | Kiến trúc | Chức năng | Code |
| **Chi tiết** | Modules, layers | Functions, interfaces | Algorithms, data structures |
| **Sơ đồ** | Architecture diagram | Data flow diagram | Flowcharts, pseudocode |
| **Người đọc** | Architects, managers | Senior developers | All developers |
| **Ví dụ** | "Hệ thống có 10 modules" | "FileScanner có 5 functions" | "scan_directory() dùng os.walk()" |

## Khi Nào Cần FLD?

✅ **Nên có FLD khi:**
- Dự án trung bình đến lớn
- Nhiều developers cùng làm việc
- Cần tài liệu chi tiết cho implementation
- Hệ thống phức tạp với nhiều modules

❌ **Không cần FLD khi:**
- Dự án nhỏ (< 5 modules)
- Team nhỏ (1-2 developers)
- Prototype/MVP nhanh
- Agile team với communication tốt

## Best Practices

### 1. Tập Trung Vào Chức Năng
- Mô tả "cái gì" module làm
- Không đi sâu vào "như thế nào" implement

### 2. Định Nghĩa Rõ Interfaces
- Input/Output rõ ràng
- Data types cụ thể
- Error handling

### 3. Vẽ Sơ Đồ
- Data flow diagrams
- Sequence diagrams
- State diagrams (nếu cần)

### 4. Mô Tả Business Logic
- Quy tắc xử lý
- Điều kiện
- Edge cases

### 5. Document Dependencies
- Internal dependencies
- External libraries
- Platform requirements

## Template FLD

```markdown
# Module: [Tên Module]

## 1. Overview
- Purpose
- Responsibilities
- Key Features

## 2. Functional Decomposition
### Function 1: [Tên]
- Purpose
- Input
- Output
- Logic

### Function 2: [Tên]
...

## 3. Interface Specification
- Function signatures
- Parameters
- Return values
- Exceptions

## 4. Data Flow
- Diagram
- Description

## 5. Business Logic
- Rules
- Validations
- Conditions

## 6. Dependencies
- Internal
- External
- Platform

## 7. Error Handling
- Error scenarios
- Recovery strategies

## 8. Performance Considerations
- Time complexity
- Space complexity
- Optimization notes
```

## Công Cụ Tạo FLD

### Documentation:
- **Confluence**: Wiki-based
- **Notion**: Modern, flexible
- **Google Docs**: Simple, collaborative
- **Markdown**: Version control friendly

### Diagrams:
- **Lucidchart**: Online, easy
- **Draw.io**: Free, powerful
- **Microsoft Visio**: Professional
- **PlantUML**: Text-based, code-friendly

## Tài Liệu Tham Khảo

- "Software Architecture in Practice" - Bass, Clements, Kazman
- "Design Patterns" - Gang of Four
- IEEE 1016: Software Design Descriptions
