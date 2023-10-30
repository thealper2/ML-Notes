  
Öneri sistemleri (recommendation systems), kullanıcılara ürünler, içerik veya hizmetler hakkında kişiselleştirilmiş öneriler sunan bir tür yapay zeka uygulamasıdır. Bu sistemler, genellikle büyük veri kümelerini analiz ederek ve kullanıcıların geçmiş etkileşimleri veya tercihleri gibi bilgileri kullanarak, kullanıcıların ilgisini çekebilecek öğeleri tahmin etmeye çalışırlar. Öneri sistemleri, e-ticaret siteleri, video akış platformları, müzik akış servisleri, haber siteleri ve daha pek çok alanda kullanılır. ikiye ayrılır:
- **İçerik Tabanlı (Content-Based) Öneri Sistemleri**
- **İşbirliği Tabanlı (Collaborative)  Öneri Sistemleri**

### Content-Based Filtering
İçerik tabanlı öneri sistemleri, kullanıcılara belirli öğeleri veya içerikleri kişiselleştirilmiş önerilerle sunan bir tür yapay zeka uygulamasıdır. Bu sistemler, kullanıcıların veya öğelerin içerik özelliklerini analiz ederek çalışırlar. İçerik tabanlı öneri sistemleri, bir kullanıcının geçmiş tercihleri ve incelemeleri gibi verileri kullanarak, bu kullanıcının ilgisini çekebilecek benzer içerikleri önerir.Content-based öneri sistemlerinde kullanılan benzerlik hesaplama yöntemleri, kullanıcı profili ile içerik özellikleri arasındaki benzerliği değerlendirmek için kullanılır.

- **Kosinüs Benzerliği (Cosine Similarity):** Vektörler arasındaki açıyı ölçerek benzerliği hesaplar. Kullanıcı profil vektörü ile her öğe arasındaki kosinüs benzerliği hesaplanır.

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# Özellik vektörleri: Her bir satır bir filmü temsil eder.
# Her bir sütun bir türü temsil eder. Örneğin, 1. sütun "Aksiyon", 2. sütun "Komedi" vb.
# Örnek özellik vektörleri sadece temsil amaçlıdır.
features = np.array([
    [1, 0, 1, 0, 1],  # Film 1: Aksiyon ve Bilim Kurgu
    [0, 1, 0, 1, 0],  # Film 2: Komedi
    [1, 0, 0, 0, 1],  # Film 3: Aksiyon ve Korku
    [0, 0, 0, 1, 1]   # Film 4: Korku
])

# Kullanıcı profil vektörü: Kullanıcının tür tercihlerini temsil eder.
user_profile = np.array([1, 1, 0, 0, 0])  # Kullanıcı Aksiyon ve Komedi filmlerini sever.

# Cosine similarity hesaplama
similarities = cosine_similarity([user_profile], features)

# Benzerlik skorları ve önerilen filmler
similarities = similarities[0]  # Tek bir kullanıcının benzerlik skorları
recommended_movies = np.argsort(similarities)[::-1]  # Benzerlik sırasına göre filmleri sırala

print("Benzerlik Skorları: ", similarities)
print("Önerilen Filmler (Sırasıyla): ", recommended_movies)
```

- **Jaccard Benzerliği (Jaccard Similarity):** İki kümenin kesişimini birleşimine bölen bir oranı ifade eder. Özelliklerin varlığı veya yokluğuyla ilgili olduğu için sıklıkla kategorik veriler üzerinde kullanılır.

```python
import numpy as np

# Film türlerini temsil eden özellik vektörleri (örnek veri)
# Her satır bir filmı temsil eder, her sütun bir türü temsil eder.
# Örneğin, 1. sütun "Aksiyon", 2. sütun "Komedi" vb.
features = np.array([
    [1, 0, 1, 0, 0],  # Film 1: Aksiyon ve Bilim Kurgu
    [0, 1, 0, 1, 0],  # Film 2: Komedi ve Romantik
    [1, 0, 0, 0, 1],  # Film 3: Aksiyon ve Korku
    [0, 0, 0, 1, 1]   # Film 4: Korku
])

