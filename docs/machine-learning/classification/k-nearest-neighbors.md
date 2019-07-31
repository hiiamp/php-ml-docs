# KNearestNeighbors Classifier

Phân loại sử dụng giải thuật k-nearest neighbors: sử dụng k phần tử "lân cận" để có thể phân loại được phần tử đang xét.

## Các tham số hàm dựng

* $k - số nearest neighbors sẽ quét (mặc định: 3)
* $distanceMetric - Đối tượng khoảng cách, mặc định là Euclidean (xem thêm [tài liệu về distance](../../math/distance.md))

```
$classifier = new KNearestNeighbors($k=4);
$classifier = new KNearestNeighbors($k=3, new Minkowski($lambda=4));
```

## Train

Để train một classifier đơn giản bằng cách cung cấp cho nó các mẫu và nhãn tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
$samples = [[1, 3], [1, 4], [2, 4], [3, 1], [4, 1], [4, 2]];
$labels = ['a', 'a', 'a', 'b', 'b', 'b'];

$classifier = new KNearestNeighbors();
$classifier->train($samples, $labels);
```

Bạn có thể train cho classifier bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

## Predict

Để dự đoán nhãn của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$classifier->predict([3, 2]);
// return 'b'

$classifier->predict([[3, 2], [1, 5]]);
// return ['b', 'a']
```
