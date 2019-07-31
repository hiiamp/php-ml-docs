# Phân loại với sự hỗ trợ của vector - Support Vector Classification

Việc phân loại sẽ thưc hiện bởi máy học với sự hỗ trợ của vector (Support Vector Machine) dựa trên libsvm.

### Các tham số hàm dựng

* $kernel (int) - loại nhân (kernel) được sử dụng trong thuật toán (mặc đinh: Kernel::RBF)
* $cost (float) - tham số C trong C-SVC (mặc định: 1.0)
* $degree (int) - bậc của hàm Kernel::POLYNOMIAL (default 3)
* $gamma (float) - hệ số nhân (kernel) cho ‘Kernel::RBF’, ‘Kernel::POLYNOMIAL’ và ‘Kernel::SIGMOID’. Nếu gamma là ‘null’ thì 1/features sẽ được sử dụng thay thế cho gamma.
* $coef0 (float) - hệ số tùy thuộc vào mỗi hàm của kernel. Nó chỉ thực sự có ý nghĩa trong ‘Kernel::POLYNOMIAL’ và ‘Kernel::SIGMOID’ (mặc định: 0.0)
* $tolerance (float) - dung sai (phạm vi sai số) của kết quả (mặc định: 0.001)
* $cacheSize (int) - kích cỡ của bộ nhớ cache tính bằng MB (mặc định: 100)
* $shrinking (bool) - rút ngắn thời gian train bằng giải thuật rút gọn heuristics? (mặc định: true)
* $probabilityEstimates (bool) - bật chức năng ước tính xác suất? (mặc định: false)

```
$classifier = new SVC(Kernel::LINEAR, $cost = 1000);
$classifier = new SVC(Kernel::RBF, $cost = 1000, $degree = 3, $gamma = 6);
```

### Train

Để train một classifier đơn giản bằng cách cung cấp cho nó các mẫu và nhãn tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
use Phpml\Classification\SVC;
use Phpml\SupportVectorMachine\Kernel;

$samples = [[1, 3], [1, 4], [2, 4], [3, 1], [4, 1], [4, 2]];
$labels = ['a', 'a', 'a', 'b', 'b', 'b'];

$classifier = new SVC(Kernel::LINEAR, $cost = 1000);
$classifier->train($samples, $labels);
```

Bạn có thể train cho classifier bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

### Predict

Để dự đoán nhãn của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$classifier->predict([3, 2]);
// return 'b'

$classifier->predict([[3, 2], [1, 5]]);
// return ['b', 'a']
```

### Ước tính xác suất

Để sử dụng tính năng ước tính xác suất, khi khỏi tạo classifier thì tham số `$probabilityEstimates` phải được đặt là true. Ví dụ:

```
use Phpml\Classification\SVC;
use Phpml\SupportVectorMachine\Kernel;

$samples = [[1, 3], [1, 4], [2, 4], [3, 1], [4, 1], [4, 2]];
$labels = ['a', 'a', 'a', 'b', 'b', 'b'];

$classifier = new SVC(
    Kernel::LINEAR, // $kernel
    1.0,            // $cost
    3,              // $degree
    null,           // $gamma
    0.0,            // $coef0
    0.001,          // $tolerance
    100,            // $cacheSize
    true,           // $shrinking
    true            // $probabilityEstimates, set to true
);

$classifier->train($samples, $labels);
```

Sử dụng phương thức `predictProbability` thay cho `predict`:

```
$classifier->predictProbability([3, 2]);
// return ['a' => 0.349833, 'b' => 0.650167]

$classifier->predictProbability([[3, 2], [1, 5]]);
// return [
//   ['a' => 0.349833, 'b' => 0.650167],
//   ['a' => 0.922664, 'b' => 0.0773364],
// ]
```
