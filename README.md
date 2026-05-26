# Lộ Trình Ôn Tập C/C++ Cho Lập Trình Nhúng

Tài liệu này cung cấp lý thuyết tóm tắt và hướng dẫn thực hiện cho 7 bài tập cốt lõi. Mỗi bài tập tập trung vào một kỹ năng quan trọng trong lập trình hệ thống.

---

## Bài 1: Kiểu dữ liệu & Thư viện `stdint.h` / `cstdint`

### 📘 Lý thuyết
- **Vấn đề:** Kiểu `int` có thể là 2 byte trên MCU 8-bit nhưng lại là 4 byte trên MCU 32-bit.
- **Giải pháp:** Dùng `stdint.h` (C) hoặc `cstdint` (C++) để cố định kích thước:
  - `int8_t` / `uint8_t`: 1 byte (-128..127 / 0..255)
  - `int16_t` / `uint16_t`: 2 byte
  - `int32_t` / `uint32_t`: 4 byte
- **Tràn số (Overflow):** Khi một biến vượt quá giới hạn của nó (ví dụ: `uint8_t` đang là 255, cộng thêm 1 sẽ quay về 0).

### 💡 Hướng dẫn làm bài
1. Dùng `scanf("%lld", &n)` (C) hoặc `cin >> n` (C++) để nhập số lớn.
2. So sánh `n` với các hằng số giới hạn (VD: -128 và 127).
3. Sử dụng ép kiểu: `(int8_t)n` hoặc `static_cast<int8_t>(n)`.

---

## Bài 2: Thao tác Bit (Bitwise Operations)

### 📘 Lý thuyết
- **Mặt nạ (Mask):** `(1 << n)` tạo ra một số có bit thứ `n` bằng 1.
- **Các phép toán:**
  - **Set bit:** `REG |= (1 << n)` (Dùng OR với 1).
  - **Clear bit:** `REG &= ~(1 << n)` (Dùng AND với 0).
  - **Toggle bit:** `REG ^= (1 << n)` (Dùng XOR với 1).
  - **Read bit:** `(REG >> n) & 1`.

### 💡 Hướng dẫn làm bài
1. In số Hex: `printf("0x%X", n)` hoặc `cout << hex << uppercase << n`.
2. Phép XOR không dùng `^`: Sử dụng công thức logic `(A & ~B) | (~A & B)`.

---

## Bài 3: Con trỏ (Pointers) & Volatile

### 📘 Lý thuyết
- **Con trỏ:** Lưu địa chỉ. `*p` để lấy giá trị tại địa chỉ đó.
- **Hoán vị:** Phải truyền địa chỉ (`&a`, `&b`) vào hàm để thay đổi giá trị gốc.
- **Truy cập byte:** Ép kiểu địa chỉ bất kỳ sang `uint8_t*` để đọc từng byte một.
- **Volatile:** Báo trình biên dịch "đừng tối ưu biến này". Thường dùng cho biến thay đổi bởi phần cứng hoặc ngắt.

### 💡 Hướng dẫn làm bài
1. Hàm swap: `void swap(int *a, int *b) { int temp = *a; *a = *b; *b = temp; }`.
2. Đọc byte của float: `uint8_t *ptr = (uint8_t *)&f;` sau đó dùng vòng lặp 4 lần.

---

## Bài 4: Mảng & Chuỗi (Arrays & Strings)

### 📘 Lý thuyết
- **Mảng & Con trỏ:** `arr[i]` tương đương với `*(arr + i)`.
- **Đảo ngược mảng:** Dùng 2 con trỏ (một ở đầu, một ở cuối) đổi chỗ cho nhau dần vào giữa.
- **Chuỗi trong C:** Là mảng `char` kết thúc bằng ký tự `\0`.

### 💡 Hướng dẫn làm bài
1. Duyệt mảng bằng con trỏ: `for (int *p = arr; p < arr + n; p++)`.
2. Nối chuỗi: Tìm vị trí `\0` của chuỗi 1, sau đó copy từng ký tự chuỗi 2 vào.

---

## Bài 5: Struct, Union & Enum

### 📘 Lý thuyết
- **Struct:** Các phần tử nằm ở các địa chỉ khác nhau. Kích thước = tổng các phần tử + padding (để căn lề bộ nhớ).
- **Union:** Tất cả phần tử dùng chung **một** địa chỉ. Kích thước = phần tử lớn nhất.
- **Enum:** Định nghĩa các hằng số có tên giúp code dễ đọc.

### 💡 Hướng dẫn làm bài
1. Dùng Union để tách số 32-bit:
   ```c
   union { uint32_t value; uint8_t bytes[4]; } data;
   ```
2. Nhập `data.value`, sau đó in `data.bytes[0]`...`data.bytes[3]`.

---

## Bài 6: Tiền xử lý (Preprocessor) & Macros

### 📘 Lý thuyết
- **Macro:** Là thay thế văn bản trước khi biên dịch.
- **An toàn Macro:** Luôn dùng ngoặc đơn bao quanh tham số: `#define SQUARE(x) ((x) * (x))`.
- **Biên dịch điều kiện:** Dùng để bật/tắt tính năng hoặc hỗ trợ nhiều dòng chip khác nhau.

### 💡 Hướng dẫn làm bài
1. Viết `SET_BIT(reg, bit)` tương tự bài 2 nhưng dùng tham số.
2. Kiểm tra `#ifdef DEBUG` để in log.

---

## Bài 7: Con trỏ hàm & State Machine

### 📘 Lý thuyết
- **Con trỏ hàm:** Lưu địa chỉ của một hàm để gọi gián tiếp. Cú pháp: `void (*func_ptr)(int, int)`.
- **State Machine:** Hệ thống chuyển đổi giữa các trạng thái dựa trên sự kiện. Giúp quản lý logic phức tạp (như điều khiển thang máy, cửa tự động).

### 💡 Hướng dẫn làm bài
1. Mảng con trỏ hàm: `int (*math_funcs[])(int, int) = {add, sub, mul, div};`.
2. State Machine: Dùng biến `current_state` và cấu trúc `switch-case`.

---
*Chúc bạn ôn tập tốt! Nếu gặp lỗi khi chạy code, hãy copy lỗi đó và hỏi tôi.*
