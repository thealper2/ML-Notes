1. AffinityPropagation  
2. AgglomerativeClustering  
3. Birch  
4. DBSCAN  
5. FeatureAgglomeration  
6. KMeans  
7. MeanShift  
8. MiniBatchKMeans  
9. OPTICS  
10. SpectralClustering

---
# AffinityPropagation
Affinity Propagation, veri kümeleme (clustering) için kullanılan bir algoritmadır. Bu algoritma, özellikle verinin kendi içinde mesajlaşma (iletişim) yeteneğine dayalıdır ve her veri noktasının diğer tüm veri noktalarıyla iletişim kurduğu bir "mesajlaşma" tabanlı bir yaklaşım kullanır. Affinity Propagation algoritması şu adımları takip eder:
1. Benzerlik Matrisi Oluşturma: İlk adım, veri noktaları arasındaki benzerlikleri ölçmek ve bir benzerlik matrisi oluşturmaktır. Benzerlik matrisi, her bir veri noktasının diğer tüm veri noktalarına olan benzerlik derecesini içerir.  
2. İletişim Matrisi ve Sorumluluk Matrisi Hesaplama: Her veri noktası, diğer veri noktalarına ne kadar "mesaj göndermeli" ve ne kadar "mesaj almalı" gerektiğini hesaplar. Bu hesaplamalar, iletişim matrisi (responsibility matrix) ve sorumluluk matrisi (availability matrix) olarak adlandırılan iki matris içinde yapılır.
3. Mesajlaşma ve Güncelleme: Veri noktaları arasında mesajlaşma sürekli olarak gerçekleşir. Mesajlaşma sonucunda iletişim matrisi ve sorumluluk matrisi güncellenir.
4. Küme Merkezlerinin Belirlenmesi: Algoritma, her veri noktasının bir küme merkezi olup olmadığını belirler. Bu işlem, iletişim matrisi ve sorumluluk matrisi kullanılarak yapılır.
5. Kümeleme Sonuçlarının Elde Edilmesi: Algoritma, her veri noktasını bir küme merkezine atar ve verileri bu merkezlere göre kümelendirir.

**Avantajlar:**
- Otomatik Küme Merkezi Seçimi: Affinity Propagation, küme merkezlerini otomatik olarak belirler, bu nedenle küme sayısını önceden belirlemeniz gerekmez.
- Farklı Şekil ve Boyuttaki Kümeleme: Farklı şekil ve boyuttaki veri kümelerini tanıyabilir ve başa çıkabilir.
- Kümelerin Belirgin Olmasını Sağlar: Genellikle kümeler arasında belirgin sınırlar oluşturur.

**Dezavantajlar:**
- Hesaplama Maliyeti: Büyük veri kümeleri için hesaplama maliyeti yüksek olabilir.
- Hassas Parametre Ayarı: Algoritmanın bazı parametrelerinin hassas bir şekilde ayarlanması gerekebilir.
- Küme Merkezi Sayısını Belirlememe: Algoritma, otomatik olarak küme merkezi sayısını belirler, bu nedenle bazen beklenenden daha fazla veya daha az küme oluşabilir.

```python
from sklearn.cluster import AffinityPropagation
from sklearn.datasets import make_blobs

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# Affinity Propagation modeli oluşturma
model = AffinityPropagation()

# Veriyi modele uydurma
model.fit(data)

# Küme merkezlerini ve etiketleri al
cluster_centers_indices = model.cluster_centers_indices_
labels = model.labels_

# Küme merkezlerini ve etiketleri yazdır
print("Küme Merkezleri:")
print(data[cluster_centers_indices])
print("Küme Etiketleri:")
print(labels)
```

Affinity Propagation algoritmasının ana formülü şu iki matris üzerinde dönerek hesaplamaları içerir: iletişim matrisi (Responsibility Matrix) ve sorumluluk matrisi (Availability Matrix). Aşağıda bu matrislerin güncellenmesi ve kullanıldığı formüller verilmektedir:

1. İletişim Matrisi (Responsibility Matrix, R):

```shell
R(i, k) = S(i, k) - max[a + b, a ≠ k] {A(i, a) + S(i, a)}
```

Burada:
- i, veri noktasının indeksi
- k, veri noktasının indeksi
- S(i, k), benzerlik matrisindeki i ve k arasındaki benzerlik skoru
- A(i, a), sorumluluk matrisindeki i ve a arasındaki değer
- max[a + b, a ≠ k] {A(i, a) + S(i, a)}, i ve k hariç diğer tüm a veri noktaları için maksimum toplam

