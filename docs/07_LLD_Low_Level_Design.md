# LLD - Low-Level Design (Thiết Kế Mức Thấp)

## Định Nghĩa

**LLD (Low-Level Design)** là tài liệu thiết kế chi tiết nhất, mô tả cách implement từng component/module ở mức code. LLD bao gồm algorithms, data structures, class diagrams, và pseudocode.

## Mục Đích

- Cung cấp blueprint chi tiết cho developers
- Mô tả algorithms và logic xử lý
- Định nghĩa classes, methods, data structures
- Làm cơ sở trực tiếp cho coding

## Nội Dung LLD

### 1. Class Diagrams (Sơ Đồ Lớp)
- Classes và relationships
- Attributes và methods
- Inheritance, composition

### 2. Detailed Algorithms (Thuật Toán Chi Tiết)
- Pseudocode
- Flowcharts
- Step-by-step logic

### 3. Data Structures (Cấu Trúc Dữ Liệu)
- Internal data structures
- Data types
- Memory layout

### 4. Method Specifications (Đặc Tả Phương Thức)
- Input parameters với types
- Return values với types
- Exceptions
- Complexity analysis

### 5. Database Schema (Lược Đồ Cơ Sở Dữ Liệu)
- Tables, columns, types
- Indexes
- Constraints
- Relationships

### 6. Error Handling (Xử Lý Lỗi)
- Exception types
- Error recovery
- Logging strategy

## Ví Dụ LLD Cho Module FileScanner

### 1. Class Diagram

```
┌─────────────────────────────────────────┐
│           FileScanner                   │
├─────────────────────────────────────────┤
│ - _installation_path: str               │
│ - _file_list: List[FileInfo]            │
├─────────────────────────────────────────┤
│ + __init__(path: str)                   │
│ + scan_directory() -> List[FileInfo]   │
│ + calculate_hash(path: str) -> str     │
│ + check_signature(path: str) -> Info   │
│ - _collect_metadata(path: str) -> Info │
│ - _is_executable(path: str) -> bool    │
│ - _is_hidden(path: str) -> bool        │
└─────────────────────────────────────────┘
                  │
                  │ uses
                  ▼
┌─────────────────────────────────────────┐
│           FileInfo                      │
├─────────────────────────────────────────┤
│ + path: str                             │
│ + size: int                             │
│ + created_date: datetime                │
│ + modified_date: datetime               │
│ + file_type: str                        │
│ + is_hidden: bool                       │
│ + is_executable: bool                   │
│ + hash_sha256: Optional[str]            │
│ + signature_info: Optional[SignatureInfo]│
└─────────────────────────────────────────┘
                  │
                  │ has
                  ▼
┌─────────────────────────────────────────┐
│         SignatureInfo                   │
├─────────────────────────────────────────┤
│ + is_signed: bool                       │
│ + signer: Optional[str]                 │
│ + is_valid: bool                        │
│ + timestamp: Optional[datetime]         │
└─────────────────────────────────────────┘
```

### 2. Detailed Method Specifications

#### Method: scan_directory()

**Signature**:
```python
def scan_directory(self) -> List[FileInfo]:
```

**Purpose**: Quét đệ quy thư mục và thu thập thông tin tất cả files

**Algorithm** (Pseudocode):
```
FUNCTION scan_directory():
    file_list = empty list
    
    FOR each (dirpath, dirnames, filenames) in os.walk(installation_path):
        FOR each filename in filenames:
            full_path = join(dirpath, filename)
            
            TRY:
                file_info = _collect_metadata(full_path)
                
                IF _is_executable(full_path):
                    file_info.hash_sha256 = calculate_hash(full_path)
                    file_info.signature_info = check_signature(full_path)
                
                file_list.append(file_info)
                
            CATCH PermissionError:
                LOG warning "Cannot access: {full_path}"
                CONTINUE
                
            CATCH Exception as e:
                LOG error "Error processing {full_path}: {e}"
                CONTINUE
    
    RETURN file_list
```

**Flowchart**:
```
[Start]
   ↓
[Initialize file_list = []]
   ↓
[os.walk(path)]
   ↓
[For each file] ──No──→ [Return file_list]
   ↓ Yes
[Collect metadata]
   ↓
[Is executable?] ──No──→ [Add to file_list]
   ↓ Yes                      ↓
[Calculate hash]              ↓
   ↓                          ↓
[Check signature]             ↓
   ↓                          ↓
[Add to file_list] ←──────────┘
   ↓
[Loop back]
```

