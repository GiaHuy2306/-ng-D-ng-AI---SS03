# Bài 1: Phân tích & Lựa chọn Prompt

## 1. Đáp án lựa chọn

**Chọn phương án B.**

## 2. Vì sao phương án B tối ưu nhất?

Phương án B áp dụng đầy đủ nhất cấu trúc **5 thành phần cốt lõi của Prompt** gồm: **Role - Goal - Context - Constraint - Format**.

### Role - Vai trò

Phương án B có nêu rõ:

> "Hãy đóng vai trò là một Java Developer chuyên nghiệp."

Điều này giúp AI hiểu cần trả lời theo góc nhìn của một lập trình viên Java có kinh nghiệm, từ đó sinh ra mã nguồn chuẩn hơn.

### Goal - Mục tiêu

Prompt nêu rõ nhiệm vụ:

> "Viết class UserService xử lý đăng ký tài khoản (registerUser)."

AI biết chính xác cần tạo lớp dịch vụ nào và hàm nào, tránh trả lời lan man hoặc thiếu trọng tâm.

### Context - Bối cảnh

Prompt cung cấp bối cảnh kỹ thuật:

> "Dự án sử dụng Spring Boot 3.x và Java 17."

Thông tin này giúp AI sinh code phù hợp với phiên bản Java và Spring Boot đang dùng.

### Constraint - Ràng buộc

Phương án B nêu rõ các ràng buộc nghiệp vụ:

- Kiểm tra trùng email bằng `userRepository.existsByEmail()`
- Nếu trùng thì ném `DuplicateEmailException`
- Mã hóa mật khẩu bằng `PasswordEncoder`

Nhờ vậy, AI có đủ điều kiện để viết đúng logic nghiệp vụ.

### Format - Định dạng đầu ra

Prompt yêu cầu rõ:

> "Trình bày kết quả dưới dạng khối mã nguồn Java kèm chú thích tiếng Việt rõ ràng ở từng bước."

Điều này giúp đầu ra đúng định dạng mong muốn, dễ đọc và dễ sử dụng.

## 3. Vì sao phương án A chưa tốt?

Phương án A chỉ nêu yêu cầu chung chung:

> "Hãy viết code Java Spring Boot xử lý đăng ký tài khoản người dùng..."

### Các thành phần còn thiếu hoặc chưa rõ

- **Role:** Không yêu cầu AI đóng vai trò cụ thể.
- **Goal:** Có mục tiêu nhưng chưa rõ cần viết class nào, hàm nào.
- **Context:** Không nói dự án dùng Java 17 hay Spring Boot 3.x.
- **Constraint:** Có nhắc mã hóa mật khẩu và kiểm tra email, nhưng không chỉ rõ dùng `userRepository.existsByEmail()` hay ném `DuplicateEmailException`.
- **Format:** Không yêu cầu định dạng code cụ thể và chú thích tiếng Việt.

### Hệ quả

AI có thể viết code chưa đúng cấu trúc mong muốn, thiếu exception, thiếu hàm cụ thể hoặc dùng cách kiểm tra email khác.

## 4. Vì sao phương án C chưa tốt?

Phương án C có nêu một số thông tin nhưng vẫn chưa đầy đủ.

### Các thành phần còn thiếu hoặc chưa rõ

- **Role:** Không có vai trò cho AI.
- **Goal:** Có yêu cầu tạo hàm đăng ký nhưng chưa nói rõ class `UserService` hay hàm `registerUser`.
- **Context:** Chỉ nói dự án Spring Boot, chưa nêu Java 17 và Spring Boot 3.x.
- **Constraint:** Có yêu cầu check trùng email và ném `DuplicateEmailException`, nhưng chưa nêu rõ phải dùng `userRepository.existsByEmail()` và chưa nhắc mã hóa mật khẩu bằng `PasswordEncoder`.
- **Format:** Chỉ yêu cầu code Java, chưa yêu cầu chú thích tiếng Việt chi tiết.

### Hệ quả

AI có thể sinh code thiếu mã hóa mật khẩu, dùng sai cách kiểm tra email hoặc không đúng chuẩn cấu trúc OOP.

## 5. Kết luận

Phương án B là tốt nhất vì có đầy đủ 5 thành phần quan trọng của một prompt hiệu quả: **Role, Goal, Context, Constraint và Format**. Nhờ đó, AI có thể hiểu rõ yêu cầu và tạo ra mã nguồn Java Spring Boot chính xác hơn ngay từ lần đầu.