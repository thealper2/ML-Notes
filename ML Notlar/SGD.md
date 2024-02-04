Stochastic Gradient Descent (SGD), her bir veri noktası için gradyan iniş algoritmasını kullanarak ağırlıklarını günceller ve böylece regresyon yoluyla öğrenir.

**Çalışma Adımları**
1. Eğitim verilerindeki örneklerden rastgele başlangıç parametreleriyle başlar.
2. Rastgele seçilen örnekler üzerinden gradyan (türev) hesaplar. Bu gradyan, kayıp fonksiyonunun optimuma doğru yönelik bir tahmini sağlar.
3. Hesaplanan gradyan kullanılarak parametreler güncellenir. SGD, her adımda gradyanın ters yönünde bir adım atarak parametrelerin güncellenmesini sağlar. Bu adım öğrenme oranıdır.
4. Parametreler güncellendikçe kayıp fonksiyonunun değeri azalır.
5. SGD belirli bir iterasyon sayısına uğraşana kadar adımları tekrarlar.
# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| alpha | float | 0.0001 | Düzenlemeyi kontrol eder. |
| loss | str, "squared_error", "huber", "epsilon" | "squared_error" | Kayıp fonksiyonu. |
| penalty | "l1", "l2", "elasticnet", None | "l2" | Düzenleme fonksiyonu. |
| learning_rate | str, "constant", "optimal", "invscaling" | "invscaling" | Öğrenme oranı. |
