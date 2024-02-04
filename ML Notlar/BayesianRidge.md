Bayes teoremini ve bayes istatistik prensiplerine dayanarak lineer regresyon temelli bir modeldir. Bayes teoremi kullanarak olasılık dağılmını güncelleyerek parametreleri belirler.

1. Bir önceki dağılım (prior distribution) belirlenir. Bu, parametrelerin olası değerleri hakkında bir öngörü sağlar.
2. Problemi bir olasılık dağılımı olarak ele alır.
3. Veri dağılımına bağlı olarak bir olasılık fonksiyonu (likelihood function) belirlenir. Bu fonksiyon, modelin parametrelerinin belirli bir değere sahip olma olasılığını tanımlar.
4. Model, veriye dayalı olarak bayes teoremini kullanarak önceki dağılımları günceller.
5. Güncellenmiş dağılımlar modelin parametreleri için bir sonraki dağılımı (posterior distribution) oluşturur.
6. Model bu dağılımı kullanarak tahmin yapar.

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| alpha_1 | float | 1e-6 | Prior distribution için L2 regularizasyon hassasiyeti. |
| alpha_2 | float | 1e-6 | Likelihood function için L2 regularizasyon hassasiyeti. |
| lambda_1 | float | 1e-6 | Prior distribution için L1 regularizasyon hassasiyeti. |
| lambda_2 | float | 1e-6 | Likelihood function için L1 regularizasyon hassasiyeti. |
| tol | float | 1e-3 | Optimizsayon algoritmasının toleransı. |
