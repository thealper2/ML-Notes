**Vectorizer vs Transformer**: Vectorizer metin verilerini doğrudan vektörlere dönüştürürken, Transformer ise zaten vektörleştirilmiş metin verileri üzerinde işlem uygular.

# TfidfVectorizer (Term Frequency - Inverse Document Frequency)
Metin verilerini sayısal vektörlere dönüştürmek için kullanılır. Yüksek boyutlu metin verilerini işlemek için etkili bir araçtır. Nadir görülen terimlerin, özellikle küçük veri setlerinde, model performansına etkisi az olabilir. Stop-word gibi yaygın kelimelerin etkisini azaltır. Metin verilerindeki kelime önemini dikkate alarak vektörler oluşturur. Vektörün boyutunun büyüklüğüne bağlı olarak bellek kullanımı artar.
- **Term Frequency (Terim Frekansı - TF):** Bir belgedeki bir terimin kaç kez geçtiğini ölçer. Yüksek TF, bir terimin belgedeki önemini gösterir.
- **Inverse Document Frequency (Ters Belge Frekansı - IDF):** Bir terimin tüm belgelerde ne kadar yaygın olduğun ölçer. Yaygın terimlerin genel anlamda daha az önemli olduğunu gösterir.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
X_train = vectorizer.fit_transform(X_train)
X_test = vectorizer.transform(X_test)
```

# DictVectorizer
Sözlük yapılarından özellik matrisleri oluşturmak için kullanılır. Sözlük yapısındaki her öğeyi bir özellik olarak düşünür. He özellik için benzersiz değerler toplar ve bunları bir özellik matrisini dönüştürür. Özelliklerin her bir değeri için 0 veya 1 gibi ikili bir temsil kullanarak özellik matrisini oluşturur. 

```python
from sklearn.feature_extraction import DictVectorizer

dv = DictVectorizer(sparse=False)
test_dict = [{'foo': 1, 'bar': 2}, {'foo': 3, 'baz': 1}]
X = dv.fit_transform(test_dict)
```

# CountVectorizer
Metindeki her bir kelimenin belirli bir belgedeki frekansını içerir. Önişleme adımları uygulanan metindeki her bir kelimenin metindeki frekansı hesaplanır. Bu frekanslar, her bir kelimenin birer özellik olduğu ve metin belgesinin bir vektör olarak temsil edildiği bir matrise dönüştürülür.

```python
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer()
X_train = vectorizer.fit_transform(X_train)
X_test = vectorizer.transform(X_test)
```

# HashingVectorizer
Bir hash fonksiyonu kullanarak metin verilerini sayısal vektörlere dönüştürür. Bu sayede, sabit boyutta bir vektör elde edilir. Her bir kelimenin bir hash fonksiyonuyla belirli bir boyuttaki bir vektör içindeki konumun belirler. Kelimelerin belirlenen boyuttaki vektördeki konumlarına göre vektör oluşturulur. Hash fonksiyonları çakışma (collision) problemine neden olabilir yani farklı kelimeler aynı hash değerine sahip olabilir. Kullanılan hash fonksiyonu geri dönüşümlü olmadığı için vektörden kelimeye dönüş yapmak zordur.

```python
from sklearn.feature_extraction.text import HashingVectorizer

vectorizer = HashingVectorizer()
X_train = vectorizer.fit_transform(X_train)
X_test = vectorizer.transform(X_test)
```