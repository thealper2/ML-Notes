# Filter Methods (Filtre Yöntemleri)
Filtre yöntemleri bir ön işleme adımı olarak kullanılır. Özelliklerin seçimi herhangi bir makine öğrenimi algoritmasından bağımsızdır. Bunun yerine, özellikler, sonuç değişkeniyle olan korelasyonlarına yönelik çeşitli istatistiksel testlerdeki puanlarına göre seçilir. Wrapper Methods (Sarmalayıcı Yöntemler)'den daha düşük tahmin performansı verirler. Hızlı bir tarama ve alakasız özelliklerin çıkarılması için çok uygundurlar.

- **Variance Threshold (Varyans Eşiği):** Varyansı belirli bir eşiği karşılamayan tüm özellikleri kaldırır. Default olarak tüm sıfır varyanslı özellikleri kaldırır.
```python
from sklearn.feature_selection import VarianceThreshold
vt = VarianceThreshold(threshold=0).fit(X_train)

vt.get_support()
```

- **Quasi-constant Features (Yarı sabit özellikler):** Yarı sabit özellikler, veri kümesindeki gözlemlerin büyük çoğunluğu için aynı değeri gösteren özelliklerdir. Bu özellikler, bir makine öğrenimi modelinin bir hedefi ayırt etmesine veya tahmin etmesine olanak tanıyan çok az bilgi sağlar. Ancak istisnalar da olabilir.
```python
from sklearn.feature_selection import VarianceThreshold
vt = VarianceThreshold(threshold=0.01).fit(X_train)

vt.get_support()
```

- **SelectKBest:** Özellikleri en yüksek k puana göre seçer. Beraber Chi-square testi yapılabilir.
```python
from sklearn.feature_selection import SelectKBest, chi2
X_new = SelectKBest(chi2, k=3).fit_transform(X, y)
X_new.shape
```
- **SelectPercentile:** En yüksek puanların yüzdelik dilimine göre özellikleri seçer.
```python
from sklearn.feature_selection import SelectPercentile, chi2
X_new = SelectPercentile(chi2, percentile=5).fit_transform(X, y)
X_new.shape
```

**NOT:** SelectKBest ve SelectPercentile için aşağıdaki yöntemler de kullanılabilir:
- Regresyon problemleri için: f_regression, mutual_info_regression
```python
f_value = f_regression(X_train, y_train)

for feature in zip(X_train.columns, f_value[0]):
	print(feature)

mi_score = mutual_info_regression(X_train, y_train)
for feature in zip(X_train.columns, mi_score):
	print(feature)
```
- Sınıflandırma problemleri için: chi2, f_classif, mutual_info_classif
```python
f_value = f_classif(X_train, y_train)

for feature in zip(X_train.columns, f_value[0]):
	print(feature)

mi_score = mutual_info_classif(X_train, y_train)
for feature in zip(X_train.columns, mi_score):
	print(feature)
```

F-testine dayalı yöntemler iki rastgele değişken arasındaki doğrusal bağımlılık derecesini tahmin eder. Karşılıklı bilgi yöntemleri (mutual_ ile başlayanlar) her türlü istatistiksel bağımlılığı yakalayabilir ancak parametrik olmadıkları için doğru tahmin için daha fazla örneğe ihtiyaç duyarlar.

- **Information Gain (Karşılıklı Bilgi):** Bir özelliğin varlığının/yokluğunun hedef hakkında doğru tahminde bulunmaya ne kadar katkıda bulunduğunu ölçer. Bu değişkenlerden birini bilmenin diğer hakkıdaki belirsizliği ne kadar azalttığını ölçer. Örneğin X-Y bağımsızsa birini bilmenin diğeri hakkında bilgi vermez. Böylece information gain = 0'dır.
- **Fisher Score:** Negatif olmayan her özellik ve sınıf arasındaki ki-kare istatistiklerini hesaplar. Özellikler kategorik ise chi2 kullanılır.
- **ANOVA F-value:** Özellikler nicel  ise her bir özellik ile hedef arasındaki ANOVA F-değeri hesaplanır. F-değeri, sayısal özelliği hedefe göre gruplandırdığımızda, her bir grubun ortalamalarının önemli ölçüde farklı olup olmadığını hesaplar.
- **Pearson Correlation:** Korelasyon, 2 veya daha fazla değişkenin doğrusal ilişkisinin bir ölçüsüdür. Korelasyon sayesinde bir değişkeni diğerinden tahmin edebiliriz. İyi değişkenler hedef değişkenle yüksek oranda ilişkilidir. Değişkenler hedef değişkenle ilişkili olmalı fakat kendi aralarında ilişkisiz olmalıdır. Eğer öyleyse, korelasyonlu olanlardan sadece birini tutmamız ve diğerlerini bırakmamız gerekir.
```python
df_corr = df.corr()
```

