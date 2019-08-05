# SelectKBest

`SelectKBest` - lựa chọn k đặc tính có ảnh hưởng lớn nhất.

## Các tham số hàm dựng

* $k (int) - số đặc tính được lựa chọn, phần còn lại sẽ bị loại bỏ (default: 10)
* $scoringFunction (ScoringFunction) - hàm thực hiện tính toán từ `samples` và `targets` để trả về mảng với điểm số tương ứng (mặc định: ANOVAFValue)

```php
use Phpml\FeatureSelection\SelectKBest;

$transformer = new SelectKBest(2);
```

## Example of use

Để làm ví dụ, chúng ta có thể thực hiện lựa chọn đặc tính trên tập dữ liệu Iris để chỉ lấy 2 đặc tính tốt (ảnh hưởng) nhất như sau:

```php
use Phpml\FeatureSelection\SelectKBest;
use Phpml\Dataset\Demo\IrisDataset;

$dataset = new IrisDataset();
$selector = new SelectKBest(2);
$selector->fit($samples = $dataset->getSamples(), $dataset->getTargets());
$selector->transform($samples);

/*
$samples[0] = [1.4, 0.2]; 
*/
```

## Scores

Bạn sẽ nhận được một mảng với số điểm đánh giá độ ảnh hưởng cho mỗi đặc tính. 
Điểm số các cao thì độ ảnh hưởng của đặc tính đó càng lớn, tức là đặc tính càng hiệu quả hơn khi được sử dụng để train.
Tất nhiên, những điểm số này phụ thuộc, được tính bằng `ScoringFunction` đã sử dụng.

```
use Phpml\FeatureSelection\SelectKBest;
use Phpml\Dataset\Demo\IrisDataset;

$dataset = new IrisDataset();
$selector = new SelectKBest(2);
$selector->fit($samples = $dataset->getSamples(), $dataset->getTargets());
$selector->scores();

/*
..array(4) {
  [0]=>
  float(119.26450218451)
  [1]=>
  float(47.364461402997)
  [2]=>
  float(1179.0343277002)
  [3]=>
  float(959.32440572573)
} 
*/
```

## Scoring function

Các hàm đánh giá đặc tính có sẵn:

Đối với phân loại (classification):
 - **ANOVAFValue**
   Phân tích phương sai một yếu tố (the one-way ANOVA kiểm tra một giả thuyêt khống rằng có 2 hoặc nhiều nhóm có cùng ý nghĩa.
   Kiểm tra này được thực hiện cho các mẫu có từ hai nhóm trở lên, và kích cỡ của mỗi nhóm là có thể khác nhau.

Đối với hồi quy (regression):
 - **UnivariateLinearRegression**  
   Mô hình tuyến tính nhanh (quick linear model) kiểm tra độ hiệu quả của một biến hồi quy đơn hoặc tuần tự cho nhiều biến hồi quy.
   
   Điều này được thực hiện trong 2 bước:
   
     - 1. Mối tương quan chéo giữa mỗi biến hồi quy và kết quả đích được tính toán như sau:
      ((X[:, i] - mean(X[:, i])) * (y - mean_y)) / (std(X[:, i]) *std(y))
 
     - 2. Chuyển đối kết quả sang điểm số. 

## Pipeline

`SelectKBest` được implements `Transformer` interface vì vậy chúng ta có thể sử dụng như là một phần của pipeline:

```php
use Phpml\FeatureSelection\SelectKBest;
use Phpml\Classification\SVC;
use Phpml\FeatureExtraction\TfIdfTransformer;
use Phpml\Pipeline;

$transformers = [
    new TfIdfTransformer(),
    new SelectKBest(3)
];
$estimator = new SVC();

$pipeline = new Pipeline($transformers, $estimator);
```
