  Data leakage (veri sızıntısı), veri setinin yanlış bir şekilde kullanılması sonucu, sonuçların yanıltıcı veya yanıltıcı hale gelmesi durumunu ifade eder. Data leakage, modelin yanıltıcı şekillerde yüksek doğruluk oranlarına ulaşmasına veya yanlış sonuçlar üretmesine neden olabilir. Modelin öğrenmemesi gereken bir şeyi öğrenmesidir. Aşağıdaki durumlar örnektir;
  - Eksik verilerin veri setinin tümünü kullanarak (train-test ayırmadan) mean/mode/median ile doldurulması.
  - Scale ederken veri setinin tümünün kullanılması (train-test ayırmadan. X_scaled = ss.fit_transform(X))
  - Bazı kategorik sütunlara one-hot encoding uygulanması / encode edilmesi.
  - Over/Under Sampling işlemlerinde veri setinin tümünün kullanılması (train-test ayırmadan)