**Time Complexity**: O(n) where n = number of files
**Space Complexity**: O(n) for storing file list

**Error Handling**:
- `PermissionError`: Log warning, skip file, continue
- `FileNotFoundError`: Log error, skip file, continue
- `IOError`: Log error, skip file, continue

---

#### Method: calculate_hash()

**Signature**:
```python
def calculate_hash(self, file_path: str) -> str:
```

**Purpose**: Tính SHA256 hash của file

**Algorithm** (Pseudocode):
```
FUNCTION calculate_hash(file_path):
    CHUNK_SIZE = 8192  # 8KB chunks
    hasher = hashlib.sha256()
    
    TRY:
        WITH open(file_path, 'rb') as file:
            WHILE True:
                chunk = file.read(CHUNK_SIZE)
                IF chunk is empty:
                    BREAK
                hasher.update(chunk)
        
        RETURN hasher.hexdigest()
        
    CATCH FileNotFoundError:
        RAISE FileNotFoundError(f"File not found: {file_path}")
        
    CATCH IOError as e:
        RAISE IOError(f"Cannot read file: {file_path}, {e}")
```

**Detailed Implementation**:
```python
def calculate_hash(self, file_path: str) -> str:
    """
    Calculate SHA256 hash of a file.
    
    Uses chunked reading to handle large files efficiently.
    
    Args:
        file_path: Absolute path to file
        
    Returns:
        Hex string of SHA256 hash (64 characters)
        
    Raises:
        FileNotFoundError: If file doesn't exist
        IOError: If file cannot be read
        
    Time Complexity: O(n) where n = file size
    Space Complexity: O(1) - constant memory usage
    
    Example:
        >>> scanner = FileScanner("C:/Gridex")
        >>> hash_val = scanner.calculate_hash("C:/Gridex/app.exe")
        >>> print(hash_val)
        'a3b2c1d4e5f6...'  # 64 char hex string
    """
    CHUNK_SIZE = 8192  # 8KB - optimal for most systems
    hasher = hashlib.sha256()
    
    try:
        with open(file_path, 'rb') as file:
            while True:
                chunk = file.read(CHUNK_SIZE)
                if not chunk:
                    break
                hasher.update(chunk)
        
        return hasher.hexdigest()
        
    except FileNotFoundError:
        raise FileNotFoundError(f"File not found: {file_path}")
        
    except IOError as e:
        raise IOError(f"Cannot read file: {file_path}, Error: {e}")
```

**Performance Analysis**:
- **Chunk size**: 8KB chosen for balance between memory and I/O
- **Throughput**: ~100 MB/s on typical HDD
- **Memory**: Constant O(1) - only 8KB buffer
- **Optimization**: Could use mmap for very large files

---

#### Method: _collect_metadata()

**Signature**:
```python
def _collect_metadata(self, file_path: str) -> FileInfo:
```

**Purpose**: Thu thập metadata của một file

**Algorithm** (Pseudocode):
```
FUNCTION _collect_metadata(file_path):
    stat_info = os.stat(file_path)
    
    file_info = FileInfo(
        path = file_path,
        size = stat_info.st_size,
        created_date = datetime.fromtimestamp(stat_info.st_ctime),
        modified_date = datetime.fromtimestamp(stat_info.st_mtime),
        file_type = _determine_file_type(file_path),
        is_hidden = _is_hidden(file_path),
        is_executable = _is_executable(file_path),
        hash_sha256 = None,  # Will be filled later if executable
        signature_info = None  # Will be filled later if executable
    )
    
    RETURN file_info
```

**Implementation**:
```python
def _collect_metadata(self, file_path: str) -> FileInfo:
    """
    Collect metadata for a single file.
    
    Args:
        file_path: Absolute path to file
        
    Returns:
        FileInfo object with metadata
        
    Raises:
        OSError: If file cannot be accessed
    """
    stat_info = os.stat(file_path)
    
    return FileInfo(
        path=file_path,
        size=stat_info.st_size,
        created_date=datetime.fromtimestamp(stat_info.st_ctime),
        modified_date=datetime.fromtimestamp(stat_info.st_mtime),
        file_type=self._determine_file_type(file_path),
        is_hidden=self._is_hidden(file_path),
        is_executable=self._is_executable(file_path),
        hash_sha256=None,
        signature_info=None
    )
```

---

