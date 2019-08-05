# Confusion Matrix

Lớp hỗ trợ tính toán ra một "ma trận nhầm lẫn - `confusion matrix`" để từ đó đánh giá được độ chính xác của một thuật toán phân loại.

### Example (all targets)

Tính ma trận nhầm lẫn cho tất cả các mục tiêu.

```
use Phpml\Metric\ConfusionMatrix;

$actualTargets = [2, 0, 2, 2, 0, 1];
$predictedTargets = [0, 0, 2, 2, 0, 2];

$confusionMatrix = ConfusionMatrix::compute($actualTargets, $predictedTargets)

/*
$confusionMatrix = [
    [2, 0, 0],
    [0, 0, 1],
    [1, 0, 2],
];
*/
```

### Example (chosen targets)

Tính toán ma trận nhầm lẫn cho một vài mục tiêu được lựa chọn.

```
use Phpml\Metric\ConfusionMatrix;

$actualTargets = ['cat', 'ant', 'cat', 'cat', 'ant', 'bird'];
$predictedTargets = ['ant', 'ant', 'cat', 'cat', 'ant', 'cat'];

$confusionMatrix = ConfusionMatrix::compute($actualTargets, $predictedTargets, ['ant', 'bird'])

/*
$confusionMatrix = [
    [2, 0],
    [0, 0],
];
*/
```
