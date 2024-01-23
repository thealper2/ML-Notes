Online Learning, modelin sürekli olarak yeni veri üzerinde güncellendiği veya eğitildiği bir öğrenme yöntemidir. Bu öğrenme yöntemi sayesinde modelin zaman içinde değişen ve gelişen bir çevreyle başa çıkabilmesi sağlanır. İki kategoriye ayrılır
- Continual Learning (Sürekli Öğrenme)
- Incremental Learning (Artımlı Öğrenme)

# Offline Learning
Model bir veri seti üzerinde eğitilir ve eğitildikten sonra sabit kalır. Yeni veri geldiğinde, model güncellenmez ve bu nedenle yeni bilgileri öğrenme yeteneği sınırlıdır.

---
# Continual Learning (Sürekli Öğrenme)
Bir modelin zaman içinde gelen yeni veri ile sürekli olarak güncellenerek öğrenmeye devam ettiği bir yöntemdir. Model başlangıçta öğrendiği bilgileri sürekli olarak genişletir ve günceller. Model, yeni veriyi öğrenirken önceki bilgileri unutma eğilimindedir. Bu bilgi çakışmasına (catastrophic forgetting) neden olabilir. Bunu önlemek için ağ yeniden kullanılır (network reuse). Önceki eğitilmiş ağ, yeni veri üzerinde eğitim yapmak için kullanılır.

# Incremental Learning (Artımlı Öğrenme)
Bir modelin önceki eğitimin genişletmek veya yeni sınıflar ekleyerek güncellenmesine dayanır.


# Modeller

Parametreler: fit_partial, warm_start, init_model

 'fit_partial' parametresi ile eğitilenler:
1. MultinomialNB
2. BernoulliNB
3. Perceptron
4. SGDClassifier
5. PassiveAggressiveClassifier
6. SGDRegressor
7. PassiveAggressiveRegressor
8. MiniBatchKMeans

'init_model' parametreli ile eğitilenler:
- LGBMClassifier
- XGBClassifier
- CatBoostClassifier
- LGBMRegressor
- XGBRegressor
- CatBoostRegressor
