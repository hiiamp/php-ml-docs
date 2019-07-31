# Support Vector Regression

Hồi quy bằng việc sử dụng máy học với sự hỗ trợ của vector (Epsilon-Support Vector Regression) dựa trên libsvm.

### Các tham số hàm dựng

* $kernel (int) - loại nhân(kernel) được sự dụng trong thuật toán (mặc định: Kernel::RBF)
* $degree (int) -bậc của hàm Kernel::POLYNOMIAL (mặc định: 3)
* $epsilon (float) -  epsilon trong hàm mất mát (loss function) của epsilon-SVR (mặc định: 0.1)
* $cost (float) - tham số C trong C-SVC (mặc định: 1.0)
* $gamma (float) - hệ số nhân (kernel) cho ‘Kernel::RBF’, ‘Kernel::POLYNOMIAL’ và ‘Kernel::SIGMOID’. Nếu gamma là ‘null’ thì 1/features sẽ được sử dụng thay thế cho gamma.
* $coef0 (float) - hệ số tùy thuộc vào mỗi hàm của kernel. Nó chỉ thực sự có ý nghĩa trong ‘Kernel::POLYNOMIAL’ và ‘Kernel::SIGMOID’ (mặc định: 0.0)
* $tolerance (float) - dung sai (phạm vi sai số) của kết quả (mặc định: 0.001)
* $cacheSize (int) - kích cỡ của bộ nhớ cache tính bằng MB (mặc định: 100)
* $shrinking (bool) - rút ngắn thời gian train bằng giải thuật rút gọn heuristics? (mặc định: true)

```
$regression = new SVR(Kernel::LINEAR);
$regression = new SVR(Kernel::LINEAR, $degree = 3, $epsilon=10.0);
```

### Train

Để train một mô hình đơn giản bằng cách cung cấp cho nó các mẫu và kết quả đích tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
use Phpml\Regression\SVR;
use Phpml\SupportVectorMachine\Kernel;

$samples = [[60], [61], [62], [63], [65]];
$targets = [3.1, 3.6, 3.8, 4, 4.1];

$regression = new SVR(Kernel::LINEAR);
$regression->train($samples, $targets);
```

Bạn có thể train cho mô hình bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

### Predict

Để dự đoán kết quả đích của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$regression->predict([64])
// return 4.03
```
