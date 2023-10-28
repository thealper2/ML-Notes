# Tukey's IQR Method
IQR (Interquartile Range) methodu, veri dağılımının merkezi eğilimini ve dağılımın yayılmasını analiz etmek için kullanılan bir istatistiksel yöntemdir. Bu yöntem, aykırı değerleri tanımlamak ve ele almak için sıkça kullanılır. 

IQR, verinin üçüncü çeyrek (Q3) ile birinci çeyrek (Q1) arasındaki farkı temsil eder. IQR, veri dağılımının merkezi eğilimini ve dağılımın yayılmasını belirlemeye yardımcı olur. Birinci çeyrek (Q1), verinin alt yarısının (25. persentil) merkezi değeri. Üçüncü çeyrek (Q3), verinin üst yarısının (75. persentil) merkezi değeri. Eğer veri setinde bu alt sınırın altındaki değerler veya üst sınırın üstündeki değerler bulunuyorsa, bu değerler aykırı değerler olarak kabul edilir.

```shell
IQR = Q3 - Q1
1. Alt Sınır: Q1 - 1.5 * IQR
2. üst Sınır: Q3 + 1.5 * IQR
```

```python
import numpy as np

data = np.array([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# IQR hesaplama
q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)
iqr = q3 - q1

# Alt sınır ve üst sınır hesaplama
lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

# Aykırı değerleri belirleme
outliers = data[(data < lower_bound) | (data > upper_bound)]

print("IQR:", iqr)
print("Alt Sınır:", lower_bound)
print("Üst Sınır:", upper_bound)
print("Aykırı Değerler:", outliers)
```

---
# Standard Deviation Method
Standart sapma (standard deviation) veya z-skor metodu olarak bilinir. Bu mtot, veri noktalarının ortalama değerine göre ne kadar sapma gösterdiğini analiz eder ve bu sapmaları kullanarak aykırı değerleri tanımlar. Standart sapma, veri noktalarının ortalama etrafındaki dağılımı ölçer. Yüksek bir standart sapma, veri noktalarının ortalama etrafında daha fazla yayıldığını gösterir.

```python
import numpy as np

data = np.array([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# Verilerin ortalama ve standart sapmasını hesaplama
mean = np.mean(data)
std_dev = np.std(data)

# Aykırı değerleri belirleme (örneğin, ±2 standart sapma sınırını kullanabiliriz)
lower_bound = mean - 2 * std_dev
upper_bound = mean + 2 * std_dev

outliers = data[(data < lower_bound) | (data > upper_bound)]

print("Ortalama:", mean)
print("Standart Sapma:", std_dev)
print("Alt Sınır:", lower_bound)
print("Üst Sınır:", upper_bound)
print("Aykırı Değerler:", outliers)
```

---
# Z-Score Method
Z-skor metodu, aykırı değerleri tespit etmek ve değerlerin ortalama etrafındaki sapmalarını ölçmek için kullanılan bir istatistiksel yöntemdir. Bu yöntem, bir veri noktasının, ortalama etrafındaki sapmasını standart sapma birimleri cinsinden ifade eder. Bir veri noktasının z-skoru, o noktanın veri setinin noktalama değerinden ne kadar sapma gösterdiğini standart sapma birimleri cinsinden ifade eder. Z-skor, genellikle bir normal dağılıma (ortalama=0, standart sapma=1) dönüştürülür. Dolayısıyla, Z-skorları kullanarak bir veri noktasının hangi yüzde dilimine veya persentile ait olduğu belirlenebilir. Örneğin, Z-skoru -2.0 olan bir değer, veri setinin altındaki %2.5'lik dilimde yer alır.

```python
import numpy as np
from scipy import stats

data = np.array([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# Verilerin ortalama ve standart sapmasını hesaplama
mean = np.mean(data)
std_dev = np.std(data)

# Z-skorları hesaplama
z_scores = (data - mean) / std_dev

# Aykırı değerleri belirleme (örneğin, Z-skor ±2 sınırını kullanabiliriz)
threshold = 2
outliers = data[np.abs(z_scores) > threshold]

print("Ortalama:", mean)
print("Standart Sapma:", std_dev)
print("Aykırı Değerler:", outliers)
```

