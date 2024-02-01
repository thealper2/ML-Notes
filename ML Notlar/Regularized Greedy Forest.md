Normal RF'den hızlıdır. Daha fazla parametreye sahiptir. İki temel bileşenden oluşur:
- **Regularization (Düzenleme):** Her bir karar ağacının büyüklüğünü ve karmaşıklığını kontrol etmek için bir düzenleme yöntemi kullanır. Bu düzenleme, her bir ağacın büyüklüğünü sınırlayarak overfittingi önler.
- **Greedy Learning:** Her bir ağaç, bir özellik seçerek ve bu özelliğe göre bir bölme yaparak oluşturulur. Her bir bölme için en iyi özelliği seçmek için bir düzgünleştirme işlemi uygular. Bu da daha iyi genelleme sağlar.

```python
from rgf import RGFClassifier

model = RGFClassifier(max_leaf=150, algorithm='RGF_Sib', test_interval=100)
model.fit(X_train, y_train)
```

# Hiperparametreler

| Parametre Adı | Değerler | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| algorithm | "RGF", "RGF_Opt", "RGF_Sib" | "RGF" | "RGF", "l2" düzenlileştirme,  "RGF_Opt" min-penalty, "RGF_Sib" min-penalty + sum-to-zero sibling. |
| loss | "LS", "Expo", "Log" | "LS" | LS square loss, Expo exponential loss, Log logistic loss. |
