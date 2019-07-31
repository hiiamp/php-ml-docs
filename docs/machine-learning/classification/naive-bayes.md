# NaiveBayes Classifier

Phân loại dựa trên việc áp dụng định lý Bayes với các tiên đề (thuần túy) độc lập một cách chặt chẽ.
### Train

Để train một classifier đơn giản bằng cách cung cấp cho nó các mẫu và nhãn tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
$samples = [[5, 1, 1], [1, 5, 1], [1, 1, 5]];
$labels = ['a', 'b', 'c'];

$classifier = new NaiveBayes();
$classifier->train($samples, $labels);
```

Bạn có thể train cho classifier bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

### Predict

Để dự đoán nhãn của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$classifier->predict([3, 1, 1]);
// return 'a'

$classifier->predict([[3, 1, 1], [1, 4, 1]]);
// return ['a', 'b']
```