2. Sorumluluk Matrisi (Availability Matrix, A):
```
A(i, k) = min[0, R(k, k) + Σ[max(0, R(a, k)), a ≠ i and a ≠ k]]
```    

Burada:
- i, veri noktasının indeksi
- k, veri noktasının indeksi
- R(k, k), iletişim matrisindeki k'nin kendisiyle olan değer
- R(a, k), iletişim matrisindeki a ve k arasındaki değer
- Σ\[max(0, R(a, k)), a ≠ i and a ≠ k], i ve k hariç diğer tüm a veri noktaları için hesaplanan değerlerin toplamı

### Hiperparametreler

| Parameter Name | Type | Default | Description |
| - | - | - | - |
| damping | float | 0.5 | Algoritmanın güncelleme adımlarında kullanılan bir sönümleme faktörüdür. Bu faktör, matris güncellemelerinin istikrarlı hale gelmesine yardımcı olur. Genellikle [0.5, 1] arasında bir değer alır. |
| convergence_iter | int | 15 | Algoritmanın dönüşüm kriterini belirlemek için kullanılır. Belli bir iterasyon sayısına veya sonuçların değişimine dayalı olarak algoritmanın sonlandırılmasını kontrol eder. |  
| preference | array | None | İlk küme merkezi tahminleri üzerinde etkilidir. Özellikle önceden belirlenmiş bir küme sayısı kullanılmadığında, veri noktalarının küme merkezi olma olasılığını ayarlamak için kullanılır. |
| max_iter | int | 200 | Maksimum iterasyon sayısı. |

---
# AgglomerativeClustering
Agglomerative Clustering, veri kümeleme için kullanılan hiyerarşik bir kümeleme (hierarchical clustering) algoritmasıdır. Bu algoritma, veri noktalarını başlangıçta ayrı ayrı kümelere yerleştirir ve ardından bu kümeleri birleştirerek hiyerarşik bir yapı oluşturur. Agglomerative Clustering, aşağıdaki adımları izler:

1. Başlangıçta, her veri noktası ayrı bir küme olarak kabul edilir. Yani, N veri noktası için N küme oluşturulur.
2. Sonraki adımlarda, belirli bir kriteri (örneğin, mesafe veya benzerlik) kullanarak en yakın iki küme birleştirilir. Bu birleştirme işlemi, her adımda bir adet daha büyük küme oluşturur.
3. Adımlar tekrar edilir ve tüm veri noktaları tek bir büyük küme haline gelene kadar devam eder. Bu, bir hiyerarşik ağaç yapısı oluşturur.
4. Son olarak, kullanıcı belirli bir kesme noktasını veya küme sayısını seçebilir ve bu ağaç yapısını keserek kümeleme sonuçlarını alabilir.

**Avantajlar:**
- Hiyerarşik Sonuçlar: Agglomerative Clustering, hiyerarşik bir yapıda küme sonuçları sağlar. Bu, veriyi farklı düzeylerde kümelemeyi ve görselleştirmeyi kolaylaştırır.
- Basit Parametre Ayarı: Genellikle bir mesafe veya benzerlik kriteri dışında fazla hiperparametre gerektirmez.
- İşaretsiz Kümeleme: Etiketlenmemiş verilerle çalışmak için uygundur.

**Dezavantajlar:**
- Hesaplama Maliyeti: Agglomerative Clustering, büyük veri kümeleri için hesaplama maliyeti yüksek olabilir, çünkü tüm veri noktaları arasındaki mesafeleri hesaplamak gerekebilir.
- Kesme Noktası Seçimi: Hiyerarşik ağaçtan kesme noktasını belirlemek, doğru küme sayısını seçmeyi zorlaştırabilir.
- Veri Noktalarının Eşit Dağılmaması: Bazı veri noktalarının yoğun, bazılarının seyrek dağıldığı durumlarda iyi sonuçlar üretmeyebilir.

```python
from sklearn.cluster import AgglomerativeClustering
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=3, cluster_std=1.0, random_state=42)

# Agglomerative Clustering modeli oluşturma
model = AgglomerativeClustering(n_clusters=3)  # Küme sayısını belirtin

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```

Agglomerative Clustering algoritması, hiyerarşik kümeleme için kullanılan bir yöntemdir. Bu algoritma, veri noktalarını hiyerarşik bir ağaç yapısı içinde birleştirir ve bu yapıyı keserek küme sonuçlarını elde edebilirsiniz. Agglomerative Clustering'ın formülü veya matematiksel denklemi yoktur, çünkü bu bir hiyerarşik yöntemdir ve birçok farklı mesafe veya benzerlik ölçüsü kullanabilir. Ancak, algoritmanın çalışma mantığı şu adımlarla özetlenebilir:

