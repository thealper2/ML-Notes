Değişkenlerin öngörüler üzerindeki etkilerini görselleştirmektir. Belirli bir bağımsız değişkenin diğer değişkenlere göre bağımlığını gösterir. PDP tüm değişkenleri bağımsız sayar. Bir değişkenin diğer değişkenlerle etkileşimlerini gösterir. 

# Adımları

1. **Değişken Seçimi:** İlgilenilen bağımsız değişken seçilir.
2. **Değişkenin Değer Aralığının Belirlenmesi:** Seçilen değişkenin olası değer aralığı belirlenir.
3. **Diğer Değişkenlerin Değerleri Sabit Tutma:** Diğer bağımsız değişkenlerin değerleri sabit tutularak, seçilen değişkenin etkisi incelenir.
4. **Modelin Tahminlerinin Alınması:** Değişkenin değeri değiştirilerek, model üzerinden tahminler alınır.
5. **Sonuçların Görselleştirilmesi**

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_boston
from sklearn.inspection import plot_partial_dependence
from sklearn.ensemble import GradientBoostingRegressor

boston = load_boston()
X, y = boston.data, boston.target

model = GradientBoostingRegressor(n_estimators=50, max_depth=6, learning_rate=0.1, loss='huber', random_state=4242)

model.fit(X, y)

features = [5]
plot_partial_dependence(model, X, features, grid_resolution=50, feature_names=boston.feature_names)

plt.show()
```

