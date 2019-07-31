# Apriori Associator

Học mối quan hệ của các đối tượng (Association rule learning) dựa trên [Thuật toán Apriori](https://en.wikipedia.org/wiki/Apriori_algorithm) cho tần suất xuất hiện của các đối tượng trong tập hợp đang xét.

### Các tham số hàm dựng

* $support - ngưỡng tối thiểu của [support](https://en.wikipedia.org/wiki/Association_rule_learning#Support), vd: tỉ lệ mẫu chứa cả X và Y đúng với quy tắc "nếu X thì Y"
* $confidence - ngưỡng tối thiểu của [confidence - độ tin cậy](https://en.wikipedia.org/wiki/Association_rule_learning#Confidence), vd: tỉ lệ mẫu chứa cả X và Y so với mãu chứa X.

```
use Phpml\Association\Apriori;

$associator = new Apriori($support = 0.5, $confidence = 0.5);
```

### Train

Để train một associator đơn giản bằng cách cung cấp cho nó các mẫu và nhãn tương ứng (kiểu dữ liệu phải là `array`). Ví dụ:

```
$samples = [['alpha', 'beta', 'epsilon'], ['alpha', 'beta', 'theta'], ['alpha', 'beta', 'epsilon'], ['alpha', 'beta', 'theta']];
$labels  = [];

use Phpml\Association\Apriori;

$associator = new Apriori($support = 0.5, $confidence = 0.5);
$associator->train($samples, $labels);
```

Bạn có thể train cho associator bằng cách sử dụng nhiều mẫu dữ liệu, kết quả dự đoán cuối dùng sẽ dựa trên tất cả dữ liệu đã sử dụng để training.

### Predict

Để dự đoán nhãn của mẫu, ta sử dụng phương thức `predict`. Bạn có thể dự đoán cho một hoặc nhiều mẫu (array) cùng lúc:

```
$associator->predict(['alpha','theta']);
// return [['beta']]

$associator->predict([['alpha','epsilon'],['beta','theta']]);
// return [[['beta']], [['alpha']]]
```

### Associating

Để lấy được quy luật association ta có thể sử dụng phương thức `rules`.

```
$associator->getRules();
// return [['antecedent' => ['alpha', 'theta'], 'consequent' => ['beta'], 'support' => 1.0, 'confidence' => 1.0], ... ]
```

### Tần suất của các nhóm đối tượng

Để lấy tần suất của các nhóm đối tượng với k phần tử, sử dụng phương thức `apriori`.

```
$associator->apriori();
// return [ 1 => [['alpha'], ['beta'], ['theta'], ['epsilon']], 2 => [...], ...]
```