1. Başlangıçta, her veri noktası kendi kümesine aittir. Yani N veri noktası için N küme vardır.
2. Tüm veri noktaları arasındaki mesafeleri veya benzerlikleri hesaplayın. Bu mesafeleri kullanarak en yakın iki kümenin tespit edilmesi gerekir.
3. En yakın iki küme birleştirilir ve birleşik kümenin merkezi veya temsilcisi hesaplanır.
4. Adımlar 2 ve 3 tekrarlanır ve her adımda birleşen küme sayısı azalır.
5. Bu işlem, son birleşik küme oluşana kadar devam eder ve hiyerarşik bir ağaç yapısı oluşur.
6. Kullanıcı, bir kesme kriteri kullanarak bu ağacı keser ve belirli bir küme sayısını veya belirli bir benzerlik seviyesini seçer.

### Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| n_clusters | int | 2 | Küme sayısını belirlemek için kullanılan bir hiperparametredir. Kullanıcı bu sayıyı belirtir veya veriyi gözlemleyerek seçer. |
| metric | "euclidean", "l1", "l2", "manhattan", "cosine", "precomputed" | None | Kullanılan mesafe veya benzerlik ölçüsünü belirlemek için kullanılır. |
| linkage | "ward", "complete", "average", "single" | "ward" | Küme birleştirme stratejisini belirler. Ward yöntemi, küme içi varyansları minimize etmeye çalışır. Complete-linkage, iki küme arasındaki en uzak veri noktalarının mesafesini kullanır. Average-linkage, iki küme arasındaki veri noktalarının ortalama mesafesini kullanır. |
| distance_threshold | float | None | Hiyerarşik ağaçtan kesme yaparak küme sayısını veya benzerlik seviyesini belirlemek için kullanılır. Bu eşik değerini aşan her birleşme noktası, sonuç kümelemeyi belirler.  | 

---
# Birch
BIRCH (Balanced Iterative Reducing and Clustering Using Hierarchies), veri kümeleme için kullanılan bir hiyerarşik kümeleme algoritmasıdır. BIRCH, büyük veri kümeleri üzerinde etkili bir şekilde çalışabilen bir öğrenme yöntemidir.

**Nasıl Çalışır:**
1. BIRCH, veriyi kümelemek için özel bir veri yapısı olan bir "CF-Tree" (Clustering Feature Tree) kullanır. Bu ağaç, hızlı ve etkili bir şekilde kümeleme yapmayı sağlar.
2. İlk olarak, her veri noktası birer "giriş" olarak CF-Tree'ye eklenir.
3. CF-Tree, her bir girişi temsil eden küçük bir CF (Clustering Feature) vektörü içerir. Bu vektörler, girişlerin yoğunluğu, merkezi ve varyansı gibi özellikleri özetler.
4. Girişler, CF-Tree'ye eklenirken ağaç yapısı otomatik olarak güncellenir. Ağaç birleştirmeleri ve yeniden düzenlemeleri gerçekleştirerek ağaç dengesini korur.
5. BIRCH, CF-Tree'nin yapısını kullanarak kümeleme yapar. Ağaç yapısındaki düğümler, veri noktalarını temsil eden küme merkezlerini içerir.
6. Kümeleme sonuçları, CF-Tree yapısının bir dolaşımı sırasında elde edilir.

**Avantajlar:**
- Hafif Bellek Kullanımı: BIRCH, büyük veri kümeleriyle çalışırken düşük bellek kullanımı sağlar.
- Hızlı İşlem: Özellikle veriyi sık sık güncellemek veya canlı verilerle çalışmak gerektiğinde hızlı sonuçlar sağlar.
- Hiyerarşik Sonuçlar: BIRCH, hiyerarşik bir kümeleme yapabilir ve farklı kümeleme seviyelerini incelemek için kullanılabilir.

**Dezavantajlar:**
- Küme Sayısını Belirlemekte Zorluk: Küme sayısını önceden belirlemek gerekebilir.
- Hassas Hiperparametre Ayarı: BIRCH'te bazı hiperparametrelerin hassas bir şekilde ayarlanması gerekebilir.
- Düşük Hassasiyet: Diğer bazı kümeleme algoritmalarına göre daha düşük hassasiyet sağlayabilir.

```python
from sklearn.cluster import Birch
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=3, cluster_std=1.0, random_state=42)

# BIRCH modeli oluşturma
model = Birch(threshold=0.5, n_clusters=3)  # threshold değeri ve küme sayısını belirtin

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```

### Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| threshold | float | 0.5 | CF-Tree'ye giriş eklerken kullanılan eşik değeridir. Bu değer, her düğümde kaç girişin saklanacağını ve bir düğümün alt düğümlere bölünüp bölünmeyeceğini belirler. Eşik değeri büyüdükçe ağaç daha yüzeysel olur, bu da daha fazla düğümün alt düğümlere bölünmesi anlamına gelir. Bu değeri ayarlayarak kümeleme sonuçları üzerinde büyük bir etkiye sahip olabilirsiniz. | 
| branching_factor | int | 50 | BIRCH ağacının her düğümünde kaç alt düğümün olacağını belirler. Düğüm sayısını etkiler ve yine ağacın derinliği ve genişliği üzerinde etkilidir. |
| n_clusters | int | 3 | Küme sayısını önceden belirlemeniz gereken bir hiperparametredir. | 

---
# DBSCAN
DBSCAN (Density-Based Spatial Clustering of Applications with Noise), veri madenciliği ve kümeleme için kullanılan bir kümeleme algoritmasıdır. DBSCAN, yoğunluğa dayalı bir kümeleme yöntemi olarak çalışır ve noise (gürültü) noktalarını tanıyabilir. 

**Nasıl Çalışır:**

1. DBSCAN, veri noktalarını üç farklı kategoriye ayırır:
    - **Çekirdek Noktalar (Core Points)**: Veri noktası, epsilon (ε) yarıçapı içinde en az "MinPts" komşusu varsa bir çekirdek noktasıdır.
    - **Sınırlayıcı Noktalar (Border Points)**: Veri noktası, epsilon yarıçapı içinde daha az "MinPts" komşusu olmasına rağmen bir çekirdek noktasının içindedir.
    - **Gürültü Noktaları (Noise Points)**: Veri noktası, epsilon yarıçapı içinde MinPts komşusu olmayan bir noktadır.
2. Algoritma, bir çekirdek noktadan başlar ve o noktanın epsilon yarıçapı içindeki tüm noktaları ziyaret eder. Eğer bu noktaların sayısı MinPts'ten büyükse, bir yeni küme başlatılır ve bu noktalar o kümeye atanır. Bu işlem tekrarlanarak tüm çekirdek noktalar ziyaret edilir.
3. Sınırlayıcı noktalar, bir çekirdek noktasının içinde yer alır ve ilgili çekirdek noktanın kümesine atanır.
4. Gürültü noktaları hiçbir kümeyle ilişkilendirilmez ve genellikle kümeleme sonuçlarından çıkarılır.

**Avantajlar:**
- Veri noktalarının şekil ve boyutuna duyarlı değildir, bu nedenle farklı şekil ve yoğunluğa sahip kümeleri tanıyabilir.
- Gürültüyü tanır ve gürültü noktalarını ayırt eder.
- Küme sayısını önceden belirlemek gerekmez, bu nedenle veriyi esnek bir şekilde kümeleyebilir.

**Dezavantajlar:**
- Veri noktalarının yoğunluğuna ve epsilon (ε) parametresine hassastır. Bu nedenle bu parametreleri doğru bir şekilde ayarlamak önemlidir.
- Büyük veri kümeleri için hesaplama maliyeti yüksek olabilir.
- İlk noktanın seçimi ve ziyaret sırası sonuçları etkileyebilir. Başlangıç noktası ve sıra, algoritmanın sonuçlarına bağlıdır.

```python
from sklearn.cluster import DBSCAN
from sklearn.datasets import make_moons
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_moons(n_samples=200, noise=0.05, random_state=42)

# DBSCAN modeli oluşturma
model = DBSCAN(eps=0.3, min_samples=5)

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```

# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| eps | float | 0.5 | DBSCAN'da bir veri noktasının komşuluk yarıçapını belirler. Bu parametre, bir veri noktasının ε yarıçapı içindeki diğer noktaları incelediği alandır. Doğru ε değeri seçmek, kümeleme sonuçlarını etkileyebilir. İyi bir ε değeri, verinin yoğunluğuna ve dağılımına bağlıdır. | 
| min_samples | int | 5 | Bir veri noktasının bir çekirdek nokta olabilmesi için en az kaç komşusu olması gerektiğini belirler. Bu parametre, bir kümenin minimum boyutunu tanımlar. MinPts değerini seçerken, verinin yoğunluğunu dikkate almalısınız. Düşük MinPts değerleri daha fazla küme oluşturabilirken, yüksek MinPts değerleri daha büyük kümeler oluşturur. |

