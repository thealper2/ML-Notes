LGBM, Microsoft tarafından 2017 yılında geliştirilmiştir. Light Gradient Boosting Machine, histogram tabanlıdır. Gradient boosting yöntemini kullanır. Ağaçları düşey olarak büyütür. Bu, her ağacın yalnızca veri kümesinin belirli bir alt kümesinde odaklanmasını sağlar böylece hesaplama süresi azalır.  Diğer makine öğrenmesi modellerinden farklı olarak paralel öğrenme ve GPU kullanımını destekler. Modelin tanıtıldığı "LightGBM: A Highly Efficient Gradient Boosting Decision Tree" makalesinde diğer modellere göre 20 kat daha hızlı çalıştığı yazmaktadır. İki tür büyüme stratejisine sahiptir:
- **Leaf-wise:** Bölme işlemi kaybı azalan yapraklardan devam eder. Model daha az hata oranı ile daha hızlı öğrenir.
- **Depth-wise:** Ağaç büyürken dengesi korunur. 

- **Gradient-based One-Side Sampling (GOSS):** Eğitim sürecinde kullanılan bir örnekleme tekniğidir. GOSS, büyük gradyanlara sahip örnekleri korurken, küçük gradyanlara sahip örnekleri filtreleyerek veri setinin boyutunu azaltır. Böylece gradient boost algoritması daha hızlı çalışır.
- **Exclusive Feature Bundling (EFB):** Özellik mühendisliği sırasında kullanılan bir tekniktir. EFB, benzer davranış gösteren özellikleri gruplayarak bellek kullanımını azaltır ve modelin karmaşıklığını azaltır. Bu sayede, eğitim süresi kısaltılır ve modelin genelleştirme yeteneği artar.

# Hiperparametreler

| Parametre         | Type | Default | Açıklama                                                                             |
| ----------------- | ---- | ------- | ------------------------------------------------------------------------------------ |
| num_leaves        | int  | 31      | Bir ağaçtaki her seviyedeki maksimum yaprak sayısı. 2^max_depth'den küçük olmalıdır. |
| max_depth         | int  | -1      | Bir ağacın maksimum derinliği.                                                       |
| learning_rate     | int  | 0.1     | Gradient güncellemeleri sırasında kullanılan öğrenme oranı.                          |
| n_estimators      | int  | 100     | Oluşturulacak ağaç sayısı.                                                           |
| min_child_samples | int  | 20      | Bir yaprağın altındaki minimum örnek sayısı.                                         |
| subsample         | int  | 1       | Her ağaç için kullanılacak alt örnekleme oranı.                                      |
| colsample_bytree  | int  | 1       | Her ağaç için kullanılan özelliklerin yüzdesi.                                       |
| reg_alpha         | int  | 0       | L1 düzenleme                                                                         |
| reg_lambda        | int  | 0       | L2 düzenleme                                                                         |
