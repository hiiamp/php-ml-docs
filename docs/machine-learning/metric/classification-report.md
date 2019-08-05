# Classification Report

Lớp tính toán các số liệu chính của một kết quả phân loại : precision, recall, F1 score and support (các số liệu này sẽ được trình bày rõ ở phía dưới).

### Report

Các tham số phải cung cấp để tạo một đối tượng `report`:

* $actualLabels - (array) nhãn đúng của mẫu
* $predictedLabels - (array) nhãn dự đoán tương ứng

```
use Phpml\Metric\ClassificationReport;

$actualLabels = ['cat', 'ant', 'bird', 'bird', 'bird'];
$predictedLabels = ['cat', 'cat', 'bird', 'bird', 'ant'];

$report = new ClassificationReport($actualLabels, $predictedLabels);
```

Tham số sau là tùy chọn:

* $average - (int) averaging method for multi-class classification
    * `ClassificationReport::MICRO_AVERAGE` = 1
    * `ClassificationReport::MACRO_AVERAGE` = 2 (default)
    * `ClassificationReport::WEIGHTED_AVERAGE` = 3

### Metrics

Sau khi khởi tạo một đối tượng `report`, bạn có thể lấy ra các số liệu sau bằng cách sử dụng các phương thức tương ứng:

* precision (`getPrecision()`) - tỉ lệ đúng khi so sánh giữa kết quả dự đoán với kết quả thực
* recall (`getRecall()`) - tỉ lệ đúng khi so sánh giữa kết quả thực với kết quả dự đoán
* F1 score (`getF1score()`) - điểm đánh giá độ chính xác
* support (`getSupport()`) - số lượng mẫu
* average (`getAverage()`) - trung bình của các tham số `precision`, `recall`, `support`

```
$precision = $report->getPrecision();
// $precision = ['cat' => 0.5, 'ant' => 0.0, 'bird' => 1.0];
```

### Example

```
use Phpml\Metric\ClassificationReport;

$actualLabels = ['cat', 'ant', 'bird', 'bird', 'bird'];
$predictedLabels = ['cat', 'cat', 'bird', 'bird', 'ant'];

$report = new ClassificationReport($actualLabels, $predictedLabels);

$report->getPrecision();
// ['cat' => 0.5, 'ant' => 0.0, 'bird' => 1.0]

$report->getRecall();
// ['cat' => 1.0, 'ant' => 0.0, 'bird' => 0.67]

$report->getF1score();
// ['cat' => 0.67, 'ant' => 0.0, 'bird' => 0.80]

$report->getSupport();
// ['cat' => 1, 'ant' => 1, 'bird' => 3]

$report->getAverage();
// ['precision' => 0.5, 'recall' => 0.56, 'f1score' => 0.49]
```
