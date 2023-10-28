## Grid Search

- Grid Search, bir makine öğrenme modelinin hiperparametrelerini ayarlamak için kullanılan bir hiperparametre tuning yöntemidir. Bu yöntem, belirli bir hiperparametre uzayında tüm olası kombinasyonları deneyerek en iyi hiperparametre setini bulmayı amaçlar. Grid Search, parametrelerin bir ızgara gibi düzenlendiği ve her hiperparametre kombinasyonunun denendiği bir arama sürecini içerir.

**Avantajları**
- Tüm hiperparametre kombinasyonlarını denediği için en iyi sonuçları elde etme olasılığı yüksektir.
- Basit ve anlaşılır bir yaklaşım, hiperparametrelerin aralığını ve adım büyüklüğünü belirlemek kolaydır.
- Özellikle küçük veri setleri için etkili olabilir.

**Dezavantajları**
- Hesaplama maliyeti yüksektir, çünkü tüm kombinasyonlar denendiğinden, büyük veri setlerinde veya çok sayıda hiperparametrele sahip modellerde kullanmak zaman alabilir.
- İzgara araması, hiperparametreler arasındaki etkileşimleri dikkate almaz.
- Optimum hiperparametrelerin belirlenmesi için birçok deneme gerekebilir.

```python
from sklearn.model_selection import GridSearchCV
from sklearn.svm import SVC

# Hiperparametreler ve değer aralıkları
param_grid = {'C': [0.1, 1, 10], 'kernel': ['linear', 'rbf']}

# Model
svm_model = SVC()

# Grid Search
grid_search = GridSearchCV(estimator=svm_model, param_grid=param_grid, cv=5, scoring='accuracy')
grid_search.fit(X_train, y_train)

# En iyi hiperparametre kombinasyonu ve sonuç
best_params = grid_search.best_params_
best_score = grid_search.best_score_

print("En iyi hiperparametreler:", best_params)
print("En iyi doğruluk:", best_score)
```

---
## Random Search

- Random Search, hiperparametre tuning yöntemlerinden biridir ve makine öğrenme modellerinin hiperparametrelerini ayarlamak için kullanılır. Random Search, Grid Search gibi tüm hiperparametre kombinasyonlarını denemek yerine rastgele seçilen hiperparametre kombinasyonlarını kullanarak modelin performansını değerlendirir. Bu yöntem daha verimli olabilir ve daha iyi sonuçlar elde etme olasılığı yüksektir.

**Avantajları**
- Hesaplama maliyeti, Grid Search'e göre genellikle daha düşüktür, çünkü rastgele kombinasyonlar denendiğinden daha az model eğitilir.
- Optimum hiperparametreleri belirleme olasılığı Grid Search'e göre daha hızlıdır, özellikle büyük hiperparametre uzaylarında.

**Dezavantajları**
- En iyi sonuçları elde etmek için daha fazla denemeye ihtiyaç duyabilir, çünkü rastgele kombinasyonlar şansa bağlıdır.
- Hiperparametreler arasındaki etkileşimleri yakalamak zor olabilir, çünkü rastgele seçilen kombinasyonlar arasında bu etkileşimler olmayabilir.

```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.svm import SVC
from scipy.stats import uniform, randint

# Hiperparametreler ve değer aralıkları
param_dist = {
    'C': uniform(loc=0.1, scale=9.9),
    'kernel': ['linear', 'rbf']
}

# Model
svm_model = SVC()

# Random Search
random_search = RandomizedSearchCV(estimator=svm_model, param_distributions=param_dist, n_iter=10, cv=5, scoring='accuracy')
random_search.fit(X_train, y_train)

# En iyi hiperparametre kombinasyonu ve sonuç
best_params = random_search.best_params_
best_score = random_search.best_score_

print("En iyi hiperparametreler:", best_params)
print("En iyi doğruluk:", best_score)
```

---
# Particle Swarm Optimization (PSO)
PSO (Particle Swarm Optimization), doğal bir olay olan kuş sürülerinin ve bal arılarının davranışlarından esinlenen bir evrimsel optimizasyon algoritmasıdır. PSO, birçok olası çözüm noktasını temsil eden parçacıkların birbirleriyle etkileşimde bulunarak, bir hedef işlevi eniyilemek için bir araya gelmesini simüle eder. PSO, özellikle hiperparametre tuning ve optimizasyon problemlerinde kullanılır.

**Avantajları:**
- PSO, doğal olarak paralelleştirilebilir, bu nedenle çok sayıda işlemci veya hesaplama kaynağı kullanarak hızlı sonuçlar elde etmek mümkündür.
- Basit bir algoritma yapısına sahiptir ve kolayca uygulanabilir.
- Çeşitli problem türlerinde etkili sonuçlar verir.

**Dezavantajları:**
- PSO'nun başarısı, başlangıç noktalarının rastgele seçimine ve algoritmanın parametrelerine hassasiyet gösterebilir. Bu nedenle, bazı problemlerde diğer optimizasyon yöntemlerinden daha iyi sonuçlar elde etmek zor olabilir.
- Global en iyi çözümü bulmak garanti değildir. Bazı problemlerde, algoritma lokal minimumlarda sıkışabilir.
---
# Genetic Algorithm (GA)
Genetik Algoritma (Genetic Algorithm - GA), biyolojik evrim süreçlerinden esinlenen bir evrimsel optimizasyon tekniğidir. Genetik algoritma, çözüm uzayında potansiyel çözümleri genetik operatörler (çaprazlama, mutasyon, seçilim) kullanarak geliştirir ve bu operatörler yoluyla en iyi çözümü bulmaya çalışır. Genetik algoritma, birçok problemi çözmek ve karmaşık optimizasyon problemlerine yaklaşmak için kullanılır.

