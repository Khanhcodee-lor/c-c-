# 7 Bài C/C++ Cơ Bản Để Bắt Đầu Học Lập Trình Nhúng (Embedded Systems)

Chào mừng bạn đến với lộ trình cơ bản C/C++ dành cho lập trình nhúng. Dưới đây là 7 bài học cốt lõi giúp bạn nắm vững nền tảng trước khi làm việc trực tiếp với phần cứng và vi điều khiển.

## Bài 1: Kiểu dữ liệu và Thư viện `stdint.h`
- Hiểu về kích thước bộ nhớ của các kiểu dữ liệu chuẩn (`char`, `int`, `float`) trên các kiến trúc khác nhau.
- Tầm quan trọng của thư viện `stdint.h` (`uint8_t`, `uint16_t`, `uint32_t`, `int8_t`,...) để đảm bảo tính nhất quán của dữ liệu ở các nền tảng VĐK (8-bit, 16-bit, 32-bit).
- Ép kiểu (Type casting) an toàn.

## Bài 2: Các Phép Toán Thao Tác Bit (Bitwise Operations)
- Các toán tử bit: AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), Dịch trái (`<<`), Dịch phải (`>>`).
- Kỹ thuật thao tác bit cơ bản:
  - **Set bit**: Bật 1 bit lên mức 1.
  - **Clear bit**: Xóa 1 bit về mức 0.
  - **Toggle bit**: Đảo trạng thái 1 bit.
  - **Read bit / Check bit**: Đọc trạng thái của 1 bit cụ thể.
- **Ứng dụng:** Thao tác trực tiếp với các thanh ghi (Registers) của vi điều khiển.

## Bài 3: Con trỏ (Pointers) và Từ khóa `volatile`
- Bản chất của con trỏ: Lưu trữ địa chỉ bộ nhớ.
- Truy cập và thay đổi giá trị thông qua con trỏ (Dereferencing).
- Con trỏ vô kiểu (`void *`) và ép kiểu con trỏ.
- **Từ khóa `volatile`**: Cực kỳ quan trọng trong Embedded. Báo cho trình biên dịch biết biến này có thể bị thay đổi bởi các yếu tố bên ngoài (như phần cứng, ngắt - ISR) để không tối ưu hóa biến đó.

## Bài 4: Mảng (Arrays), Chuỗi (Strings) và Quản lý Vùng Nhớ
- Thao tác an toàn với mảng 1 chiều và chuỗi ký tự (`char array`).
- Khái niệm về con trỏ và mảng (Pointer arithmetic).
- Phân biệt các vùng nhớ: **Stack** (biến cục bộ), **Heap** (cấp phát động), **Data** (biến toàn cục/static đã khởi tạo), **BSS** (chưa khởi tạo) và **Text/Flash** (mã lệnh).
- Lý do tại sao lập trình nhúng (đặc biệt là Bare-metal) thường hạn chế hoặc không dùng cấp phát động (`malloc`/`free`).

## Bài 5: Cấu trúc (Struct), Hợp nhất (Union) và Enum
- **Struct**: Đóng gói các dữ liệu liên quan. 
  - Khái niệm Memory Alignment và Struct Padding.
  - Cách dùng `__attribute__((packed))` để tránh lãng phí bộ nhớ khi truyền nhận dữ liệu (ví dụ: bản tin UART, CAN).
- **Union**: Các biến dùng chung một vùng nhớ. Rất hữu ích khi cần tách/ghép các byte dữ liệu (ví dụ: tách 1 biến 32-bit thành 4 biến 8-bit).
- **Enum**: Liệt kê các hằng số, giúp code dễ đọc và quản lý trạng thái tốt hơn.

## Bài 6: Tiền xử lý (Preprocessor) và Macros
- Chỉ thị `#include`, `#define`.
- Biên dịch có điều kiện: `#ifdef`, `#ifndef`, `#if`, `#endif` (Hữu ích khi viết code hỗ trợ nhiều chip khác nhau).
- Viết Macros như một hàm (`Function-like macros`). 
- Ưu/nhược điểm của Macro so với hàm (Inline functions). Các Macro thao tác bit phổ biến (`SET_BIT`, `CLEAR_BIT`).

## Bài 7: Hàm, Con Trỏ Hàm và Máy Trạng Thái (State Machine)
- Phân biệt truyền tham trị (Pass by value) và truyền tham chiếu/con trỏ (Pass by pointer/reference).
- **Con trỏ hàm (Function Pointers)**: Cách khai báo và sử dụng. Ứng dụng phổ biến trong việc tạo Callback functions (xử lý sự kiện, ngắt).
- **Máy trạng thái hữu hạn (FSM - Finite State Machine)**: Cách tư duy và thiết kế chương trình C theo dạng non-blocking (không dùng `delay()` làm treo hệ thống) để xử lý nhiều tác vụ cùng lúc trên VĐK.