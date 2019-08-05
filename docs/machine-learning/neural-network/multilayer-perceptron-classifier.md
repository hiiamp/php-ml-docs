# MLPClassifier

Mô hình đa lớp perceptron (multilayer perceptron - MLP) có thể xem như là một mô hình mạng thần kinh lan truyền, nó ánh xạ các tập hợp dữ liệu đầu vào đến các tập hợp dữ liệu kết quả đầu ra tương ứng.

## Các tham số hàm dựng

* $inputLayerFeatures (int) - số lượng các tính năng của lớp đầu vào
* $hiddenLayers (array) - mảng tùy chỉnh cấu hình cho các lớp ẩn (hidden layer), mỗi giá trị đại diện cho số lượng tế bào thần kinh trong mỗi lớp
* $classes (array) - mảng chứa tập hợp các nhãn của các lớp được training (không được sử dụng mảng với key)
* $iterations (int) - số lần lặp lại việc training
* $learningRate (float) - tỉ lệ học
* $activationFunction (ActivationFunction) - hàm xác thực neuron (có tác dụng chuẩn hóa output)

```
use Phpml\Classification\MLPClassifier;
$mlp = new MLPClassifier(4, [2], ['a', 'b', 'c']);

// 4 nút trong lớp đầu vào, 2 nút trong lớp ẩn đầu tiên và 3 nhãn có thể.

```

Chúng ta cũng có thể sử dụng hàm xác thực neuron (`ActivationFunction`) để chuẩn hóa output cho mỗi lớp ẩn riêng lẻ. Ví dụ:

```
use Phpml\NeuralNetwork\ActivationFunction\PReLU;
use Phpml\NeuralNetwork\ActivationFunction\Sigmoid;
$mlp = new MLPClassifier(4, [[2, new PReLU], [2, new Sigmoid]], ['a', 'b', 'c']);
```

Thay vì sử dụng mảng để tùy chỉnh cho mỗi lớp ẩn như cách trên, ta có thể sử dụng mảng các đối tượng được khởi tạo trước đó để thay thế. Ví dụ:

```
use Phpml\NeuralNetwork\Layer;
use Phpml\NeuralNetwork\Node\Neuron;
$layer1 = new Layer(2, Neuron::class, new PReLU);
$layer2 = new Layer(2, Neuron::class, new Sigmoid);
$mlp = new MLPClassifier(4, [$layer1, $layer2], ['a', 'b', 'c']);
```

## Train

Để train cho một MLP, ta cung cấp cho nó mẫu và nhãn tương ứng (dưới dạng array). Ví dụ:


```
$mlp->train(
    $samples = [[1, 0, 0, 0], [0, 1, 1, 0], [1, 1, 1, 1], [0, 0, 0, 0]],
    $targets = ['a', 'a', 'b', 'c']
);
```

Sử dụng phương thức partialTrain để train theo nhiều đợt. Ví dụ:

```
$mlp->partialTrain(
    $samples = [[1, 0, 0, 0], [0, 1, 1, 0]],
    $targets = ['a', 'a']
);
$mlp->partialTrain(
    $samples = [[1, 1, 1, 1], [0, 0, 0, 0]],
    $targets = ['b', 'c']
);

```

Tỉ lệ học (`learningRate`) có thể được cập nhật giữa các lần chạy partialTrain:

```
$mlp->setLearningRate(0.1);
```

## Predict

Để dự đoán nhãn của mẫu ta sử dụng phương thức `predict`. Có thể dự đoán một mẫu hoặc nhiều mẫu cùng lúc bằng cách sử dụng `array` như sau:

```
$mlp->predict([[1, 1, 1, 1], [0, 0, 0, 0]]);
// return ['b', 'c'];

```

## Activation Functions

* BinaryStep
* Gaussian
* HyperbolicTangent
* Parametric Rectified Linear Unit
* Sigmoid (default)
* Thresholded Rectified Linear Unit
