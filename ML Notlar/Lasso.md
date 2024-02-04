Lasso (Least Absolute Shrinkage and Selection Operator), model karmaşıklığını kontrol etmek için L1 düzenlemesini kullanır. Lineer regresyonun bir türevidir ve L1 düzenlemesi (penalty) ekleyerek modeldeki katsayıları sıfıra yaklaştırarak özellik seçimi yapar. Model, katsayıların sıfıra yaklaşmasını sağlayarak önemsiz özellikleri elemeye çalışır. İlgiz değişkenlerin katsayılarını sıfıra eşitler.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| - | - | - | - |
| alpha | float | 1.0 | L1 düzenlemesi katsayısıdır. Negatif olmamalıdır. alpha 0 olduğunda LineerRegresyon gibi sonuç döner. |
| fit_intercept | bool | True | Kesişimin (intercept) uydurulup uydurulmayacağı. | 
| copy_X | bool | True | Eğer True ise modeli eğitirken X değeri fonksiyonda kullanılacak ve eğitimden sonra da aynı olacaktır. False olduğunda ise X fonksiyona girdikten sonra ilk hali ile aynı olmayabilir. |
| precompute | bool | False | Hesaplamaları hızlandırmak için önceden hesaplanmış bir Gram matrisi olup olmayacağı. |
| max_iter | int | 1000 | Maksimum iterasyon sayısı |
| tol | float | 1e-4 | Optimizasyon toleransı. | 
| warm_start | bool | False | True ise önceki fit çözümünü başlangıç olarak kullanır. |
| positive | bool | False | True ise katsayıları pozitif olmaya zorlar. |
| selection | string | "cyclic" | "random" olduğu zaman her iterasyonda rastgele bir katsayı güncellenir. Tol 1e-4'den yüksek olduğunda daha hızlı yakınsamaya yol açar. | 
| random_state | int | None | Seed |