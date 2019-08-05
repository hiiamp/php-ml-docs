# Variance Threshold

`VarianceThreshold` (ngưỡng phương sai) là một cách đơn giản và cơ bản để tiếp cận feature selection (lựa chọn đặc tính). 
Nó sẽ loại bỏ tất cả các đặc tính không đạt đến một ngưỡng phương sai nhất định nào đó (tức là loại bỏ các đặc tính mà độ ảnh hưởng của nó là nhỏ và "có thể bỏ qua" trong quá trình tính toán, phân loại ...). 
Mặc định, các đặc tính có phương sai bằng 0 sẽ bị loại bỏ, i.e. đặc tính có cùng giá trị trong tất cả mẫu.

## Các tham số hàm dựng

* $threshold (float) - đặc tính với phương sai nhỏ hơn ngưỡng này sẽ bị loại bỏ (mặc định: 0.0)

```php
use Phpml\FeatureSelection\VarianceThreshold;

$transformer = new VarianceThreshold(0.15);
```

## Example of use

Ví dụ, giả sử chúng ta có một tập dữ liệu chưa các đặc tính kiểu boolean và chúng ta muốn loại bỏ tất cả các đặc tính là một hoặc không (on or off)
trong hơn 80% mẫu. 
Các đặc tính boolean là các biến ngẫu nhiên tuân theo bernouli, và phương sai của các biến đó được tính bằng:
```
Var[X] = p(1 - p)
```
Tiếp theo, chúng ta có thể sử dụng ngưỡng (`threshold`) .8 * (1 - .8):

```php
use Phpml\FeatureSelection\VarianceThreshold;

$samples = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [0, 1, 0], [0, 1, 1]];
$transformer = new VarianceThreshold(0.8 * (1 - 0.8));

$transformer->fit($samples);
$transformer->transform($samples);

/*
$samples = [[0, 1], [1, 0], [0, 0], [1, 1], [1, 0], [1, 1]];
*/
```

## Pipeline

`VarianceThreshold` được implements `Transformer` interface vì vậy nó có thể sử dụng như một phần của pipeline:

```php
use Phpml\FeatureSelection\VarianceThreshold;
use Phpml\Classification\SVC;
use Phpml\FeatureExtraction\TfIdfTransformer;
use Phpml\Pipeline;

$transformers = [
    new TfIdfTransformer(),
    new VarianceThreshold(0.1)
];
$estimator = new SVC();

$pipeline = new Pipeline($transformers, $estimator);
```
