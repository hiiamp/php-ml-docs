# DBSCAN clustering

Đây là giải thuật phân cụm dựa trên mật độ: đặt một tập hợp điểm trong không gian, giải thuật sẽ kết hợp các điêm có quan hệ chặt chẽ với nhau (các điểm với nhiều mối quan hệ, đặc điểm (gần) giống nhau), các điểm nằm ở vùng có mật độ thấp được xem như là nhiễu (có điểm lân cận ở quá xa so với khoảng cách tối thiểu được quy định trong giải thuật). DBSCAN là một trong những thuật toán phân cụm phổ biến nhất và cũng được trích dẫn nhiều nhất trong tài liệu khoa học.

### Các tham số hàm dựng

* $epsilon - epsilon, khoảng cách lớn nhất giữa hai mẫu mà chúng có thể được xem như là thuộc cùng một cụm
* $minSamples - số lượng điểm mẫu tối thiểu quanh một điểm được xem là đặc trưng cho cụm để cụm đó không bị xem là nhiễu (bao gồm cả điểm được xem là đặc trưng)
* $distanceMetric - Đối tượng khoảng cách, mặc định là Euclidean (xem thêm tại [distance documentation](../../math/distance.md))

```
$dbscan = new DBSCAN($epsilon = 2, $minSamples = 3);
$dbscan = new DBSCAN($epsilon = 2, $minSamples = 3, new Minkowski($lambda=4));
```

### Clustering

Để chia mẫu thành các cụm, ta sử dụng phương thức `cluster`. Phương thức này trả về kiểu `array` của các cụm đã được chia với các mẫu bên trong.

```
$samples = [[1, 1], [8, 7], [1, 2], [7, 8], [2, 1], [8, 9]];

$dbscan = new DBSCAN($epsilon = 2, $minSamples = 3);
$dbscan->cluster($samples);
// return [0=>[[1, 1], ...], 1=>[[8, 7], ...]] 
```
