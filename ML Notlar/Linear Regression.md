Linear Regression, bağımlı ve bağımsız değişkenler arasındaki ilişkiyi temsil eden doğrusal bir denklem oluşturarak tahmin etmeye çalışır. Bu model, verilerdeki ilişkiyi en iyi şekilde temsil eden doğruyu bulmaya çalışır. Özellik sayımız bir ise "Simple Linear Regression", birden fazla ise "Multiple Linear Regression" kullanılır.

**Çalışma Adımları**


# Hiperparametreler
| Parametre | Tür | Default | Açıklama |
| - | - | - | - |
| fit_intercept | bool | True | Model için keşiminin (intercept) hesaplanıp hesaplanmayacağını belirler. 
| copy_X | bool | True | Eğer True ise modeli eğitirken X değeri fonksiyonda kullanılacak ve eğitimden sonra da aynı olacaktır. False olduğunda ise X fonksiyona girdikten sonra ilk hali ile aynı olmayabilir. |
| n_jobs |int | None | Hesaplama için kullanılacak iş sayısı. Büyük problemlerde işe yarar, hızlanma sağlar. |
| positive | bool | Default | Katsayıyı (coefficient) pozitif olmaya zorlar. |