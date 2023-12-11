1. KFold
2. Stratified KFold
3. Repeated KFold
4. Repeated Stratified KFold
5. Leave One-Out
6. Leave P-Out
7. Time Series Split

# KFold
Veriyi rastgele parçalara böler ve modeli eğitmek ve test etmek için bu parçaları kullanır. Veri setini daha iyi kullanarak eğitim yapılmasını sağlar. Yavaş olabilir.
1. Veri kümesi K parçaya bölünür.
2. K parçanın her biri sırasıyla test seti olarak kullanır. Diğer k-1 parçayı eğitim seti olarak kullanır.
3. Model K kez eğitilir ve test edilir. 
4. Her bir eğitim-test işlemi sonucunda elde edilen performans ölçümleri ortalanır.

```python
from sklearn.model_selection import KFold
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
y = np.array([11, 12, 13, 14])

kf = KFold(n_splits=2)

for train_index, test_index in kf.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = LinearRegression()
    model.fit(X_train, y_train)
    
    score = model.score(X_test, y_test)
    print("Test seti skoru:", score)
```

# Stratified KFold
KFold gibi çalışır fakat her katmanın sınıf dağılımını korumak için sınıfları dengeli bir şekilde böler. Sınıf dengesizliği durumunda daha güvenilir sonuçlar sağlar. Sınıf dağılımını koruyarak her katmanda her sınıfın temsil edilmesini sağlar. Stratifikasyon her zaman mümkün olmayabilir.
1. Veri kümesi k parçaya bölünür
2. Her bir parçanın sınıf dağılımını KFold gibi böler.
3. Her parça, orijinal veri setindeki sınıf oranlarını yansıtacak şekilde oluşturulur.
4. Model K kez eğitilir ve test edilir, her seferinde farklı bir parça test seti olarak seçilir.

```python
from sklearn.model_selection import StratifiedKFold
from sklearn.datasets import make_classification
from sklearn.linear_model import LogisticRegression

X, y = make_classification(n_samples=100, n_features=4, n_informative=2, n_redundant=0, random_state=42, n_classes=2)

skf = StratifiedKFold(n_splits=3)

for train_index, test_index in skf.split(X, y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = LogisticRegression()
    model.fit(X_train, y_train)
    
    score = model.score(X_test, y_test)
    print("Test seti skoru:", score)
```

# Repeated KFold
Veri kümesini KFold yöntemiyle bölmenin tekrarlanabilir bir versiyonudur. Bir KFold çapraz doğrulama işlemini belirli bir sayıda tekrarlayarak daha güvenilir bir performans tahmini elde etmeyi amaçlar. Veri kümesi dengeli ise gereksiz olabilir.
1. Veri kümesi k parçaya bölünür.
2. Bu K parçayı kullanarak model eğitilir ve test edilir.
3. İşlem belirli bir sayıda tekrarlanır.
4. Her tekrarda farklı rastgele parçalar seçilir.

```python
from sklearn.model_selection import RepeatedKFold
from sklearn.datasets import make_regression
from sklearn.linear_model import LinearRegression

X, y = make_regression(n_samples=100, n_features=2, noise=0.1, random_state=42)

rkf = RepeatedKFold(n_splits=3, n_repeats=2)

for train_index, test_index in rkf.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = LinearRegression()
    model.fit(X_train, y_train)
    
    score = model.score(X_test, y_test)
    print("Test seti skoru:", score)
```

# Repeated Stratified KFold
StratifiedKFold'un tekrarlanabilir bir versiyonudur. Sınıflandırma problemlerinde kullanılan ve sınıf dengesini koruyarak veri setini tekrarlayan bir çapraz doğrulama tekniğidir.
1. Veri kümesi StratifiedKFold gibi sınıf dengesini koruyarak K parçaya bölünür.
2. Bu K parçayı kullanarak modeli eğitir ve test eder.
3. İşlem belirli bir sayıda tekrarlanır.
4. Her tekrarda farklı rastgele parçalar seçilir.

