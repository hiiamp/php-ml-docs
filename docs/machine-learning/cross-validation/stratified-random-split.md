# Stratified Random Split

Tương tự như `RandomSpilt`, nó cũng chia mẫu thành 2 nhóm: nhóm dùng để train and và nhóm dùng để test test.
Tuy nhiên, `StratifiedRandomSplit` cố gắng lấy mẫu test sau cho số lượng `target` (hoặc `label`) là bằng hoặc gần bằng nhau.
Số mẫu trong mỗi nhóm có thể dễ dàng điều chỉnh.

### Các tham số hàm dựng

* $dataset - đối tượng được implements `Dataset` interface
* $testSize - tỉ lệ tách mẫu thành nhóm dùng để test (float, từ 0 đến 1, mặc định: 0.3)
* $seed - tạo mẫu ngẫu nhiên (e.g. for tests)
 
```
$split = new StratifiedRandomSplit($dataset, 0.2);
```

### Samples and labels groups

Để lấy được mẫu và nhãn tương ứng của nhóm test và nhóm train, sử dụng getters như sau:

```
$dataset = new StratifiedRandomSplit($dataset, 0.3, 1234);

// nhóm train
$dataset->getTrainSamples();
$dataset->getTrainLabels();

// nhóm test
$dataset->getTestSamples();
$dataset->getTestLabels();
```

### Example

```
$dataset = new ArrayDataset(
    $samples = [[1], [2], [3], [4], [5], [6], [7], [8]],
    $targets = ['a', 'a', 'a', 'a', 'b', 'b', 'b', 'b']
);

$split = new StratifiedRandomSplit($dataset, 0.5);
```

Lượng mẫu của mỗi `target` trong `$split` sẽ bằng nhau. 2 mẫu với target `a` và 2 mẫu với target `b`.
