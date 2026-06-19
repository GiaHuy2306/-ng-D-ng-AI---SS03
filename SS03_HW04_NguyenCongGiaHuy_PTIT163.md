# Bài 4: Phân tích & Lựa chọn - Iterative Prompting

## 1. Đáp án lựa chọn

**Chọn phương án C.**

## 2. Vì sao phương án C đúng nhất?

Phương án C thể hiện đúng tư duy **Iterative Prompting**, tức là không bỏ cuộc khi AI trả lời chưa tốt, mà tiếp tục cải thiện prompt dựa trên kết quả trước đó.

Quy trình Iterative Prompting gồm 3 bước chính:

### Bước 1: Đánh giá

Người dùng xem lại kết quả AI trả về và nhận ra đoạn code chưa tối ưu.

Cụ thể, AI dùng vòng lặp từ `2` đến `n - 1`, khiến thuật toán chậm khi kiểm tra số lớn.

### Bước 2: Nhận diện lỗi

Người dùng chỉ rõ lỗi nằm ở đâu:

```text
Vòng lặp chạy đến n - 1 là chưa tối ưu đối với số lớn.
```

Đây là điểm quan trọng vì AI được cho biết chính xác vấn đề cần sửa, thay vì chỉ nói chung chung là “code chưa tốt”.

### Bước 3: Tinh chỉnh

Người dùng đưa ra yêu cầu cải thiện cụ thể:

```text
Hãy sửa vòng lặp chỉ chạy đến căn bậc hai của n bằng Math.sqrt(n).
```

Cách này giúp giảm độ phức tạp thuật toán từ:

```text
O(n)
```

xuống còn:

```text
O(sqrt(n))
```

Nhờ đó, AI có cơ sở rõ ràng để sửa code đúng hướng và tạo ra phiên bản tối ưu hơn.

## 3. Vì sao phương án A không hiệu quả?

Phương án A là:

```text
Bỏ cuộc và tự mình viết lại code tối ưu bằng tay vì AI không thông minh như quảng cáo.
```

Phương án này không đúng với tinh thần Iterative Prompting vì:

* Không đánh giá và phản hồi lại kết quả AI.
* Không chỉ ra lỗi cụ thể cho AI.
* Không tận dụng khả năng cải thiện câu trả lời qua nhiều lượt chat.
* Làm mất thời gian vì người dùng phải tự làm lại toàn bộ.

Hệ quả là quá trình dùng AI bị dừng lại ngay khi gặp kết quả chưa tốt, trong khi đúng ra cần tiếp tục tinh chỉnh prompt.

## 4. Vì sao phương án B không hiệu quả?

Phương án B là:

```text
Mở một phiên chat mới và dán lại prompt ban đầu nhưng đổi từ viết hoa.
```

Phương án này cũng không hiệu quả vì:

* Mở phiên chat mới làm mất ngữ cảnh cũ.
* Chỉ đổi chữ viết hoa không cung cấp thêm thông tin kỹ thuật.
* AI vẫn không biết lỗi nằm ở đâu.
* Không có yêu cầu rõ ràng về thuật toán `Math.sqrt(n)` hay độ phức tạp `O(sqrt(n))`.

Hệ quả là AI có thể tiếp tục trả về kết quả tương tự như lần đầu, vì prompt chưa được cải thiện thật sự.

## 5. Kết luận

Phương án C là lựa chọn đúng nhất vì nó áp dụng đầy đủ quy trình **Đánh giá -> Nhận diện lỗi -> Tinh chỉnh**. Người dùng không chỉ nói kết quả chưa đạt, mà còn chỉ rõ nguyên nhân và đưa ra hướng sửa cụ thể. Đây chính là cách dùng AI hiệu quả trong Iterative Prompting.
