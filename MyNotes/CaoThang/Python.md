# Python

## Trình biên dịch (Compiler) vs. Trình thông dịch (Interpreter)

| **Tiêu chí**  | **Trình biên dịch (C++, Go, Rust)**                                                               | **Trình thông dịch (Python, PHP, JS)**                                                          |
| ------------- | ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Cơ chế**    | Dịch **toàn bộ** mã nguồn (Source Code) ra mã máy (Machine Code) một lần duy nhất trước khi chạy. | Dịch từng lệnh (hoặc khối lệnh), chuyển thành mã máy và **thực thi ngay lập tức** theo tuần tự. |
| **Đầu ra**    | Tạo ra một file thực thi độc lập (`.exe` trên Windows hoặc binary trên Linux).                    | Không tạo file thực thi độc lập. Cần có môi trường (Python runtime) để chạy file nguồn `.py`.   |
| **Thời gian** | Tốn thời gian chờ biên dịch (Compile time) lâu, nhưng chạy (Run time) cực nhanh.                  | Không tốn thời gian biên dịch (chạy ngay), nhưng tốc độ thực thi chậm hơn.                      |
| **Báo lỗi**   | Quét toàn bộ code, báo tất cả lỗi cú pháp **trước khi** chạy chương trình.                        | Chạy đến dòng nào lỗi thì báo ở dòng đó. (Dòng 1 đúng vẫn chạy, đến dòng 2 lỗi mới dừng).       |
| **Bảo mật**   | Mã nguồn được giấu kín (người dùng chỉ nhận được file `.exe`).                                    | Mã nguồn công khai (thường phải giao file `.py` cho người dùng hoặc server).                    |

## Mô hình hoạt động của Python (Thực tế nó là lai (Hybrid)!)

```mermaid
graph LR
    A[SourceCode.py] -->|Compiler| B[Bytecode.pyc]
    B -->|Input| C[Python Virtual Machine]
    C -->|Interprets| D[Machine Code]
    D -->|Executes| E[CPU / Hardware]
```

## Các kiểu reverse

| **Phương pháp** | **Cú pháp**          | **Time Complexity**  | **Space Complexity**     | **Kiểu trả về**        |
| --------------- | -------------------- | -------------------- | ------------------------ | ---------------------- |
| **Slicing**     | `new_list = a[::-1]` | $O(N)$               | $O(N)$ (Tạo bản sao)     | `list`                 |
| **Iterator**    | `it = reversed(a)`   | $O(1)$ (lúc gọi hàm) | $O(1)$ (Chỉ lưu con trỏ) | `list_reverseiterator` |
| **In-place**    | `a.reverse()`        | $O(N)$               | $O(1)$ (Đổi chỗ tại chỗ) | `None`                 |

## Dictionary & The "Collections" Power

Trong Python, `dict` là **Hash Map** (O(1)) nhưng từ Python 3.7+, nó **giữ nguyên thứ tự chèn** (Insertion Order).

### 1. Dictionary Comprehension

Giống List Comprehension, nhưng dùng ngoặc nhọn `{}` và cú pháp `key: value`.

**Bài toán:** Bạn có list tên `names = ["An", "Binh", "Cuong"]`. Bạn muốn tạo dict để tra cứu độ dài tên: `{'An': 2, 'Binh': 4, ...}`.

```python
# {key: value for item in list}
d = {name: len(name) for name in names}
```

```python
original = {'a': 1, 'b': 2, 'c': 3}
# k, v là unpacking tuple
inverted = {v: k for k, v in original.items()}
print(inverted)
```

### 2. Truy cập an toàn (`.get()`)

Trong Python, `d["key_khong_ton_tai"]` sẽ ném lỗi **KeyError** làm crash chương trình. Vậy nên chúng ta sẽ sử dụng method `.get()` để tránh việc đó.

```python
# d.get(key, default_value)
print(user_data.get("age", 0))
```

### 3. Module `collections`

#### A. `Counter` (Đếm tần suất)

```python
from collections import Counter
s = "hello world"
count = Counter(s)
# Output: Counter({'l': 3, 'o': 2, 'h': 1, ...})

# Tính năng bá đạo: Lấy 3 phần tử xuất hiện nhiều nhất
print(count.most_common(3))
```

#### B. `defaultdict` (Dictionary mặc định)

Khắc phục sự phiền toái khi phải kiểm tra "key đã tồn tại chưa" trước khi append vào list.

**Bài toán:** Gom nhóm các file theo đuôi mở rộng. List file: `['img.png', 'doc.txt', 'pic.png']`. Mong muốn: `{'png': ['img.png', 'pic.png'], 'txt': ['doc.txt']}`.

```python
from collections import defaultdict

# Khai báo: Nếu key chưa có, tự động tạo ra một list rỗng []
files_by_ext = defaultdict(list)

files = ['img.png', 'doc.txt', 'pic.png']
for f in files:
    ext = f.split('.')[-1]
    # Không cần if ext in files_by_ext, cứ append thẳng tay
    files_by_ext[ext].append(f) 

print(dict(files_by_ext))
```