**Avantajları:**
- Genetik Algoritma, global optimuma yaklaşma yeteneği ile karmaşık ve çok boyutlu problemleri çözmek için kullanılabilir.
- Çeşitli problem türlerinde etkili sonuçlar verir ve çok sayıda uygulama alanına sahiptir.
- Paralelleştirilebilir, bu nedenle büyük hesaplamalı kaynaklarda hızlı bir şekilde uygulanabilir.

**Dezavantajları:**
- Genetik Algoritma, hesaplama maliyeti yüksek olabilir, özellikle büyük popülasyonlar ve uzun iterasyonlar gerektiren problemlerde.
- Başlangıç popülasyonunun kalitesi ve uygunluk fonksiyonunun doğru seçimi algoritmanın başarısını etkiler.
- Genetik Algoritma, bazı problemlerde lokal minimumlarda sıkışabilir ve global optimuma ulaşamayabilir.

---
## Optuna

- Optuna, en iyi parametre setini bulmak için parametrelerin rastgele kombinasyonlarını deneyen bir yöntemdir. GridSearch'e ve RandomSearch'e göre(iterasyon sayısına bağlı) daha hızlı çalışabilir. Ayrıca, parametreler arasındaki ilişkileri dikkate alarak daha iyi parametre kombinasyonları bulur. Bayesian Optimization yöntemi kullanılarak gerçekleştirilir.

**Avantajları:**
1. **Otomasyon ve Akıllı Arama:** Optuna, deneme-yanılma yöntemine dayalı hiperparametre ayarlama işlemini otomatikleştirir ve akıllı bir arama stratejisi kullanır. Bu, hiperparametre optimizasyonunu daha verimli hale getirir.
2. **Modüler ve Esnek:** Optuna, farklı makine öğrenme çerçeveleri ve algoritmalarıyla kullanılabilir. Ayrıca, hiperparametre optimizasyonunuzu özelleştirmek için esnek bir yapı sunar.
3. **Dokümantasyon ve Topluluk Desteği:** Optuna'nın iyi bir dokümantasyonu vardır ve geniş bir kullanıcı topluluğuna sahiptir. Bu, başlamak ve sorunlarla başa çıkmak için faydalıdır.
4. **Veritabanı Desteği:** Optuna, sonuçları ve çalışma bilgilerini veritabanında saklama yeteneğine sahiptir. Bu, geçmiş çalışmaları izlemenize ve sonuçları yeniden kullanmanıza olanak tanır.
5. **Dağıtık Hesaplama Desteği:** Optuna, çoklu işlemcileri veya farklı makine üzerinde çalıştırılabilecek çalışmaları yönetmek için dağıtık hesaplama yetenekleri sunar.

**Dezavantajları:**
1. **Hesaplama Maliyeti:** Optuna'nın bazı kullanımları, büyük sayıda denemenin yapılmasını gerektirebilir ve bu nedenle hesaplama maliyeti yüksek olabilir.
2. **Yavaşlık:** Optuna'nın bazı optimizasyon işlemleri yavaş olabilir, özellikle büyük hiperparametre uzaylarında veya çok uzun süren modellerde.
3. **Ayarlanması Zor Olabilir:** Optuna'nın başlangıçta bazı ayarlamalar gerektirebilir ve en uygun arama stratejisinin seçilmesi hiperparametre optimizasyonunu etkileyebilir.
4. **Karmaşıklık:** Bazı kullanıcılar için, özellikle temel hiperparametre ayarlaması gereken basit modellerde, Optuna kullanmanın gereksiz bir karmaşıklık olduğunu düşünebilir.

```python
import optuna
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier

# Veriyi yükle
data = load_iris()
X, y = data.data, data.target

# Eğitim ve test veri setlerini oluştur
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Optuna ile optimize edilecek hiperparametreleri tanımla
def objective(trial):
    # Hiperparametreler
    max_depth = trial.suggest_int("max_depth", 1, 32)
    min_samples_split = trial.suggest_float("min_samples_split", 0.1, 1.0)
    min_samples_leaf = trial.suggest_float("min_samples_leaf", 0.1, 0.5)

    # Karar ağacı modelini oluştur
    model = DecisionTreeClassifier(
        max_depth=max_depth,
        min_samples_split=min_samples_split,
        min_samples_leaf=min_samples_leaf,
    )

    # Modeli eğit ve doğruluk skoru hesapla
    model.fit(X_train, y_train)
    accuracy = model.score(X_test, y_test)
    return accuracy

# Optuna çalıştır
study = optuna.create_study(direction="maximize")  # Maksimize edilen metrik (doğruluk)
study.optimize(objective, n_trials=100)  # 100 farklı deneme yap

# En iyi hiperparametreleri ve sonucu al
best_params = study.best_params
best_accuracy = study.best_value

print("En iyi hiperparametreler:", best_params)
print("En iyi doğruluk:", best_accuracy)
```