---
# Modified Z-Score Method
Modified Z-score metodu, Z-skor yöntemine benzer bir aykırı değer tespit yöntemidir; ancak veri setinin normal dağılımını varsayımını zorlamaz. Bu yöntem, Z-skorlara benzer bir hesaplama kullanırken, medyanı ve medyan kesintiye dayalı olarak aykırı değerleri tanımlar. Modified Z-score, veri setindeki standard sapmayı ölçer ve bu sapma değerlerini aykırı değerleri tanımlamak için kullanır. Modified Z-score hesaplandığında, tipik olarak bir eşik değeri belirlenir (örneğin, 3.5 veya 2.0 gibi). Bu eşik değerini aşan veya altına inen Modified Z-skorları, aykırı değerler olarak kabul edilir.

```python
import numpy as np

data = np.array([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# Verilerin medyanını hesaplama
median = np.median(data)

# Medyan Kesintisini Hesaplama (MAD)
mad = np.median(np.abs(data - median))

# Modified Z-score hesaplama
threshold = 3.5  # Aykırı değer eşik değeri
modified_z_scores = 0.6745 * (data - median) / mad

# Aykırı değerleri belirleme
outliers = data[np.abs(modified_z_scores) > threshold]

print("Medyan:", median)
print("MAD (Median Absolute Deviation):", mad)
print("Aykırı Değerler:", outliers)
```

---
# Isolation Forest 
Isolation Forest, aykırı değerleri tespit etmek için kullanılan bir makine öğrenimi algoritmasıdır. Bu algoritma, veri noktalarını izole ederek aykırı değerleri tanımlar. Isolation Forest, verilerin normal gözlemlerden daha hızlı ve kolay bir şekilde izole edilmesini sağlar. Bu nedenle büyük veri setleri üzerinde etkili bir şekilde çalışabilir. Isolation Forest, bir ağaç yapısı kullanarak veri noktalarını izole eder. Bu ağaç, rastgele veri noktalarını bölen ve böldüğü kısmın büyüklüğüne göre aykırı değerlerin izolasyon derecesini ölçen bir yapıdır. Aykırı değerler, daha az bölünmüş veya yüksek bir izolasyon derecesine sahip olan yapraklada bulunma eğilimindedirler. 

```python
from sklearn.ensemble import IsolationForest

data = [
    [15], [18], [19], [20],
    [21], [22], [24], [28],
    [29], [30], [35], [40],
    [200]
]

# contamination, aykırı değerlerin oranı
clf = IsolationForest(contamination=0.05)
clf.fit(data)

outliers = clf.predict(data)

# Aykırı değerlerin indekslerini bulma
outlier_indices = [i for i, prediction in enumerate(outliers) if prediction == -1]
print("Aykırı Değerlerin İndeksleri:", outlier_indices)
```

---
# DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

DBSCAN (Density-Based Spatial Clustering of Applications with Noise), veri madenciliği ve kümeleme problemleri için kullanılan bir kümeleme algoritmasıdır. DBSCAN, yoğunluk temelli bir yaklaşımı benimser ve aykırı değerleri tespit etmek için kullanılabilir. Algoritma, veri noktalarının yoğun bölgelerini ve bu bölgelerden uzakta kalan noktaları tanımlar. Aykırı değerler, yoğun bölgelerin dışında kalan noktalar olarak kabul edilir. DBSCAN, veri noktalarını iki temel parametre kullanarak sınıflandırır: epsilon (ε) ve minimum nokta sayısı (MinPts). Bu iki parametre, DBSCAN'in aykırı değerleri belirleme yeteneğini belirler. Aykırı değerler, yoğunluk tabanlı bir yaklaşım kullanılarak tespit edilir. DBSCAN algoritması, bir veri noktasının "çekirdek nokta" olup olmadığını belirlemek için kullanılır. Bir noktanın çekirdek nokta olabilmesi için, epsilon mesafesi içinde en az MinPts sayısında diğer noktaları içermesi gerekir. Aykırı değerler, bu kriteri karşılayamayan noktalar olarak kabul edilir.

```python
from sklearn.cluster import DBSCAN
import numpy as np

data = np.array([[1, 2], [2, 2], [2, 3], [8, 7], [8, 8], [25, 25]])

dbscan = DBSCAN(eps=3, min_samples=2)
dbscan.fit(data)

# Aykırı değerlerin indekslerini bulma
outlier_indices = np.where(dbscan.labels_ == -1)
print("Aykırı Değerlerin İndeksleri:", outlier_indices)
```

