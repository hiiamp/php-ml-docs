# K-means clustering

Trong thuật toán K-means clustering, chúng ta không biết nhãn (label) của từng điểm dữ liệu. Mục đích là làm thể nào để phân dữ liệu thành các cụm (cluster) khác nhau sao cho dữ liệu trong cùng một cụm có tính chất giống nhau.
Thuật toán yêu cầu chỉ định số cụm dữ liệu cần phân tách.

### Các tham số hàm dựng

* $clustersNumber - Số cụm dữ liệu cần phân tách
* $initialization - Phương thức khởi tạo, mặc định là kmeans++ (xem ở cuối)

```
$kmeans = new KMeans(2);
$kmeans = new KMeans(4, KMeans::INIT_RANDOM);
```

### Clustering

Để chia mẫu thành các cụm, ta sử dụng phương thức `cluster`. Phương thức này trả về kiểu `array` của các cụm đã được chia với các mẫu bên trong.

```
$samples = [[1, 1], [8, 7], [1, 2], [7, 8], [2, 1], [8, 9]];
Hoặc có thể gán nhãn theo cho từng mẫu bằng cách khai báo mảng như sau:
$samples = [ 'Label1' => [1, 1], 'Label2' => [8, 7], 'Label3' => [1, 2]];

$kmeans = new KMeans(2);
$kmeans->cluster($samples);
// return [0=>[[1, 1], ...], 1=>[[8, 7], ...]] or [0=>['Label1' => [1, 1], 'Label3' => [1, 2], ...], 1=>['Label2' => [8, 7], ...]]
```

### Phương thức khởi tạo

#### kmeans++ (mặc định)

K-means++ là phương pháp chọn trung tâm các cụm ban đầu cho phân cụm k-mean theo cách thông minh nhằm tăng tốc độ hội tụ.
Sử dụng phương pháp tạo ra các DASV bao gồm việc tìm trọng tâm ban đầu tốt cho các cụm.

#### random

Phương thức này chọn ra các trọng tâm hoàn toàn ngẫu nhiên cho các cụm. Sử dụng ranh giới không gian đã được tính toán để đảm bảo không đặt trọng tâm của cụm quá xa dữ liệu mẫu.