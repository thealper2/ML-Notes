Extremely Randomized Trees, ağaçların oluşturulması sırasında rastgelelik kullanarak bir dizi karar ağacı oluşturur ve bu ağaçların tahminlerini bir araya getirerek sonuçları üretir. Diğer ağaç tabanlı yöntemlerden farkı, ağaçların oluşturulması ve eğitim sürecindeki rastgelelik derecesinin daha yüksek olmasıdır.

**Çalışma Adımları**
1. Her bir ağaç oluşturulurken, özelliklerden rastgele bir alt küme seçilir.
2. Her özellik için rastgele bir eşik değeri seçilir.
3. Rastgele özellik ve eşik değerleri kullanılarak karar ağaçları oluşturulur. Maksimum derinliğe ulaşana kadar büyütülür.
4. Bootstrap ile her ağacın farklı bir eğitim veri setiyle eğitilmesi sağlanır.
5. Tüm ağaçlar üzerinde tahminler yapılır ve bu tahminler bir araya getirilerek modelin tahminleri üretilir. Sınıflandırma için en sık görülen tahmin alınır. Regresyon için tahminlerin ortalaması alınır.

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| n_estimators | int | 100 | Oluşturulacak ağaç sayısı. |
| max_depth | int | None | Oluşturulacak ağaçların maksimum derinliği. Fazla olması modelin karmaşıklığını ve aşırı uyumu artırabilir. |
| min_samples_split | int | 2 | Bir iç düğümün ikiye bölünmeden önce kaç örneğe sahip olması gerektiği. |
| min_samples_leaf | int | 1 | Bir yaprak düğümünün en az kaç örneğe sahip olması gerektiği. |
| max_features | "sqrt", "log2", float | "sqrt" | Her bir ağaçta kullanılacak maksimum özellik sayısı. <br/> "sqrt": len(n_features) <br/> "log2": log2(n_features) |
| bootstrap | bool |  | Bootstrap örneklemlerinin kullanılıp kullanılmayacağını belirler. |
