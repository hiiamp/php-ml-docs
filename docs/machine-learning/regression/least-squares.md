# LeastSquares Linear Regression

Mô hình hồi quy tuyến tính sử dụng phương pháp bình phương nhỏ nhất để đưa ra lời giải gần đúng. 

### Train

Để train một mô hình đơn giản bằng cách cung cấp cho nó các mẫu và kết quả đích tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
$samples = [[60], [61], [62], [63], [65]];
$targets = [3.1, 3.6, 3.8, 4, 4.1];

$regression = new LeastSquares();
$regression->train($samples, $targets);
```

Bạn có thể train cho mô hình bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

### Predict

Để dự đoán kết quả đích của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$regression->predict([64]);
// return 4.06
```

### Multiple Linear Regression

Hồi quy tuyến tính đa biến có cách sử dụng tương tự nhưng với đầu vào nhiều tham số hơn để dự đoán ra kết quả đích. 
Ví dụ: Mô hình sau sử dụng quãng đường đã đi được và năm sản xuất để tính toán giá trị của một chiếc oto.  

```
$samples = [[73676, 1996], [77006, 1998], [10565, 2000], [146088, 1995], [15000, 2001], [65940, 2000], [9300, 2000], [93739, 1996], [153260, 1994], [17764, 2002], [57000, 1998], [15000, 2000]];
$targets = [2000, 2750, 15500, 960, 4400, 8800, 7100, 2550, 1025, 5900, 4600, 4400];

$regression = new LeastSquares();
$regression->train($samples, $targets);
$regression->predict([60000, 1996])
// return 4094.82
```

### Sai số và hệ số hồi quy

Sau khi train cho mô hình của mình, bạn có thể lấy được sai số (intercept) và mảng hệ số hồi quy (coefficients) của mô hình đó.
```
$regression->getIntercept();
// return -7.9635135135131

$regression->getCoefficients();
// return [array(1) {[0]=>float(0.18783783783783)}]
```
