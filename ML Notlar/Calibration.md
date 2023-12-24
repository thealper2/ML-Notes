Kalibrasyon, modelin çıktılarını gerçek olasılıklara daha yakın hale getirmeyi amaçlar. 
1. Platt Scaling (Sigmoid Fitting)
2. Isotonic Regression
3. Beta Calibration
4. Platt's Method Extension

---
# Platt Scaling (Sigmoid Fitting)
Adını John Platt'ten alır. Genellikle sigmoid fonksiyonu ile gerçekleştirilir. İlk olarak sınıflandırıcı çıktıları log-odds'a dönüştürülür. Ardından, log-odds değerleri sigmoid fonksiyonuna geçirilir. Bu olasılıkları \[0, 1] aralığına yeniden ölçekler.

```python
from sklearn.calibration import CalibratedClassifierCV

svm = SVC(probability=True, random_state=42)
svm.fit(X_train, y_train)

calibrated_svm = CalibratedClassifierCV(svm, method='sigmoid', cv='prefit')
calibrated_svm.fit(X_train, y_train)

probabilities_before = svm.predict_proba(X_test)[:, 1]
probabilities_after = calibrated_svm.predict_proba(X_test)[:, 1]
```

---
# Isotonic Regression
Olasılık tahminlerini düzgünleştirmek için monoton artan bir fonksiyonla uyumlu hale getirir. İlk olarak, modelin olasılık tahminleri sıralanır. Monoton artan bir fonksiyon olan isotonic regression kullanılır. Bu regresyon, sıralı tahminler arasında bir düzgünleştirme yaparak olasılık tahminlerini yeniden ölçekler.

```python
from sklearn.calibration import CalibratedClassifierCV
from sklearn.isotonic import IsotonicRegression

svm = SVC(probability=True, random_state=42)
svm.fit(X_train, y_train)

calibrated_svm = CalibratedClassifierCV(svm, method='sigmoid', cv='prefit')
calibrated_svm.fit(X_train, y_train)

probabilities_after = calibrated_svm.predict_proba(X_test)[:, 1]

isotonic_regressor = IsotonicRegression(out_of_bounds='clip')
isotonic_regressor.fit(probabilities_after, y_test)

probabilities_isotonic = isotonic_regressor.transform(probabilities_after)
```

---
# Beta Calibration
Olasılık tahminlerini uygun bir şekilde düzgünleştirmek için beta dağılımını kullanır. İlk olarak, modelin olasılık tahminleri log-odds'a dönüştürülür. Ardından log-odds değerleri beta dağılımına uydurulur. Beta dağılımı \[0, 1] aralığındaki değerleri modellere uygulayarak olasılık tahminlerini yeniden ölçekler.

```python 
from sklearn.calibration import CalibratedClassifierCV
from sklearn.calibration import calibration_curve

svm = SVC(probability=True, random_state=42)
svm.fit(X_train, y_train)

calibrated_svm = CalibratedClassifierCV(svm, method='sigmoid', cv='prefit')
calibrated_svm.fit(X_train, y_train)

probabilities_after = calibrated_svm.predict_proba(X_test)[:, 1]

def beta_calibration(probabilities):
    sorted_probs = np.sort(probabilities)
    beta_values = np.linspace(0.5, len(sorted_probs) - 0.5, len(sorted_probs)) / len(sorted_probs)
    calibrated_probs = np.clip(np.interp(probabilities, sorted_probs, beta_values), 0, 1)
    return calibrated_probs

probabilities_beta = beta_calibration(probabilities_after)
```

---
# Platt's Method Extension
Sigmoid dönüşümü yerine, daha genel bir logit dönüşümünü kullanır. İlk olarak modelin olasılık tahminleri logit dönüşümüne tabi tutulur. Elde edilen değerler üzerinde doğrusal bir regresyon modeli kurulur. Bu model, olasılık tahminlerini ölçeklemek için kullanılır.

```python
from sklearn.calibration import CalibratedClassifierCV

svm = SVC(probability=True, random_state=42)
svm.fit(X_train, y_train)

calibrated_svm = CalibratedClassifierCV(svm, method='sigmoid', cv='prefit')
calibrated_svm.fit(X_train, y_train)

logit_transformed_probs = calibrated_svm.predict_proba(X_test)[:, 1] 

lr = LogisticRegression()
lr.fit(logit_transformed_probs.reshape(-1, 1), y_test)

scaled_probs = lr.predict_proba(logit_transformed_probs.reshape(-1, 1))[:, 1]
```

---
# Metrikler

- **Brier Score:** Gerçek sınıf etiketleri ile tahmin edilen olasılıklar arasındaki farkların karesinin ortalamasıdır. Düşük brier skoru, daha iyi kalibre edilmiş bir modeli gösterir.
- **Reliability Diagram:** Gerçek sınıf olasılıkları ve modelin tahmin ettiği olasılıklar arasındaki ilişkiyi gösterir.
- **Calibration Curve:** Gerçek ve tahmin edilen olasılıklar arasındaki ilişkiyi görselleştiren bir eğridir. İdeal olarak eğri doğrusal olmalıdır.