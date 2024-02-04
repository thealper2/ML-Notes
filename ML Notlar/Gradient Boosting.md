Toplu öğrenme yöntemidir. Modelin performansını geliştirmek için hatalara odaklanır.

**Çalışma Adımları**
1. Temel bir model seçilir.
2. Tüm veri seti için bir başlangıç tahmini yapılır. Regresyon için veri setinin ortalaması olabilir. Sınıflandırma için veri setindeki sınıfların oranı olabilir.
3. Başlangıç tahmininden sonra, gerçek değerler ile başlangıç tahmin arasındaki hatalar hesaplanır. Bu hatalar, modelin daha fazla odaklanması gereken alanları gösterir.
4. Hataların eğimi (gradient) hesaplanır. Eğim, her bir örnek için hata fonksiyonunun, tahmin edilen değerlere göre ne kadar değiştiğini gösterir.
5. Bu hataları tahmin etmek için temel bir model oluşturur.
6. Temel model, bir öğrenme oranı ile ağırlanır ve hata tahminine katılır. Öğrenme oranı, her temel modelin katkısını düzenler ve modelin aşırı uyumunu kontrol eder.
7. Yeni temel modelin tahminleri, önceki tahminlere eklenir ve güncellenmiş bir tahmin elde edilir.
8. İterasyon sayısına kadar 3 ve 7 arası tekrarlanır.

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| n_estimators | int | 100 | Oluşturulacak temel modellerin sayısı. |
| learning_rate | float | 0.1 | Her bir temel modelin katkısının ölçeği. |
| max_depth | int | 3 | Oluşturulacak karar ağaçlarının maksimum derinliği. |
| min_samples_split | int | 2 | Bir iç düğümün ikiye bölünmeden önce kaç örneğe sahip olması gerektiği. |
| min_samples_leaf | int | 1 | Bir yaprak düğümünün en az kaç örneğe sahip olması gerektiği. |
| subsample | float | 1 | Her bir temel modelin eğitiminde kullanılacak örneklerin oranı. SGD'ye benzer bir etkiye sahiptir. |
| loss | "log_loss", "exponential" | "log_loss" | Kayıp fonksiyonu. |