--- 

# FeatureAgglomeration  
Feature Agglomeration, özellik (feature) seviyesinde kümeleme (clustering) yapmak için kullanılan bir kümeleme algoritmasıdır. Bu algoritma, veri setindeki özellikleri benzerliklerine göre gruplandırarak boyut azaltma ve özellik seçimi amaçlar. 

**Nasıl Çalışır:**
1. Feature Agglomeration, özellik benzerlik matrisi (feature similarity matrix) oluşturur. Bu matris, her bir özelliğin diğer özelliklere göre benzerliğini ölçer. Benzerlik, özelliklerin ilişkisini ölçmek için farklı yöntemlerle hesaplanabilir (örneğin, Pearson korelasyonu, kosinüs benzerliği vb.).
2. Benzerlik matrisi kullanılarak kümeleme algoritması, özellikleri gruplar. Benzer özellikler aynı kümede yer alır. Bu, özelliklerin birbirleriyle daha yakından ilişkili olduğu grupları oluşturur.
3. Özelliklerin grupları, boyut azaltma ve özellik seçimi için kullanılabilir. Her grup, tek bir temsilci (centroid) özelliğe dönüştürülür.

**Avantajlar:**

- Boyut Azaltma: Feature Agglomeration, özelliklerin sayısını azaltarak verinin boyutunu küçültebilir, bu da verinin işlenmesini hızlandırabilir.
- Özellik Seçimi: Özelliklerin grupları, en iyi temsilci özellikleri seçmek için kullanılabilir. Bu, veriyi daha basit ve anlaşılır hale getirebilir.

**Dezavantajlar:**

- Bilgi Kaybı: Özelliklerin kümelemesi, bilgi kaybına neden olabilir, çünkü her grup sadece bir temsilci özellik içerir.
- Optimal Küme Sayısı: Optimal küme sayısını belirlemek zor olabilir, ve hatalı küme sayısı seçimi sonuçları olumsuz etkileyebilir.

```python
from sklearn.cluster import FeatureAgglomeration
from sklearn.datasets import load_iris

# Veri yüklemesi
data = load_iris().data

# Feature Agglomeration modeli oluşturma
model = FeatureAgglomeration(n_clusters=2)  # Küme sayısını belirtin

# Veriyi modele uydurma
transformed_data = model.fit_transform(data)

# Sonuçları görüntüleme
print("Özgün veri şekli:", data.shape)
print("Dönüştürülmüş veri şekli:", transformed_data.shape)
```
# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| n_clusters | float | 2 | Küme sayısını belirleyen bir hiperparametredir. Kaç küme oluşturulacağını kontrol eder. Küme sayısını belirlerken, verinin doğasını ve amacınızı dikkate almalısınız. |
| metric | "euclidean", "l1", "l2", "manhattan", "cosine", "precomputed" | None | Benzerlik matrisini hesaplarken kullanılacak benzerlik ölçüsünü belirler. Özellikler arasındaki benzerliği ölçmek için Pearson korelasyonu, kosinüs benzerliği veya başka bir benzerlik metriği seçebilirsiniz. |

---
# KMeans  
K-Means, kümeleme (clustering) için yaygın olarak kullanılan bir algoritmadır. K-Means, veri noktalarını belirli bir sayıda kümeye ayırmak için kullanılır ve her bir kümenin merkezini hesaplar. 

**Nasıl Çalışır:**
1. Başlangıçta, veri noktaları rastgele seçilen "k" küme merkezi ile ilişkilendirilir. "k" bir hiperparametredir ve kullanıcı tarafından belirlenir.
2. Her veri noktası, en yakın küme merkezine atanır. Bu atanma işlemi, veri noktasının hangi kümenin merkezine daha yakın olduğunu belirlemek için öklidyen uzaklık veya başka bir mesafe ölçüsü kullanılarak yapılır.
3. Her küme için yeni merkezler hesaplanır. Yeni merkezler, o kümeye ait veri noktalarının ortalaması olarak belirlenir.
4. İkinci adımdan bu işlem, veri noktalarının atanma ve merkez hesaplama işlemlerinin kararlı hale gelene kadar devam eder. Kararlılık, veri noktalarının küme değiştirmemesi ve merkezlerin değişmemesi anlamına gelir.
5. Sonuç olarak, veri noktaları "k" küme arasında bölünür ve her bir küme kendi merkezine sahip olur.  

**Avantajlar:**
- Basit ve hızlıdır.
- Büyük veri kümeleri üzerinde etkili çalışır.
- Kümeleri rahatlıkla yorumlanabilir ve görselleştirilebilir.
- Özellikle küme sayısını belirlemek gerektiği durumlarda kullanışlıdır.