# Kullanıcının tür tercihlerini temsil eden özellik vektörü
user_profile = np.array([1, 1, 0, 0, 0])  # Kullanıcı Aksiyon ve Komedi filmlerini sever.

def jaccard_similarity(a, b):
    intersection = np.logical_and(a, b)
    union = np.logical_or(a, b)
    return np.sum(intersection) / np.sum(union)

# Jaccard benzerliği hesaplama
similarities = [jaccard_similarity(user_profile, film_features) for film_features in features]

# Benzerlik skorları ve önerilen filmler
recommended_movies = np.argsort(similarities)[::-1]  # Benzerlik sırasına göre filmleri sırala

print("Benzerlik Skorları: ", similarities)
print("Önerilen Filmler (Sırasıyla): ", recommended_movies)
```

- **Öklidyen Uzaklığı (Euclidean Distance):** İki nokta arasındaki doğrusal uzaklığı hesaplar.

```python
import numpy as np

# Özellik vektörleri: Her bir satır bir filmi temsil eder.
# Her bir sütun bir özelliği temsil eder.
features = np.array([
    [2.5, 1.0, 3.0],  # Film 1
    [1.5, 2.5, 0.5],  # Film 2
    [2.0, 3.5, 2.5],  # Film 3
    [0.5, 1.5, 3.0]   # Film 4
])

# Kullanıcı profil vektörü: Kullanıcının tercih ettiği özelliklerin ağırlıklarını içerir.
user_profile = np.array([3.0, 1.5, 2.0])

def euclidean_distance(a, b):
    return np.linalg.norm(a - b)

# Öklidyen mesafe hesaplama
distances = [euclidean_distance(user_profile, film_features) for film_features in features]

# Uzaklık skorları ve önerilen filmler
recommended_movies = np.argsort(distances)  # Uzaklık sırasına göre filmleri sırala

print("Uzaklık Skorları: ", distances)
print("Önerilen Filmler (Sırasıyla): ", recommended_movies)
```

### Collaborative Filtering

Collaborative Filtering (İşbirlikçi Filtreleme), kullanıcıların veya öğelerin geçmiş etkileşimlerini temel alarak kişiselleştirilmiş öneriler sunan bir öneri sistemlerinin bir türüdür. Bu yöntem, kullanıcıların benzer tercihleri olan diğer kullanıcıları veya öğeleri bulur ve bu benzerliklere dayanarak önerilerde bulunur.

1. **Benzer Kullanıcılar (User-Based Collaborative Filtering)**: Bu yöntem, kullanıcıların benzer tercihlere sahip olan diğer kullanıcıları bulur. Örneğin, kullanıcı A ve kullanıcı B benzer filmleri beğeniyorsa, kullanıcı A'nın beğendiği ancak kullanıcı B'nin görmediği bir filmi kullanıcı B'ye önerir. Benzer kullanıcıları bulmak için yaygın olarak kullanılan ölçümler arasında kosinüs benzerliği veya Pearson korelasyon katsayısı bulunur.    
2. **Benzer Öğeler (Item-Based Collaborative Filtering)**: Bu yöntem, benzer özelliklere sahip olan öğeleri bulur ve kullanıcıların geçmiş etkileşimleri temel alarak benzer öğeleri önerir. Örneğin, bir kullanıcı film A'nın benzer türdeki film B'yi beğendiyse, film B'yi kullanıcıya önerir. Benzer öğeleri bulmak için kullanılan ölçümler arasında cosine similarity veya Jaccard similarity gibi metrikler bulunur.

İşbirlikçi Filtreleme yöntemleri, genellikle "user-item matrix" olarak adlandırılan bir veri matrisini kullanır. Bu matris, kullanıcıların öğelerle olan etkileşimlerini veya derecelendirmelerini içerir. Boş değerler, kullanıcının belirli bir öğe ile etkileşimde bulunmadığını veya öğeyi derecelendirmediğini gösterir.