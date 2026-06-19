# Bài 2: Tối ưu Prompt Tóm tắt & Hệ thống hóa Tài liệu học tập

## 1. Nội dung Prompt sau khi tối ưu

```text
Hãy đóng vai là một Giảng viên Java giàu kinh nghiệm, có khả năng giảng dạy trực quan và dễ hiểu cho sinh viên mới học.

Nhiệm vụ của bạn là tóm tắt và hệ thống hóa nội dung sau về cơ chế Garbage Collection trong Java:

"Java Garbage Collection (GC) là quá trình tự động giải phóng bộ nhớ bằng cách tìm và xóa các đối tượng không còn được sử dụng trong bộ nhớ Heap. Bộ nhớ Heap được chia thành hai vùng chính: Young Generation và Old Generation. Vùng Young Generation lại được chia thành Eden Space và hai không gian Survivor (S0, S1). Khi một đối tượng mới được tạo ra bằng từ khóa new, nó sẽ được cấp phát tại Eden Space. Khi Eden Space đầy, một đợt dọn rác Minor GC sẽ được kích hoạt. Các đối tượng còn sống sót sau Minor GC sẽ được chuyển sang vùng Survivor. Sau nhiều lần sống sót qua các đợt Minor GC (đạt ngưỡng tuổi nhất định), đối tượng sẽ được thăng cấp (promoted) sang Old Generation. Vùng Old Generation lưu trữ các đối tượng có thời gian sống dài. Khi vùng này đầy, Major GC hoặc Full GC sẽ được kích hoạt để dọn dẹp. Quá trình Full GC thường tốn thời gian hơn rất nhiều so với Minor GC vì nó phải duyệt qua toàn bộ bộ nhớ Heap và có thể làm dừng toàn bộ ứng dụng (Stop-the-world)."

Yêu cầu đầu ra:
1. Tạo một bảng so sánh giữa Young Generation và Old Generation theo các tiêu chí:
   - Các vùng con bên trong
   - Loại đối tượng lưu trữ
   - Điều kiện kích hoạt GC
   - Tốc độ thực thi của GC

2. Sau bảng so sánh, tạo một sơ đồ ASCII đơn giản để trực quan hóa đường đi của một đối tượng từ khi được khởi tạo bằng `new` cho đến khi được thăng cấp sang Old Generation.

3. Giải thích ngắn gọn, dễ hiểu, phù hợp với người mới học Java.

4. Trình bày toàn bộ phản hồi trong một khối code markdown.