**Dezavantajlar:**
- Başlangıç merkezlerin rastgele seçilmesi, algoritmanın sonuçlarını etkileyebilir. Bu nedenle, algoritma farklı başlangıç noktalarıyla tekrar tekrar çalıştırılarak daha iyi sonuçlar elde edilebilir.
- K-Means, küme sayısını önceden belirlemeyi gerektirir, bu nedenle yanlış küme sayısı seçimi sonuçları olumsuz etkileyebilir.
- Farklı boyutlarda ve yoğunluktaki kümeleri tanıma konusunda sınırlamaları vardır.

```python
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# K-Means modeli oluşturma
model = KMeans(n_clusters=4)  # Küme sayısını belirtin

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```
# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| n_clusters | int | 8 | K-Means algoritmasıyla oluşturulacak küme sayısını belirler. Bu, kullanıcının belirlemesi gereken bir hiperparametredir. |
| init | "k-means++", "random" | "k-means++" | Başlangıç küme merkezlerinin nasıl belirleneceğini kontrol eder. |
| max_iter | int | 300 | Atama ve güncelleme adımlarının kaç kez tekrarlanacağını belirler. Algoritmanın konverjansa ulaşana kadar maksimum kaç iterasyon yapacağını kontrol eder. |
| n_init | "auto", int | 10 | Başlangıç merkezlerinin farklı başlangıç noktalarıyla çalıştırılacak deneme sayısını belirler. Bu, en iyi sonuçları bulma olasılığını artırır. |

---
# MeanShift  
Mean Shift, bir kümeleme (clustering) algoritmasıdır ve veri noktalarını veri yoğunluğu temelinde kümelemek için kullanılır. Algoritma, veri noktalarını yoğunluk merkezlerine kaydırarak kümelemeyi gerçekleştirir. 

**Nasıl Çalışır:**
1. Her veri noktası, başlangıçta kendisinin bir merkez olarak kabul edildiği bir yoğunluk merkezine atanır.
2. Her bir veri noktası için yoğunluk merkezi hesaplanır. Yoğunluk merkezi, veri noktalarının yoğunluğunun maksimum olduğu noktadır. Bu hesaplama, belirli bir yarıçap içindeki veri noktalarının ağırlıklı ortalama pozisyonunu kullanarak yapılabilir.
3. Her veri noktası, hesaplanan yoğunluk merkezi pozisyonuna kaydırılır.
4. 2. ve 3. adımlar tekrar edilir, veri noktaları yoğunluk merkezlerine yaklaştıkça, yoğunluk merkezleri daha da hassaslaşır.
5. Algoritma, veri noktaları yoğunluk merkezlerine yaklaşmayı bıraktığında sonlanır ve her bir veri noktası son yoğunluk merkezi ile ilişkilendirilir.

**Avantajlar:**
- Küme sayısını önceden belirlemek zorunda değilsiniz. Mean Shift, veri yoğunluğuna dayalı olarak doğal kümeleri bulur.
- Farklı boyutlarda ve şekillerde kümeleri tanıma yeteneğine sahiptir.
- Aykırı değerlere karşı nispeten dirençlidir.

**Dezavantajlar:**
- Hesaplama maliyeti yüksek olabilir, özellikle büyük veri setleri üzerinde çalışırken.
- İlk noktaların seçimi ve başlangıç yarıçapı seçimi sonuçları etkileyebilir. Bu nedenle, başlangıç koşullarının seçimi algoritmanın başarısını etkileyebilir.

```python
from sklearn.cluster import MeanShift
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# Mean Shift modeli oluşturma
model = MeanShift()  # Hiperparametreler belirtilmezse varsayılan değerler kullanılır

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```
# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| bandwidth | float | None | Bandwidth, yoğunluk merkezlerini hesaplamak için kullanılan pencerenin boyutunu belirler. Büyük bir bant genişliği, daha geniş yoğunluk merkezleri üretebilirken, küçük bir bant genişliği daha küçük ve hassas yoğunluk merkezleri üretebilir. Bandwidth, Mean Shift algoritmasının en önemli hiperparametrelerinden biridir ve doğru bir şekilde ayarlanmalıdır. |

---
# MiniBatchKMeans  
MiniBatchKMeans, geleneksel K-Means kümeleme algoritması ile benzer bir yaklaşımı temel alır, ancak büyük veri kümeleri üzerinde daha hızlı çalışmak için bir örnekleme (mini-batch) tabanlı bir yaklaşım kullanır. Bu, büyük veri setlerini hızlı bir şekilde kümelemek için kullanışlıdır. 

