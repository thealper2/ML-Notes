# Filter Methods (Filtre Yöntemleri)
Filtre yöntemleri bir ön işleme adımı olarak kullanılır. Özelliklerin seçimi herhangi bir makine öğrenimi algoritmasından bağımsızdır. Bunun yerine, özellikler, sonuç değişkeniyle olan korelasyonlarına yönelik çeşitli istatistiksel testlerdeki puanlarına göre seçilir. Wrapper Methods (Sarmalayıcı Yöntemler)'den daha düşük tahmin performansı verirler. Hızlı bir tarama ve alakasız özelliklerin çıkarılması için çok uygundurlar.

- **Variance Threshold (Varyans Eşiği):** Varyansı belirli bir eşiği karşılamayan tüm özellikleri kaldırır. Default olarak tüm sıfır varyanslı özellikleri kaldırır.
- **Quasi-constant Features (Yarı sabit özellikler):** Yarı sabit özellikler, veri kümesindeki gözlemlerin büyük çoğunluğu için aynı değeri gösteren özelliklerdir. Bu özellikler, bir makine öğrenimi modelinin bir hedefi ayırt etmesine veya tahmin etmesine olanak tanıyan çok az bilgi sağlar. Ancak istisnalar da olabilir.
- **SelectKBest:** Özellikleri en yüksek k puana göre seçer. Beraber Chi-square testi yapılabilir.
- **SelectPercentile:** En yüksek puanların yüzdelik dilimine göre özellikleri seçer.

**NOT:** SelectKBest ve SelectPercentile için aşağıdaki yöntemler de kullanılabilir:
- Regresyon problemleri için: f_regression, mutual_info_regression
- Sınıflandırma problemleri için: chi2, f_classif, mutual_info_classif

F-testine dayalı yöntemler iki rastgele değişken arasındaki doğrusal bağımlılık derecesini tahmin eder. Karşılıklı bilgi yöntemleri (mutual_ ile başlayanlar) her türlü istatistiksel bağımlılığı yakalayabilir ancak parametrik olmadıkları için doğru tahmin için daha fazla örneğe ihtiyaç duyarlar.

- **Information Gain (Karşılıklı Bilgi):** Bir özelliğin varlığının/yokluğunun hedef hakkında doğru tahminde bulunmaya ne kadar katkıda bulunduğunu ölçer. Bu değişkenlerden birini bilmenin diğer hakkıdaki belirsizliği ne kadar azalttığını ölçer. Örneğin X-Y bağımsızsa birini bilmenin diğeri hakkında bilgi vermez. Böylece information gain = 0'dır.
- **Fisher Score:** Negatif olmayan her özellik ve sınıf arasındaki ki-kare istatistiklerini hesaplar. Özellikler kategorik ise chi2 kullanılır.
- **ANOVA F-value:** Özellikler nicel  ise her bir özellik ile hedef arasındaki ANOVA F-değeri hesaplanır. F-değeri, sayısal özelliği hedefe göre gruplandırdığımızda, her bir grubun ortalamalarının önemli ölçüde farklı olup olmadığını hesaplar.
- **Pearson Correlation:** Korelasyon, 2 veya daha fazla değişkenin doğrusal ilişkisinin bir ölçüsüdür. Korelasyon sayesinde bir değişkeni diğerinden tahmin edebiliriz. İyi değişkenler hedef değişkenle yüksek oranda ilişkilidir. Değişkenler hedef değişkenle ilişkili olmalı fakat kendi aralarında ilişkisiz olmalıdır. Eğer öyleyse, korelasyonlu olanlardan sadece birini tutmamız ve diğerlerini bırakmamız gerekir.

---

# Wrapper Methods (Sarmalayıcı Yöntemler)
Sarmalayıcı yöntemlerde, özelliklerin bir alt kümesini kullanmaya ve bunları kullanarak bir model eğitmeye çalışılır. Önceki modelden çıkardığımız çıkarımlara dayanarak, alt kümeye özellik eklemeye veya çıkarmaya karar verilir.

- **Forward Selection:** Modelde hiçbir özellik olmadan başlanan iteratif bir yöntemdir. Her bir iterasyonda, yeni bir değişken eklenmesi modelin performansını iyileştirmeyene kadar modeli en iyi iyileştiren özelliği eklemeye devam eder. 
- **Backward Selection:** Tüm özelliklerle başlanır ve her iterasyonda modelin performansını artıran en az anlamlı özellik kaldırılır. Bu işlem, özelliklerin kaldırılmasında herhangi bir iyileşme gözlenmeyene kadar tekrarlanır.
- **Exhaustive Feature Selection:** Bir algoritma için belirli bir performans metriğini optimize ederek tüm olası özellik alt kümeleri arasından en iyi özellik alt kümesi seçilir. 
- **Recursive Feature Elimination:** En iyi performans gösteren özellik alt kümesini bulmayı amaçlayan açgözlü bir optimizasyon algoritmasıdır. Tekrar tekrar modeller oluşturur ve her iterasyonda en iyi veya en kötü performans gösteren özelliği bir kenarda tutar. Tüm özellikler tükenene kadar kalan özelliklerle bir sonraki modeli oluşturur. Daha sonra özellikleri eleme sırasına göre sıralar.
- **Recursive Feature Elimination with CV (RFECV):** 0 ile N özelliği yinelemeli olarak kaldırarak tahmin edici için en iyi özellik alt kümesini seçer.

---

# Embedded Methods (Gömülü Yöntemler)
- **Lasso Regression:** Lasso regresyonu, katsayıların büyüklüğünün mutlak değerlerine eşdeğer bir ceza ekleyen bir L1 düzenlemesi gerçekleştirir. L1, bazı katsayıları sıfıra kadar küçültebilen bir özelliğe sahiptir. Bu nedenle, bu özellik modelden çıkarılabilir.

