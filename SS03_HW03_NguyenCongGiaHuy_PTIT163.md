# Bài 3: Đọc hiểu & Dò lỗi qua Prompt

## 1. Phân tích lý do prompt thô thất bại

Prompt thô:

```text
Code này có chạy được không?
```

Prompt này thất bại vì câu hỏi quá chung chung, không định hướng AI phải kiểm tra lỗi logic hoặc trường hợp biên.

Các vấn đề chính:

* **Không có vai trò rõ ràng:** AI không được yêu cầu đóng vai QA/Tester hay người kiểm thử chuyên sâu, nên có thể chỉ kiểm tra cú pháp.
* **Không có mục tiêu cụ thể:** Prompt chỉ hỏi “có chạy được không”, không yêu cầu phân tích lỗi runtime, lỗi logic hay test case.
* **Không có bối cảnh nghiệp vụ:** Không nói hàm dùng để tính trung bình danh sách số nguyên và cần xử lý dữ liệu đầu vào không hợp lệ.
* **Không có ràng buộc kiểm thử:** Không yêu cầu kiểm tra các trường hợp như `numbers == null`, `numbers.isEmpty()` hoặc danh sách có số âm.
* **Không có định dạng đầu ra:** Không yêu cầu AI phải đưa ra code đã sửa và JUnit test case.

Hệ quả là AI có thể chỉ kết luận rằng code đúng cú pháp Java và chạy được với danh sách hợp lệ. Tuy nhiên, AI dễ bỏ sót lỗi nghiêm trọng như:

* `NullPointerException` khi `numbers == null`
* Kết quả không hợp lệ khi `numbers.isEmpty()` vì phép chia cho `numbers.size()` bằng 0

---

## 2. Prompt tối ưu mới

```text
Hãy đóng vai là một Chuyên gia Kiểm thử phần mềm QA/Tester có kinh nghiệm trong Java.

Nhiệm vụ của bạn là đọc hiểu, trace code và kiểm tra lỗi logic trong đoạn mã Java sau. Hãy tập trung vào các trường hợp biên có thể làm chương trình lỗi runtime hoặc trả về kết quả sai.

Bối cảnh:
Đoạn code dùng để tính giá trị trung bình của một danh sách số nguyên `List<Integer>`. Hàm cần hoạt động an toàn với dữ liệu đầu vào không hợp lệ.

Mã nguồn cần kiểm tra:

public class AverageCalculator {

    public static double calculateAverage(List<Integer> numbers) {

        int sum = 0;

        for (int num : numbers) {

            sum += num;

        }

        return (double) sum / numbers.size();

    }

}

Yêu cầu phân tích:
1. Chỉ ra code hiện tại có lỗi gì.
2. Nêu rõ các trường hợp biên có thể làm chương trình lỗi, đặc biệt:
   - `numbers == null`
   - `numbers.isEmpty()`
3. Giải thích ngắn gọn nguyên nhân lỗi.
4. Viết lại mã nguồn Java đã sửa lỗi hoàn chỉnh.
5. Sinh thêm JUnit test case để kiểm thử:
   - Danh sách hợp lệ
   - Danh sách rỗng
   - Danh sách null
   - Danh sách có số âm

Ràng buộc:
- Sử dụng Java.
- Với danh sách `null` hoặc rỗng, hãy ném `IllegalArgumentException`.
- Code cần rõ ràng, dễ đọc.
- Có chú thích tiếng Việt ở các bước logic quan trọng.

Định dạng đầu ra:
- Trình bày trong khối code markdown.
- Bao gồm cả class `AverageCalculator` đã sửa và class test `AverageCalculatorTest`.
```

---

## 3. Code Java đã sửa lỗi và JUnit test case

```java
import java.util.List;

public class AverageCalculator {

    public static double calculateAverage(List<Integer> numbers) {

        // Kiểm tra trường hợp danh sách bị null
        // Nếu không kiểm tra, vòng lặp for-each sẽ gây NullPointerException
        if (numbers == null) {
            throw new IllegalArgumentException("Danh sách số không được null");
        }

        // Kiểm tra trường hợp danh sách rỗng
        // Nếu danh sách rỗng, numbers.size() = 0, việc tính trung bình không hợp lệ
        if (numbers.isEmpty()) {
            throw new IllegalArgumentException("Danh sách số không được rỗng");
        }

        int sum = 0;

        // Duyệt qua từng số trong danh sách và cộng vào tổng
        for (int num : numbers) {
            sum += num;
        }

        // Ép kiểu sang double để phép chia trả về số thực
        return (double) sum / numbers.size();
    }
}
```

```java
import org.junit.jupiter.api.Test;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

import static org.junit.jupiter.api.Assertions.*;

public class AverageCalculatorTest {

    @Test
    void testCalculateAverageWithValidNumbers() {
        // Kiểm tra danh sách hợp lệ
        List<Integer> numbers = Arrays.asList(10, 20, 30);

        double result = AverageCalculator.calculateAverage(numbers);

        assertEquals(20.0, result);
    }

    @Test
    void testCalculateAverageWithEmptyList() {
        // Kiểm tra trường hợp danh sách rỗng
        List<Integer> numbers = Collections.emptyList();

        IllegalArgumentException exception = assertThrows(
                IllegalArgumentException.class,
                () -> AverageCalculator.calculateAverage(numbers)
        );

        assertEquals("Danh sách số không được rỗng", exception.getMessage());
    }

    @Test
    void testCalculateAverageWithNullList() {
        // Kiểm tra trường hợp danh sách bị null
        List<Integer> numbers = null;

        IllegalArgumentException exception = assertThrows(
                IllegalArgumentException.class,
                () -> AverageCalculator.calculateAverage(numbers)
        );

        assertEquals("Danh sách số không được null", exception.getMessage());
    }

    @Test
    void testCalculateAverageWithNegativeNumbers() {
        // Kiểm tra danh sách có số âm
        List<Integer> numbers = Arrays.asList(-10, -20, -30);

        double result = AverageCalculator.calculateAverage(numbers);

        assertEquals(-20.0, result);
    }

    @Test
    void testCalculateAverageWithMixedNumbers() {
        // Kiểm tra danh sách vừa có số âm, số dương và số 0
        List<Integer> numbers = Arrays.asList(-10, 0, 10);

        double result = AverageCalculator.calculateAverage(numbers);

        assertEquals(0.0, result);
    }
}
```

---

## 4. Kết luận

Prompt tối ưu tốt hơn vì đã chỉ rõ **vai trò**, **mục tiêu**, **bối cảnh**, **ràng buộc** và **định dạng đầu ra**. Nhờ đó, AI không chỉ kiểm tra cú pháp mà còn phải phân tích lỗi logic, tìm trường hợp biên, sửa code và viết test case để xác minh.
