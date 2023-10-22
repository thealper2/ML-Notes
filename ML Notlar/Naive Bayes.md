Naive Bayes algoritması, olasılık teorisine dayalı bir makine öğrenimi ve istatistiksel sınıflandırma algoritmasıdır. Temel olarak, bir nesnenin belirli bir sınıfa ait olma olasılığını tahmin etmek için kullanılır. Bu sınıflandırma algoritması, Bayes Teoremi'ne dayanır ve "naif" (ingenuous) olarak adlandırılır, çünkü sınıf tahminindeki özellikler arasındaki bağımsızlık varsayımı yapar, yani her özelliğin sınıfı etkileme olasılığı birbirinden bağımsızdır.

Naive Bayes Türleri

- **Gaussian Naive Bayes**: Özellikler sürekli değer (continuous value) ise bu değerlerin bir gauss dağılımı veya diğer bir değişle normal dağılımdan örneklendiğini varsayar.
- **Multinominal Naive Bayes:** Çok sınıflı kategorileri sınıflandırmak için kullanılır.
- **Bernoulli Naive Bayes:** Multinominal Naive Bayes’e benzer şekilde sınıflandırma yapar. Ancak tahminler sadece ikili şekildedir.
# Çalışma Prensibi

P(A|B) = \[P(B|A) * P(A)] / P(B)

Burada:

- P(A|B), B koşulu altında A'nın olasılığını temsil eder.
- P(A), A'nın önceden bilinen veya gözlemlenen olasılığını temsil eder.
- P(B|A), A'nın verildiği durumda B'nin olasılığını temsil eder.
- P(B), B'nin önceden bilinen veya gözlemlenen olasılığını temsil eder.

Naive Bayes algoritması, sınıflandırma problemlerinde P(A|B)'yi hesaplamak için bu formülü kullanır.
# Avantajlar
- Basit ve Hızlı
# Dezavantajlar
- Özelliklerin birbirinden bağımsız olduğunu varsayar, bu varsayıma gerçekte pek sık rastlanmaz.
- Küçük veri setlerinde kötü performans gösterebilir.
- Verilerdeki gürültüye ve eksikliğe oldukça duyarlıdır.
# Hiperparametreler

| Parameters | Types | Default | Description |
| - | - | - | - |
