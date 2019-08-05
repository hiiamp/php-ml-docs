# Random Split

Hay còn gọi là phương pháp "Hold-out", đây là một trong những phương pháp đơn giản nhất của kiểm chứng chéo bằng cách sử dụng lớp `RandomSpilt`. Các mẫu sẽ được chia thành 2 nhóm: 1 nhóm dùng để train và nhóm còn lại dùng để test lại mô hình. Số mẫu trong mỗi nhóm có thể dễ dàng điều chỉnh.

### Các tham số hàm dựng

* $dataset - đối tượng được implements `Dataset` interface
* $testSize - tỉ lệ tách mẫu thành nhóm dùng để test (float, từ 0 đến 1, mặc định: 0.3)
* $seed - tạo mẫu ngẫu nhiên (e.g. for tests)
 
```
$randomSplit = new RandomSplit($dataset, 0.2);
```

### Samples and labels groups

Để lấy được mẫu và nhãn tương ứng của nhóm test và nhóm train, sử dụng getters như sau:

```
$dataset = new RandomSplit($dataset, 0.3, 1234);

// nhóm train
$dataset->getTrainSamples();
$dataset->getTrainLabels();

// nhóm test
$dataset->getTestSamples();
$dataset->getTestLabels();
```