### 3. Data Structures

#### FileInfo Dataclass

```python
from dataclasses import dataclass
from datetime import datetime
from typing import Optional

@dataclass(frozen=True)
class FileInfo:
    """
    Immutable data structure containing file metadata.
    
    Attributes:
        path: Absolute file path
        size: File size in bytes
        created_date: File creation timestamp
        modified_date: Last modification timestamp
        file_type: File type/extension (e.g., 'exe', 'dll', 'json')
        is_hidden: Whether file has hidden attribute
        is_executable: Whether file is executable (.exe, .dll, .bat)
        hash_sha256: SHA256 hash (only for executables)
        signature_info: Digital signature info (only for executables)
    
    Example:
        >>> file_info = FileInfo(
        ...     path="C:/Gridex/app.exe",
        ...     size=1024000,
        ...     created_date=datetime.now(),
        ...     modified_date=datetime.now(),
        ...     file_type="exe",
        ...     is_hidden=False,
        ...     is_executable=True,
        ...     hash_sha256="a3b2c1...",
        ...     signature_info=SignatureInfo(...)
        ... )
    """
    path: str
    size: int
    created_date: datetime
    modified_date: datetime
    file_type: str
    is_hidden: bool
    is_executable: bool
    hash_sha256: Optional[str] = None
    signature_info: Optional['SignatureInfo'] = None
    
    def __post_init__(self):
        """Validate data after initialization."""
        if self.size < 0:
            raise ValueError("File size cannot be negative")
        if not self.path:
            raise ValueError("File path cannot be empty")
```

**Memory Layout**:
```
FileInfo object size: ~200 bytes
- path: 8 bytes (pointer) + string length
- size: 8 bytes (int64)
- created_date: 24 bytes (datetime object)
- modified_date: 24 bytes (datetime object)
- file_type: 8 bytes (pointer) + string length
- is_hidden: 1 byte (bool)
- is_executable: 1 byte (bool)
- hash_sha256: 8 bytes (pointer) + 64 bytes (if present)
- signature_info: 8 bytes (pointer) + SignatureInfo size (if present)
```

---

### 4. Algorithm Analysis

#### Suspicious File Detection Algorithm

**Purpose**: Phát hiện files đáng ngờ dựa trên patterns

**Algorithm**:
```
FUNCTION detect_suspicious_files(file_list):
    suspicious_files = empty list
    
    FOR each file in file_list:
        risk_level = "None"
        reasons = empty list
        
        # Check 1: Random hex filename
        IF filename matches pattern ^[0-9a-fA-F]{16,}$ :
            risk_level = "High"
            reasons.append("Random hex filename")
        
        # Check 2: Double extension
        IF filename matches pattern \.(pdf|doc|jpg|txt)\.(exe|bat|cmd)$ :
            risk_level = "High"
            reasons.append("Double extension (disguised executable)")
        
        # Check 3: System-like name in wrong location
        system_names = ["svchost.exe", "explorer.exe", "csrss.exe"]
        IF filename in system_names AND path not in "C:\Windows\System32":
            risk_level = "High"
            reasons.append("System-like name in wrong location")
        
        # Check 4: Hidden executable
        IF file.is_hidden AND file.is_executable:
            risk_level = "Critical"
            reasons.append("Hidden executable")
        
        # Check 5: Unsigned executable
        IF file.is_executable AND NOT file.signature_info.is_signed:
            risk_level = "High"
            reasons.append("Unsigned executable")
        
        IF risk_level != "None":
            suspicious_files.append(
                SecurityRisk(
                    file=file,
                    level=risk_level,
                    reasons=reasons
                )
            )
    
    RETURN suspicious_files
```

**Regex Patterns**:
```python
RANDOM_HEX_PATTERN = re.compile(r'^[0-9a-fA-F]{16,}$')
DOUBLE_EXTENSION_PATTERN = re.compile(r'\.(pdf|doc|jpg|txt)\.(exe|bat|cmd)$', re.IGNORECASE)
SYSTEM_NAMES = {'svchost.exe', 'explorer.exe', 'csrss.exe', 'lsass.exe', 'winlogon.exe'}
SYSTEM_PATH = r'C:\Windows\System32'
```

**Time Complexity**: O(n × m) where:
- n = number of files
- m = average number of checks per file (constant, ~5)
- Overall: O(n)

**Space Complexity**: O(k) where k = number of suspicious files found

---

### 5. Error Handling Strategy