**Nasıl Çalışır:**
1. MiniBatchKMeans, rastgele seçilen bir alt örneklemi (mini-batch) kullanır. Bu, tüm veri kümesi yerine daha küçük bir örneklem üzerinde işlem yapılmasını sağlar.
2. Mini-batch üzerinde K-Means algoritmasının adımları uygulanır: İlk olarak, her veri noktası rastgele bir küme merkezine atanır. Daha sonra, her veri noktasının atanma merkezine göre yeniden hesaplanır ve bu işlem iterasyonlarla devam eder.
3. Mini-batch'ler sırayla kullanılır ve her bir mini-batch işlendikten sonra küme merkezleri güncellenir.
4. İterasyonlar belirli bir duruma ulaştığında veya belirli bir iterasyon sayısına ulaştığında algoritma sonlanır.

**Avantajları:**
- Geleneksel K-Means algoritmasına göre daha hızlıdır, özellikle büyük veri kümeleri üzerinde etkilidir.
- Bellek verimliliği sağlar, çünkü tüm veriyi bellekte tutmak yerine mini-batch'leri kullanır.
- Paralel hesaplama için uygundur ve GPU gibi hızlandırıcılarla kullanılabilir.
- Genellikle daha hızlı yakınsar ve daha az hesaplama maliyetine sahiptir.

**Dezavantajları:**
- Küme merkezi güncellemeleri mini-batch boyutuna bağlıdır ve bu nedenle yakınsama daha dalgalı olabilir.
- Elde edilen sonuçlar, geleneksel K-Means'a göre biraz daha düzensiz olabilir.
- Küme sayısını önceden belirlemek gereklidir.

```python
from sklearn.cluster import MiniBatchKMeans
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# MiniBatchKMeans modeli oluşturma
model = MiniBatchKMeans(n_clusters=4)  # Küme sayısını belirtin

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()

```
# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| n_clusters | int | 8 | Kümelerin sayısını belirler. Bu, kullanıcı tarafından belirlenen bir hiperparametredir. |
| batch_size | int | 1024 | Her mini-batch'in boyutunu belirler. Daha büyük bir batch_size, daha yüksek hesaplama maliyeti demektir. Mini-batch boyutunu seçerken bellek ve hesaplama gücü sınırlamalarını göz önünde bulundurmalısınız. |
| max_iter | int | 100 | İterasyonların maksimum sayısını belirler. Algoritmanın ne kadar süre çalışacağını kontrol eder. |
| init | "k-means++", "random" | "k-means++" | Başlangıç merkezlerini seçme yöntemini belirler. |


---
# OPTICS  
OPTICS (Ordering Points To Identify the Clustering Structure), veri kümeleme (clustering) için kullanılan bir algoritmadır ve özellikle yoğunluk temelli kümeleme problemlerinde etkilidir. OPTICS, veri noktalarını sıralayarak kümeleme yapar ve doğal kümeleri ve yoğunluk tabanlı yapısını belirler. 

**Nasıl Çalışır:**
1. Veri noktaları, bir başlangıç veri noktasından başlayarak belirli bir uzaklığa (epsilon) kadar olan diğer veri noktalarını bulur. Bu işlem, her bir veri noktasının yakınlık grafiği (reachability plot) oluşturulurken yapılır.
2. Reachability grafiği, veri noktalarının bir sıralamasını sağlar. Reachability grafiğinde, bir veri noktasının diğer bir veri noktasına olan uzaklığına dayalı olarak bir sıralama gösterilir.
3. Reachability grafiği üzerinde bir eşik değeri (threshold) belirlenir. Bu eşik değeri, belirli bir yoğunluk seviyesini temsil eder. Veri noktaları, bu yoğunluk seviyesinin üstündeki veri noktalarını yoğunluk merkezleri olarak işaretler.
4. Yoğunluk merkezleri arasındaki uzaklıklar kullanılarak kümeleme yapılır. OPTICS, bu uzaklıkları kullanarak doğal kümeleri ve yoğunluk tabanlı yapıyı tanır.

**Avantajlar:**
- Küme sayısını önceden belirlemeye gerek yoktur, çünkü yoğunluk tabanlı bir yaklaşım kullanır.
- Aykırı değerlere karşı nispeten dirençlidir.
- Doğal kümeleri ve yoğunluk tabanlı yapıları tanıma yeteneğine sahiptir.
- Reachability grafiği, veri noktalarının sıralamasını gösterir ve bu, verinin iç yapısını anlama açısından faydalıdır.