---
# Local Outliar Factor (LOF)
LOF, aykırı değerleri tespit etmek için kullanılan bir yoğunluk tabanlı algoritmadır. LOF, bir veri noktasının lokal yoğunluğunu hesaplar ve bu lokal yoğunluğun, çevresindeki diğer noktalardan ne kadar farklı olduğunu ölçer. Aykırı değerler, diğer noktalardan belirgin bir şekilde yoğunluklara sahip olan noktalar olarak kabul edilir. LOF, bu nedenle, veri noktalarını çevresel yoğunluklarına göre sıralar ve aykırı değerleri tanımlar. LOF, bir veri noktasının çevresel yoğunluğunu KNN algoritması kullanarak hesaplar. Daha sonra bu çevresel yoğunluğu, diğer noktalardan sapma ile karşılaştırır ve aykırı değer olarak tanımlar.

```python
from sklearn.neighbors import LocalOutlierFactor
import numpy as np

data = np.array([[1, 2], [2, 2], [2, 3], [8, 7], [8, 8], [25, 25]])

# LOF modeli oluşturma
lof = LocalOutlierFactor(n_neighbors=3)  # K komşuların sayısı

# Modeli veriye uydurma ve aykırı değerleri tespit etme
outliers = lof.fit_predict(data)

# Aykırı değerlerin indekslerini bulma
outlier_indices = np.where(outliers == -1)
print("Aykırı Değerlerin İndeksleri:", outlier_indices)
```

---
# Winsorization Method
Winsorization, aykırı değerleri ele almak ve sınırlandırmak için kullanılan bir yöntemdir. Bu yöntemde, belirli bir yüzdelik dilimi temsil eden alt ve üst sınırlar belirlenir ve bu sınırlar dışındaki değerler, sınırların kendisi ile değiştirilir. Winsorization, veri setinin uç değerlerini sınırlandırarak aykırı değerlerin etkisini azaltmayı amaçlar. Winsorization, aykırı değerleri tespit etmek yerine sınırlamak amacıyla kullanılır. Alt ve üst sınırlar belirlenir ve bu sınırlar dışındaki değerler, sınırların kendisi ile değiştirilir. Bu, veri setinin uç değerlerinin etkisini azaltmaya yardımcı olabilir. Winsorization için kesme noktaları (alt ve üst sınırlar) belirlenir ve bu sınırlar dışındaki değerler, sınırların kendisi ile değiştirilir.

```shell
IQR = Q3 - Q1
1. Alt Sınır: Q1 - k * IQR
2. üst Sınır: Q3 + k * IQR
```

```python
import numpy as np

data = np.array([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# Winsorization için alt ve üst sınırları belirleme
k = 1.5  # Katsayı (genellikle 1.5 veya 2 kullanılır)
q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)
iqr = q3 - q1
lower_bound = q1 - k * iqr
upper_bound = q3 + k * iqr

# Alt ve üst sınırlar dışındaki değerleri sınırlarla değiştirme
data[data < lower_bound] = lower_bound
data[data > upper_bound] = upper_bound

print("Alt Sınır:", lower_bound)
print("Üst Sınır:", upper_bound)
print("Winsorized Veri:", data)
```

---

# Pandas - Rank Function
**pandas** kütüphanesindeki **rank** fonksiyonu, bir veri serisindeki değerleri sıralamak ve sıralama bilgilerini döndürmek için kullanılır. Bu sıralama bilgilerini kullanarak aykırı değerleri belirlemek veya sıralamaya dayalı analizler yapmak mümkün olur. Özellikle veri serilerinin sıralama sırasında hangi pozisyonda olduğunu anlamak için faydalıdır.

```python
import pandas as pd

data = pd.Series([15, 18, 19, 20, 21, 22, 24, 28, 29, 30, 35, 40, 200])

# Değerleri sıralama
ranked_data = data.rank()

# Aykırı değerleri belirleme için sıra sınırlarını belirleme
q1 = data.quantile(0.25)
q3 = data.quantile(0.75)
iqr = q3 - q1

lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

# Aykırı değerleri belirleme
outliers = data[(ranked_data < 2) | (ranked_data > len(data) - 1)]
print("Alt Sınır:", lower_bound)
print("Üst Sınır:", upper_bound)
print("Aykırı Değerler:", outliers)
```

