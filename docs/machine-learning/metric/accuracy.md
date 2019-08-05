# Accuracy

Lớp hỗ trợ tính toán độ chính xác của thuật toán phân loại.

### Score

Để tính toán độ chính xác của một kết quả phân loại, sử dụng phương thức `score` (đây là một phương thức tĩnh - static). Các tham số đầu vào như sau:

* $actualLabels - (array) nhãn đúng của mẫu
* $predictedLabels - (array) các nhãn được dự đoán tương ứng
* $normalize - (bool) trả về tỉ lệ hay số nhãn giống nhau (mặc định: true - tức là trả về tỉ lệ)

### Example

```
$actualLabels = ['a', 'b', 'a', 'b'];
$predictedLabels = ['a', 'a', 'a', 'b'];

Accuracy::score($actualLabels, $predictedLabels);
// return 0.75

Accuracy::score($actualLabels, $predictedLabels, false);
// return 3
```
