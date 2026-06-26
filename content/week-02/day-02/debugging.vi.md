+++
title = "Ghi chú về Kỹ năng gỡ lỗi (Debugging)"
weight = 3
+++

### 1. Gỡ lỗi bằng AI (AI-Assisted Debugging)

Sử dụng AI (như Antigravity, Gemini, ChatGPT...) giúp tăng tốc độ tìm lỗi rất nhanh:
- **Đưa lỗi trực tiếp:** Sao chép nguyên văn stack trace hoặc thông báo lỗi dán vào AI và yêu cầu giải thích nguyên nhân.
- **Giải thích ngữ cảnh:** Cung cấp file code chứa lỗi kèm theo lỗi đang gặp.
- **Hỏi cách sửa tối ưu:** Yêu cầu AI chỉ ra nguyên nhân gốc rễ (root cause) thay vì chỉ lấy code sửa tạm thời (quick fix).
- **Mẹo viết prompt:** "Giải thích lỗi sau: `[nội dung lỗi]`. Đoạn code liên quan: `[dán code]`. Hãy phân tích tại sao lỗi này xảy ra và đề xuất phương án giải quyết."

---

### 2. Sử dụng Console Log đúng cách

Ghi log ra console (`console.log`) là cách thủ công phổ biến nhất, nhưng cần lưu ý:
- **Ghi log có nhãn (Labeled Logs):** Nên thêm nhãn rõ ràng để biết dữ liệu từ đâu ra.
  * *Tệ:* `console.log(data);`
  * *Tốt:* `console.log(">>> Auth API Response:", data);`
- **Sử dụng các hàm log chuyên dụng:**
  * `console.error()`: Ghi nhận lỗi (hiển thị màu đỏ trong terminal/browser console).
  * `console.warn()`: Cảnh báo nguy cơ lỗi (hiển thị màu vàng).
  * `console.table()`: In mảng/đối tượng dưới dạng bảng cực kỳ trực quan.
- **Lưu ý quan trọng:** **Luôn xóa sạch `console.log` trước khi commit/push code lên production**, vì log thừa có thể làm giảm hiệu năng ứng dụng và rò rỉ thông tin bảo mật.

---

### 3. Đặt Breakpoint (Điểm dừng)

Sử dụng các công cụ Debugging chuyên nghiệp (trong VS Code, Chrome DevTools, Xcode...) để dừng chương trình tại dòng mong muốn:
- **Cách hoạt động:** Khi code chạy đến dòng có breakpoint, ứng dụng sẽ dừng lại. Bạn có thể kiểm tra giá trị của tất cả biến hiện tại (Scope/Variables) mà không cần viết `console.log`.
- **Chạy từng dòng (Stepping):**
  * *Step Over:* Chạy qua dòng tiếp theo.
  * *Step Into:* Nhảy vào bên trong hàm của dòng hiện tại để xem chi tiết.
  * *Step Out:* Chạy hết hàm hiện tại và quay ra ngoài.
- **Conditional Breakpoint (Điểm dừng có điều kiện):** Chỉ dừng lại khi biểu thức điều kiện thỏa mãn. Hữu dụng khi debug vòng lặp lớn (ví dụ: chỉ dừng khi `i === 99`).
- **Logpoint:** Cho phép ghi log ra console trực tiếp từ debugger mà không cần sửa đổi mã nguồn.

---

### 4. Cách đọc Stack Trace (Vết ngăn xếp)

Stack Trace là danh sách các hàm được gọi liên tiếp dẫn đến lỗi tại thời điểm ứng dụng bị sập.

* **Quy trình đọc:**
  1. **Xem dòng đầu tiên:** Thường chứa tên lỗi và mô tả lỗi (ví dụ: `TypeError: Cannot read properties of undefined (reading 'map')`).
  2. **Tìm file code dự án:** Bỏ qua các dòng trace thuộc thư viện (`node_modules`), tìm dòng đầu tiên chứa đường dẫn file của dự án bạn viết (ví dụ: `at OnboardingScreen.tsx:45:12`).
  3. **Lần theo chuỗi gọi hàm:** Đọc từ trên xuống dưới (đối với JS/TS) để biết hàm nào gọi hàm nào dẫn tới dòng bị lỗi đó.