---

# Wrapper Methods (Sarmalayıcı Yöntemler)
Sarmalayıcı yöntemlerde, özelliklerin bir alt kümesini kullanmaya ve bunları kullanarak bir model eğitmeye çalışılır. Önceki modelden çıkardığımız çıkarımlara dayanarak, alt kümeye özellik eklemeye veya çıkarmaya karar verilir.

- **Forward Selection:** Modelde hiçbir özellik olmadan başlanan iteratif bir yöntemdir. Her bir iterasyonda, yeni bir değişken eklenmesi modelin performansını iyileştirmeyene kadar modeli en iyi iyileştiren özelliği eklemeye devam eder. 
```python
from mlxtend.feature_selection import SequentialFeatureSelector

sfs = SequentialFeatureSelector(RandomForestRegressor(), 
								   k_features=10, 
								   forward=True, 
								   floating=False, 
								   verbose=2,
								   scoring='r2',
								   cv=5)

sfs = sfs.fit(np.array(X_train), y_train)
sfs.k_feature_idx_
```
- **Backward Selection:** Tüm özelliklerle başlanır ve her iterasyonda modelin performansını artıran en az anlamlı özellik kaldırılır. Bu işlem, özelliklerin kaldırılmasında herhangi bir iyileşme gözlenmeyene kadar tekrarlanır.
```python
from mlxtend.feature_selection import SequentialFeatureSelector

sfs = SequentialFeatureSelector(RandomForestRegressor(), 
								   k_features=10, 
								   forward=False, 
								   floating=False, 
								   verbose=2,
								   scoring='r2',
								   cv=5)

sfs = sfs.fit(np.array(X_train), y_train)
sfs.k_feature_idx_
```
- **Exhaustive Feature Selection:** Bir algoritma için belirli bir performans metriğini optimize ederek tüm olası özellik alt kümeleri arasından en iyi özellik alt kümesi seçilir. 
- **Recursive Feature Elimination:** En iyi performans gösteren özellik alt kümesini bulmayı amaçlayan açgözlü bir optimizasyon algoritmasıdır. Tekrar tekrar modeller oluşturur ve her iterasyonda en iyi veya en kötü performans gösteren özelliği bir kenarda tutar. Tüm özellikler tükenene kadar kalan özelliklerle bir sonraki modeli oluşturur. Daha sonra özellikleri eleme sırasına göre sıralar.
- **Recursive Feature Elimination with CV (RFECV):** 0 ile N özelliği yinelemeli olarak kaldırarak tahmin edici için en iyi özellik alt kümesini seçer.

---

# Embedded Methods (Gömülü Yöntemler)
- **Lasso Regression:** Lasso regresyonu, katsayıların büyüklüğünün mutlak değerlerine eşdeğer bir ceza ekleyen bir L1 düzenlemesi gerçekleştirir. L1, bazı katsayıları sıfıra kadar küçültebilen bir özelliğe sahiptir. Bu nedenle, bu özellik modelden çıkarılabilir.
```python
from sklearn.feature_selection import SelectFromModel
sel_ = SelectFromModel(Lasso(alpha=100))
sel_.fit(scaler.transform(X_train), y_train)
sel_.get_support()
```
- **Tree-based Methods:** Ağaç modellerinin içerisindeki "feature_importances_" özelliği ile yapılır.
```python
rf = RandomForestClassifier().fit(X_train, y_train)
rf.feature_importances_
```