**Dezavantajlar:**
- OPTICS hesaplama maliyeti yüksek olabilir ve büyük veri kümeleri üzerinde çalışırken zaman alabilir.
- Reachability grafiği, büyük veri kümeleri üzerinde çok büyük olabilir ve bu nedenle bellek gereksinimleri yüksek olabilir.

```python
from sklearn.cluster import OPTICS
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# OPTICS modeli oluşturma
model = OPTICS()  # Hiperparametreler belirtilmezse varsayılan değerler kullanılır

# Veriyi modele uydurma
model.fit(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=model.labels_, cmap='viridis')
plt.show()
```
# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| eps | float | None | Veri noktalarının bir yoğunluk merkezine erişilebilir kabul edilebilecek maksimum uzaklığı belirler. Bu eşik değeri, kümeleme sonuçlarını etkiler. |
| min_samples | int | 5 | Bir yoğunluk merkezi olarak kabul edilebilecek minimum veri noktası sayısını belirler. Bu, bir yoğunluk merkezi olarak kabul edilmesi için veri noktalarının çevresinde en az kaç veri noktasının bulunması gerektiğini kontrol eder. |

---
# SpectralClustering
Spectral Clustering, veri kümeleme (clustering) için kullanılan bir algoritmadır ve özellikle veri noktalarının benzerlik grafiği üzerinden kümeleme yapma yeteneğine sahiptir. Bu algoritma, veri noktalarının benzerlik matrisini kullanarak bir graf oluşturur ve bu grafiği kullanarak veri kümelemesi yapar. 

**Nasıl Çalışır:**
1. Veri noktaları arasındaki benzerlik matrisi oluşturulur. Bu matris, veri noktaları arasındaki benzerlikleri ölçer. Öklidyen uzaklık, kosinüs benzerliği veya diğer benzerlik ölçüleri kullanılabilir.
2. Benzerlik matrisi, bir grafı temsil eder. Her bir veri noktası bir düğüm ve benzerlikler arasındaki değerler ise kenarlar olarak düşünülür.
3. Graf üzerinde Laplace matrisi hesaplanır. Laplace matrisi, grafın yapısını ve veri noktalarının bağlantılarını yakalar.
4. Laplace matrisinin özdeğer ayrışımı (eigendecomposition) yapılır ve özdeğerler kullanılarak veri noktaları spektral uzayda temsil edilir.
5. Elde edilen spektral uzayda k-means veya diğer kümeleme yöntemleri kullanılarak veri noktaları kümelere ayrılır.

**Avantajlar:**
- Veri noktalarının karmaşık yapılarını ve non-lineer ilişkileri yakalama yeteneğine sahiptir.
- Küme sayısını önceden belirlemeye gerek yoktur. Veriye dayalı olarak doğal kümeleri bulur.
- Aykırı değerlere karşı nispeten dirençlidir.  
- Genellikle geleneksel kümeleme yöntemlerine göre daha iyi sonuçlar verir.


**Dezavantajlar:**
- Hesaplama maliyeti yüksektir ve büyük veri kümeleri üzerinde çalışırken zaman alabilir.
- Bazı uygulamalarda hiperparametre ayarları gerekebilir, özellikle benzerlik matrisinin oluşturulması ve graf oluşturulması aşamalarında.

```python
from sklearn.cluster import SpectralClustering
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

# Veri oluşturma
data, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.0, random_state=42)

# SpectralClustering modeli oluşturma
model = SpectralClustering(n_clusters=4)  # Küme sayısını belirtin

# Veriyi modele uydurma
labels = model.fit_predict(data)

# Sonuçları görselleştirme
plt.scatter(data[:, 0], data[:, 1], c=labels, cmap='viridis')
plt.show()
```

# Hiperparametreler

|Parameter Name|Type|Default|Description|
|---|---|---|---|
| n_clusters | int | 8 | Küme sayısını belirler. Hangi sayıyı seçeceğinizi veri yapısına ve analiz amacınıza bağlı olarak belirlemelisiniz. |
| affinity | str | "rbf" | Benzerlik matrisi hesaplama yöntemini belirler. Öklidyen uzaklık veya kosinüs benzerliği gibi farklı metrikler kullanılabilir. |
| n_neighbors | int | 10 | Grafiği oluştururken her veri noktasının en yakın kaç komşusunu kullanacağınızı belirler. Bu, grafın yoğunluğunu ve bağlantılarını etkiler. |
| eigen_solver | "arpack", "lobpcg", "amg" | None | Özdeğer ayrışımını yaparken kullanılacak algoritmayı belirler. |