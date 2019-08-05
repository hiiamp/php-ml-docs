# PHP-ML - Thư viện Machine Learning cho PHP

[![Minimum PHP Version](https://img.shields.io/badge/php-%3E%3D%207.2-8892BF.svg)](https://php.net/)
[![Latest Stable Version](https://img.shields.io/packagist/v/php-ai/php-ml.svg)](https://packagist.org/packages/php-ai/php-ml)
[![Build Status](https://travis-ci.org/php-ai/php-ml.svg?branch=master)](https://travis-ci.org/php-ai/php-ml)
[![Documentation Status](https://readthedocs.org/projects/php-ml/badge/?version=master)](http://php-ml.readthedocs.org/)
[![Total Downloads](https://poser.pugx.org/php-ai/php-ml/downloads.svg)](https://packagist.org/packages/php-ai/php-ml)
[![License](https://poser.pugx.org/php-ai/php-ml/license.svg)](https://packagist.org/packages/php-ai/php-ml)
[![Coverage Status](https://coveralls.io/repos/github/php-ai/php-ml/badge.svg?branch=master)](https://coveralls.io/github/php-ai/php-ml?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/php-ai/php-ml/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/php-ai/php-ml/?branch=master)

<p align="center">
	<img src="https://github.com/php-ai/php-ml/raw/master/docs/assets/php-ml-logo.png" />
</p>

Thư viện này là một cách tiếp cận Machine Learning hoàn toàn mới trên ngôn ngữ PHP.
Thư viện hỗ trợ các thuật toán, kiểm chứng chéo (Cross Validation), mạng thần kinh (Neural Network), tiền xử lý, chuẩn hóa dữ liệu và nhiều hơn nữa.

PHP-ML yêu cầu phiên bản PHP >= 7.2.

Một ví dụ đơn giản về phân lớp (classification):
```php
require_once __DIR__ . '/vendor/autoload.php';

use Phpml\Classification\KNearestNeighbors;

$samples = [[1, 3], [1, 4], [2, 4], [3, 1], [4, 1], [4, 2]];
$labels = ['a', 'a', 'a', 'b', 'b', 'b'];

$classifier = new KNearestNeighbors();
$classifier->train($samples, $labels);

$classifier->predict([3, 2]);
// return 'b'
```

## Các giải thưởng

<a href="http://www.yegor256.com/2016/10/23/award-2017.html">
  <img src="http://www.yegor256.com/images/award/2017/winner-itcraftsmanpl.png" width="400"/></a>

## Tài liệu

Đọc tài liệu gốc (tiếng anh) tại [Documentation](http://php-ml.readthedocs.org/).

## Cài đặt

Hiện tại thư viện vẫn đang trong quá trình phát triển, tuy nhiên bạn có thể cài đặt nó với composer:

```
composer require php-ai/php-ml
```

## Ví dụ

Truy cập vào repo sau để xem ví dụ mẫu [php-ai/php-ml-examples](https://github.com/php-ai/php-ml-examples).

## Các tính năng

* Association rule Learning - Máy học xử lý quy luật của mẫu
    * [Apriori](machine-learning/association/apriori.md)
* Classification - Phân loại
    * [SVC](machine-learning/classification/svc.md)
    * [k-Nearest Neighbors](machine-learning/classification/k-nearest-neighbors.md)
    * [Naive Bayes](machine-learning/classification/naive-bayes.md)
* Regression - Hồi quy
    * [Least Squares](machine-learning/regression/least-squares.md)
    * [SVR](machine-learning/regression/svr.md)
* Clustering - Phân cụm
    * [k-Means](machine-learning/clustering/k-means.md)
    * [DBSCAN](machine-learning/clustering/dbscan.md)
* Metric - Tính đoán độ chính xác
    * [Accuracy](machine-learning/metric/accuracy.md)
    * [Confusion Matrix](machine-learning/metric/confusion-matrix.md)
    * [Classification Report](machine-learning/metric/classification-report.md)
* Workflow - Luồng làm việc
    * [Pipeline](machine-learning/workflow/pipeline)
* Neural Network - Mạng thần kinh
    * [Multilayer Perceptron Classifier](machine-learning/neural-network/multilayer-perceptron-classifier.md)
* Cross Validation - Kiểm chứng chéo
    * [Random Split](machine-learning/cross-validation/random-split.md)
    * [Stratified Random Split](machine-learning/cross-validation/stratified-random-split.md)
* Feature Selection - Lựa chọn tính năng
    * [Variance Threshold](machine-learning/feature-selection/variance-threshold.md)
    * [SelectKBest](machine-learning/feature-selection/selectkbest.md)
* Preprocessing - Tiền xử lý
    * [Normalization](machine-learning/preprocessing/normalization.md)
    * [Imputation missing values](machine-learning/preprocessing/imputation-missing-values.md)
    * LabelEncoder
* Feature Extraction - Khai thác tính năng
    * [Token Count Vectorizer](machine-learning/feature-extraction/token-count-vectorizer.md)
    * [Tf-idf Transformer](machine-learning/feature-extraction/tf-idf-transformer.md)
* Datasets - Dữ liệu mẫu
    * [Array](machine-learning/datasets/array-dataset.md)
    * [CSV](machine-learning/datasets/csv-dataset.md)
    * [Files](machine-learning/datasets/files-dataset.md)
    * [SVM](machine-learning/datasets/svm-dataset.md)
    * [MNIST](machine-learning/datasets/mnist-dataset.md)
    * Ready to use:
        * [Iris](machine-learning/datasets/demo/iris.md)
        * [Wine](machine-learning/datasets/demo/wine.md)
        * [Glass](machine-learning/datasets/demo/glass.md)
* Models management - Quản lý mô hình
    * [Persistency](machine-learning/model-manager/persistency.md)
* Math - Toán
    * [Distance](math/distance.md)
    * [Matrix](math/matrix.md)
    * [Set](math/set.md)
    * [Statistic](math/statistic.md)


## Đóng góp và xây dựng

- Guide: [CONTRIBUTING.md](https://github.com/php-ai/php-ml/blob/master/CONTRIBUTING.md)
- Issue Tracker: [github.com/php-ai/php-ml/issues](https://github.com/php-ai/php-ml/issues)
- Source Code: [github.com/php-ai/php-ml](https://github.com/php-ai/php-ml)

You can find more about contributing in [CONTRIBUTING.md](../CONTRIBUTING.md).

## Bản quyền 

PHP-ML is released under the MIT Licence. See the bundled LICENSE file for details.

## Tác giả

Arkadiusz Kondas (@ArkadiuszKondas)

## Dịch giả

Truong Phi (@hiiamp)