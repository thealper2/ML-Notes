# ARDRegression (Automatic Relevance Determination Regression)

- **Çalışma Mantığı**: ARDRegression, Ridge ve Lasso regresyonun birleşimi olarak düşünülebilir. Bu model, L2 ve L1 düzenlemelerini bir araya getirir ve otomatik olarak modeldeki en önemli özellikleri belirlemeye çalışır. Katsayıları sıfıra yaklaştırmak ve modeli genelleştirmek için düzenleme kullanırken, aynı zamanda modelin içeriğindeki en önemli özellikleri seçmeye çalışır.
- **Kullanım Alanları**: Regresyon problemleri
- **Veri Setleri**: Özellikle yüksek boyutlu veri setleri ve özellik sayısı düşük olduğunda etkilidir.
- **Pozitif Yönler**: Özellik seçimini otomatik olarak yapar, aşırı uydurma riskini azaltır, önemli özellikleri belirlemeye yardımcı olur.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| - | - | - | - |
| tol | 1e-3 | w yakınsadıysa algoritmayı durdurur |
| alpha_1 | float | 1e-6 | L1 düzenlemesi katsayısıdır. Bu parametre arttıkça L1 düzenlemesi etkisi artar. | 
| alpha_2 | float | 1e-6 | L2 düzenlemesi katsayısıdır. Bu parametre arttıkça L2 düzenlemesi etkisi artar. |
| lambda_1 | float | 1e-6 | Intercept (kesme noktası) için L1 düzenlemesi katsayısıdır. |
| lambda_2 | float | 1e-6 | Intercept (kesme noktası) için L2 düzenlemesi katsayısıdır. |
| compute_score | bool | False | True ise modelin her adımında amaç fonksiyonunu hesaplar. |
| threshold_lamda | float | 10000 | Yüksek hassasiyete sahip ağırlıkların hesaplamadan çıkarılması (budanması) için eşik. |
| fit_intercept | bool | True | Kesişimin (intercept) uydurulup uydurulmayacağı. | 
| copy_X | bool | True | Eğer True ise modeli eğitirken X değeri fonksiyonda kullanılacak ve eğitimden sonra da aynı olacaktır. False olduğunda ise X fonksiyona girdikten sonra ilk hali ile aynı olmayabilir. |
| verbose | bool | False | True ise çıktı gösterir. |

