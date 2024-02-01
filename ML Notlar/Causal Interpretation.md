Modelin verilerden neden-sonuç ifadelerini çıkarabilmesidir. Nedensel ilişkilerin anlaşılması, sadece belirli bir olayın diğerini takip ettiği zamansal sıra veya ilişkisel korelasyonlardan daha fazlasını içerir. Bu, bir değişkenin başka bir değişkeni doğrudan etkileyebileceği ve bu etkinin nedensel olduğu anlamına gelir.

# CATE (Conditional Average Treatment Effect)
CATE, belirli bir müdahalenin veri üzerinde ortalama olarak ne tür bir etkiye sahip olduğunu gösterir. Bu etki diğer özelliklere bağlı olarak değişebilir. Nedensel etkileri incelemek için kullanılır. Teknikler:
- Double Machine Learning
- Doubly Robust
- Meta-Learner
- Orthogonal Random Forest

# Double Machine Learning
Çift model yaklaşımını kullanır. İki farklı model ile tahminler yapar ve bu tahminler arasındaki farkı analiz eder. İki model genellikle bir denklem ve bir tahminci model olarak adlandırılır.
- **Denklem modeli:** Bağımsız değişkenler ve sonucun tahmin edilmesi için kullanılır.
- **Tahminci model:** Bağımsız değişkenlerin sonucunu tahmin etmek için kullanılır.
Denklem modelininin yanıltıcı bir şekilde etkilenmemesi sağlanmalıdır. 

```python
from econml.dml import DML
from econml.sklearn_extensions.linear_model import StatsModelsLinearRegression
from sklearn.ensemble import RandomForestRegressor, RandomForestClassifier

est = DML(
	model_y=RandomForestRegressor(),
	model_t=RandomForestClassifier(),
	model_final=StatsModelLinearRegression()
)
est.fit(y, T, X=X, W=None)
```

# Doubly Robust
Çift model yaklaşımını kullanır. Kısmi modelden gelen tahminler kullanılarak doğrudan bir tahmin yapılır. Tahmin modelinden gelen tahminler kullanılarak müdahalenin etkisi tahmin edilir. Bu iki tahmin arasındaki fark, müdahalenin gerçek etkisini belirlemek için kullanılır.
- **Partial Model:** Kovaryanslar ve diğer değişkenler ile bağımlı değişken arasındaki ilişkiyi belirler.
- **Tahmin Modeli:** Müdahalenin etkisini tahmin etmek için kullanılır.

```python
from eeconml.dr import LinearDRLearner

est = LinearDRLearner()
est.fit(y, T, X=X, W=None)
```

# Meta-Learners
Birincil bir modelin çıktısını kullanarak ikincil bir modeli eğiten modeldir. Bu sayede birincil modelin performansını iyileştirir ve onun çıktılarını daha iyi bir şekilde kullanır.

```python
from econml.metalearners import XLearner
from sklearn.linear_model import LinearRegression

est = XLearner(models=LinearRegression())
est.fit(y, T, X=X)
```

# Orthogonal Random Forest
ORF, RF algoritmasına çıkarımlar için uygun hale getirmek bir düzeltme yapar. Bu düzeltme, karar ağaçlarının gözlemlenen veriler üzerinden değil, önceki çalışmalardan elde edilen tahminler üzerinde eğitilmesini sağlar. Bu tahminler, müdahalenin etkisini doğrudan tahmin etmek için kullanılır.