```python
from sklearn.model_selection import RepeatedStratifiedKFold
from sklearn.datasets import make_classification
from sklearn.ensemble import RandomForestClassifier

X, y = make_classification(n_samples=100, n_features=4, n_informative=2, n_redundant=0, random_state=42, n_classes=2)

rskf = RepeatedStratifiedKFold(n_splits=3, n_repeats=2, random_state=42)

for train_index, test_index in rskf.split(X, y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = RandomForestClassifier()
    model.fit(X_train, y_train)
    
    score = model.score(X_test, y_test)
    print("Test seti skoru:", score)
```

# Leave One-Out
Veri setinin her bir örneğini sadece bir kez test seti olarak kullanarak gerçekleştirilir. Her bir veri noktası sırasıyla test edilirken geri kalanı eğitim seti olarak kullanılır. 
1. Veri kümesi içindeki her bir örnek sırayla test seti olarak seçilir.
2. Seçilen örnek dışındaki tüm veri eğitim seti olarak kullanılır.
3. Model, seçilen örneği test etmek ve performansını ölçmek için eğitilir.
4. Bu işlem tüm veri noktaları için tekrarlanır

```python
from sklearn.model_selection import LeaveOneOut
from sklearn.datasets import load_iris
from sklearn.neighbors import KNeighborsClassifier

iris = load_iris()
X = iris.data
y = iris.target

loo = LeaveOneOut()

accuracies = []
for train_index, test_index in loo.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = KNeighborsClassifier()
    model.fit(X_train, y_train)
    
    accuracy = model.score(X_test, y_test)
    accuracies.append(accuracy)

mean_accuracy = sum(accuracies) / len(accuracies)
print("Ortalama doğruluk:", mean_accuracy)
```

# Leave P-Out
Her bir iterasyonda P öğeyi test seti olarak kullanarak gerçekleştirilir. LOO (Leave One-Out) ve KFold'un genelleştirilmiş bir versiyonudur. LOO, P=1 olduğunda Leave P-Out'a eşittir.
1. Veri kümesinde P öğeyi test seti olarak bırakır, geri kalanını eğitim seti olarak kullanır.
2. Model, test setindeki öğeleri tahmin etmek ve performansını ölçmek için eğitilir.
3. Bu işlem veri kümesindeki her bir P öğesi için tekrarlanır.

```python
from sklearn.model_selection import LeavePOut
from sklearn.datasets import load_iris
from sklearn.neighbors import KNeighborsClassifier

iris = load_iris()
X = iris.data
y = iris.target

lpout = LeavePOut(p=2)

accuracies = []
for train_index, test_index in lpout.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model = KNeighborsClassifier()
    model.fit(X_train, y_train)
    
    accuracy = model.score(X_test, y_test)
    accuracies.append(accuracy)

mean_accuracy = sum(accuracies) / len(accuracies)
print("Ortalama doğruluk:", mean_accuracy)
```

# Time Series Split
Zaman serisi veri setlerinde kullanılan çapraz doğrulama yöntemlerinden biridir. Zaman serileri için veriyi bölme ve çapraz doğrulama yapma işlemidir. 
1. Veri, kronolojik sıraya göre (zaman bileşeni) parçalara bölünür.
2. Her bir bölüm, eğitim ve test setleri olarak kullanılır.
3. Örneğin, ilk k-1 bölüm eğitim seti, k. bölüm test seti olarak kullanılabilir.
4. Bu işlem bir döngü içinde tekrarlanarak farklı eğitim ve test setleri elde edilir.

```python
from sklearn.model_selection import TimeSeriesSplit
import numpy as np

time_series = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

tscv = TimeSeriesSplit(n_splits=3)

for train_index, test_index in tscv.split(time_series):
    train_data, test_data = time_series[train_index], time_series[test_index]
    
    print("Eğitim seti:", train_data)
    print("Test seti:", test_data)
    print("------")
```