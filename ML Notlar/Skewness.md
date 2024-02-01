Veri dağılımının simetrisini ve asimetrisini ölçen bir istatistiksel terimdir.. Üç tür çarpıklık vardır:
- **Negatif (sol) çarpıklık:** Sola doğru çarpık, kuyruk sağ tarafta daha uzundur. Veri setindeki büyük değerler daha sık görülürken küçük değerler daha az sıklıkta görülür. Mean < Median < Mode. 
- **Pozitif (sağ) çarpıklık:** Sağa doğru çarpık, kuyruk sol tarafta daha uzundur. Veri setindeki küçük değerler daha sık görülürken büyük değerler daha az sıklıkta görülür. Mode < Median < Mean.
- **Simetrik dağılım:** Çarpıklık yok. Veri setindeki büyük ve küçük değerlerin görülme sıklığı eşittir.

# Box-Cox Dönüşümü
Veri setindeki çarpıklığı azaltmak veya veriyi normal dağılıma yakın bir hale getirmek için kullanılır. λ parametresi belirlenerek gerçekleştirilir.

```shell
(y^λ - 1) / λ      if λ = 0
log(y)             if λ != 0

# y -> dönüştürülmek istenen değişken
# λ -> dönüşüm parametresi
```

```python
from scipy.stats import boxcox

train, test = train_test_split(df, test_size=0.2)
train, fitted_lambda = boxcox(train)
test = boxcox(test, fitted_lambda)
```