#### Exception Hierarchy

```
Exception
├── FileSystemError (custom)
│   ├── PathNotFoundError
│   ├── AccessDeniedError
│   └── FileReadError
├── AnalysisError (custom)
│   ├── HashCalculationError
│   └── SignatureVerificationError
└── ConfigurationError (custom)
    └── InvalidPathError
```

#### Error Handling Code

```python
class FileSystemError(Exception):
    """Base exception for file system operations."""
    pass

class AccessDeniedError(FileSystemError):
    """Raised when file access is denied."""
    def __init__(self, file_path: str):
        self.file_path = file_path
        super().__init__(f"Access denied: {file_path}")

# Usage in FileScanner
def scan_directory(self) -> List[FileInfo]:
    file_list = []
    
    for dirpath, dirnames, filenames in os.walk(self._installation_path):
        for filename in filenames:
            full_path = os.path.join(dirpath, filename)
            
            try:
                file_info = self._collect_metadata(full_path)
                file_list.append(file_info)
                
            except PermissionError:
                logger.warning(f"Access denied: {full_path}")
                # Continue with next file - graceful degradation
                continue
                
            except OSError as e:
                logger.error(f"OS error processing {full_path}: {e}")
                # Continue with next file
                continue
                
            except Exception as e:
                logger.error(f"Unexpected error processing {full_path}: {e}")
                # Continue with next file
                continue
    
    return file_list
```

---

### 6. Logging Strategy

```python
import logging

# Configure logging
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('gridex_analyzer.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger('FileScanner')

# Usage
logger.info(f"Starting scan of {self._installation_path}")
logger.debug(f"Processing file: {file_path}")
logger.warning(f"Access denied: {file_path}")
logger.error(f"Failed to calculate hash: {file_path}")
logger.critical(f"Critical error: System cannot continue")
```

---

## LLD vs HLD vs FLD

| Khía Cạnh | HLD | FLD | LLD |
|-----------|-----|-----|-----|
| **Mức độ** | Cao | Trung | Thấp |
| **Chi tiết** | Modules | Functions | Code |
| **Sơ đồ** | Architecture | Data flow | Class, flowchart |
| **Nội dung** | Components, tech stack | Interfaces, logic | Algorithms, data structures |
| **Ví dụ** | "Pipeline architecture" | "FileScanner has scan_directory()" | "scan_directory() uses os.walk() with try-catch" |

---

## Best Practices

### 1. Viết Pseudocode Trước Code
- Giúp suy nghĩ logic
- Dễ review
- Language-agnostic

### 2. Phân Tích Complexity
- Time complexity
- Space complexity
- Optimization opportunities

### 3. Document Edge Cases
- Empty inputs
- Null values
- Boundary conditions

### 4. Specify Error Handling
- Exception types
- Recovery strategies
- Logging

### 5. Include Examples
- Input/output examples
- Usage examples
- Test cases

---

## Template LLD

```markdown
# Low-Level Design: [Module Name]

## 1. Class Diagram
- UML class diagram
- Relationships

## 2. Class Specifications

### Class: [ClassName]

#### Attributes
- attribute1: type - description
- attribute2: type - description

#### Methods

##### Method: method_name()
- **Signature**: `def method_name(param: type) -> return_type:`
- **Purpose**: What it does
- **Algorithm**: Pseudocode
- **Flowchart**: Visual representation
- **Time Complexity**: O(?)
- **Space Complexity**: O(?)
- **Error Handling**: Exceptions
- **Example**: Usage example

## 3. Data Structures
- Internal data structures
- Memory layout
- Justification

## 4. Algorithms
- Detailed algorithms
- Pseudocode
- Complexity analysis

## 5. Error Handling
- Exception hierarchy
- Error recovery
- Logging

## 6. Testing Strategy
- Unit test cases
- Edge cases
- Mock objects
```

---

## Công Cụ Tạo LLD

### Diagrams:
- **PlantUML**: Class diagrams, sequence diagrams
- **Draw.io**: Flowcharts
- **Lucidchart**: Professional diagrams

### Documentation:
- **Markdown**: Simple, version control
- **Doxygen**: Auto-generate from code comments
- **Sphinx**: Python documentation

---

## Tài Liệu Tham Khảo

- "Introduction to Algorithms" - CLRS
- "Design Patterns" - Gang of Four
- "Clean Code" - Robert C. Martin
- "Effective Python" - Brett Slatkin