---
# Mahalanobis Distance
Mahalanobis Uzaklığı (Mahalanobis Distance), aykırı değerleri tespit etmek ve çok boyutlu veri setlerinde veri noktalarının bir merkeze olan uzaklığını ölçmek için kullanılan bir istatistiksel yöntemdir. Bu yöntem, veri noktalarının dağılımının ve kovaryans matrisinin bilgisini kullanır. Mahalanobis Uzaklığı, aykırı değerleri tespit etmek için kullanıldığında, veri noktalarının merkeze olan uzaklığını standart sapma birimleri ile ölçer.

```python
import numpy as np
from scipy.spatial import distance

data = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9],
                 [10, 11, 12],
                 [13, 14, 15]])

# Merkez (ortalama vektör) hesaplama
mean_vector = np.mean(data, axis=0)

# Kovaryans matrisini hesaplama
covariance_matrix = np.cov(data, rowvar=False)

# Hedef veri noktasını belirleme
target_point = np.array([8, 9, 10])

# Mahalanobis Uzaklığını hesaplama
mahalanobis_distance = distance.mahalanobis(target_point, mean_vector, np.linalg.inv(covariance_matrix))
print("Mahalanobis Uzaklığı:", mahalanobis_distance)
```

---
# One-Class SVM
One-Class SVM (One-Class Support Vector Machine), aykırı değer tespiti için kullanılan bir makine öğrenimi algoritmasıdır. Bu yöntem, bir veri kümesinin çoğunluğundan farklı olan ve nadiren bulunan aykırı değerleri tanımlamak amacıyla kullanılır. One-Class SVM, veri kümesinin normal bölgesini yakalamak ve bu bölge dışında kalan noktaları aykırı değer olarak tanımlamak için bir sınıflandırma yaklaşımı kullanır. One-Class SVM, normal gözlemleri temsil eden bir hiper-düzlem (SVM düzlemi) oluşturur. Bu düzlem, veri noktalarının çoğunluğunu içerir ve aykırı değerler bu düzlemin dışında kalır. One-Class SVM, bu denklemin çözülmesi yoluyla hiper-düzlemi tanımlar ve aykırı değerleri tanımlamak için bu düzlemin dışındaki gözlemleri tespit eder.

```python
from sklearn.svm import OneClassSVM
import numpy as np

data = np.array([1, 2, 2, 3, 3, 3, 4, 4, 5, 10, 12, 12, 13])

# One-Class SVM modeli oluşturma
nu = 0.1  # Normal gözlemlerin oranı
svm = OneClassSVM(kernel="rbf", nu=nu)

# Modeli veriye uydurma
svm.fit(data.reshape(-1, 1))

# Aykırı değerleri tespit etme
outliers = data[svm.predict(data.reshape(-1, 1)) == -1]
print("Aykırı Değerler:", outliers)
```

---
# Robust Principal Component Analysis (RPCA) 
Robust Principal Component Analysis (RPCA), aykırı değerleri tespit etmek ve veri setini bileşenlere ayırırken aykırı değerlerden etkilenmemek için kullanılan bir tekniktir. RPCA, özellikle çok boyutlu veri setlerinde aykırı değerleri tespit etmek için etkilidir ve bileşen analizi ile aykırı değerleri ayırmak için kullanılır. RPCA, veri matrisini düşük rütbeli ve aykırı bileşenlere ayırır. RPCA, veri matrisini düşük rütbeli bileşenler (L) ve aykırı değerler (S) olarak iki farklı bileşenlere böler. Bu işlem, veri matrisindeki aykırı değerlerin diğer bileşenlerden izole edilmesini sağlar.

```python
import numpy as np
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_multilabel_classification

# Veri seti örneği
data, _ = make_multilabel_classification(n_samples=100, n_features=5, n_classes=2, n_labels=2, n_clusters_per_class=1, random_state=42)

# Veriyi standartlaştırma
scaler = StandardScaler()
data = scaler.fit_transform(data)

# RPCA modeli oluşturma
pca = PCA(n_components=2)
pca.fit(data)

# Aykırı değerleri tespit etme
outliers = data[pca.explained_variance_ratio_ < 0.01]
print("Aykırı Değerler:", outliers)
```