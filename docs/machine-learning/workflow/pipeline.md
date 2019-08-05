# Pipeline

Trong học máy, người ta thường chạy một chuỗi các thuật toán để xử lý và học từ tập dữ liệu.

    * Tách đừng đoạn văn bản của tài liệu thành các tokens.
    * Chuyển đổi mỗi từ ngữ của tài liệu thành các vector số học đặc trưng ([Token Count Vectorizer](machine-learning/feature-extraction/token-count-vectorizer/)).
    * Học để tạo ra mô hình dự đoán (`prediction model`) từ các vector đặc trưng và nhãn (`label`) tương ứng.
    
PHP-ML được thiết kế với luồng làm việc tương tự như một "đường ống" (`pipeline`), bao gồm một chuỗi các máy chuyển đổi (`transformer`) và một công cụ ước tính (`estimator`).


### Các tham số hàm dựng

* $transformers (array|Transformer[]) - chuỗi các đối tượng máy chuyển đổi (`transformer`) được implements (sử dụng interface)
* $estimator (Estimator) - công cụ ước tính có thể học (`train`) và dự đoán (`predict`)

```
use Phpml\Classification\SVC;
use Phpml\FeatureExtraction\TfIdfTransformer;
use Phpml\Pipeline;

$transformers = [
    new TfIdfTransformer(),
];
$estimator = new SVC();

$pipeline = new Pipeline($transformers, $estimator);
```

### Example

Đầu tiên, pipeline sẽ thay thế các giá trị bị thiếu, tiếp theo là chuẩn hóa dữ liệu và cuối cùng là thực thiện train cho mô hình ước tính SVC. Từ đó, pipeline đã được chuẩn bị sẽ tiếp hành lặp lại các bước chuyển đổi cho mẫu cần dự đoán.

```
use Phpml\Classification\SVC;
use Phpml\Pipeline;
use Phpml\Preprocessing\Imputer;
use Phpml\Preprocessing\Normalizer;
use Phpml\Preprocessing\Imputer\Strategy\MostFrequentStrategy;

$transformers = [
    new Imputer(null, new MostFrequentStrategy()),
    new Normalizer(),
];
$estimator = new SVC();

$samples = [
    [1, -1, 2],
    [2, 0, null],
    [null, 1, -1],
];

$targets = [
    4,
    1,
    4,
];

$pipeline = new Pipeline($transformers, $estimator);
$pipeline->train($samples, $targets);

$predicted = $pipeline->predict([[0, 0, 0]]);

// $predicted == 4
```
