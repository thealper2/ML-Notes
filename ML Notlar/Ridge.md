Çok değişkenli regresyon verilerini analiz etmek için kullanılır. Lineer regresyonun bir türevidir ve genellikle aşırı uydurma (overfitting) problemini çözmek için kullanılır. Model, lineer regresyonun temel yapısını korurken, katsayıları sınırlamak için L2 düzenlemesi (penalty) ekler. Bu düzenleme, kaysayıların büyüklüğünü sınırlayarak modeli daha da genelleştirilmiş hale getirir. Tüm değişkenler ile modeli oluşturur, ilgisiz değişkenleri çıkarmaz fakat katsayılarını sıfıra yaklaştırır. 

# Hiperparametreler
| Parametre | Type | Default | Açıklama |
| - | - | - | - |
| alpha | float | 1.0 | L2 düzenlemesi katsayısıdır. Bu parametre arttıkça katsayıların büyüklüğüne daha fazla düzenleme uygulanır. |
| fit_intercept | bool | True | Kesişimin (intercept) uydurulup uydurulmayacağı. | 
| copy_X | bool | True | Eğer True ise modeli eğitirken X değeri fonksiyonda kullanılacak ve eğitimden sonra da aynı olacaktır. False olduğunda ise X fonksiyona girdikten sonra ilk hali ile aynı olmayabilir. |
| max_iter | int | None | Gradyan çözücüsü için maximum iterasyon sayısı. |
| tol | float | 1e-4 | Katsayı hassasiyeti (coef) |
| solver | string | "auto" | Hesaplamada kullanılacak çözücü. | 
| positive | bool | False | True ise katsayıları pozitif olmaya zorlar. |
| random_state | int | None | Seed |