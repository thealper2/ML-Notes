- Dengesiz sınıf dağılımı düşük tespit oranına (recall score) yol açar.
- Örneklem arttırma (oversampling), örneklem azaltma (undersampling)
- Çoğunluk (majority), azınlık (minority)

--- 
# Under Sampling Metodları
##### A. Dönüştürülmüş Veri Seti Üzerinden Örneklem Seçen Metodlar
1. **Near Miss Undersampling:** Çoğunluk sınıfın azınlık sınıflara uzaklığına göre bu örneklemleri seçen bir örneklem azaltma metodudur.
2. **Condensed Nearest Neighbors Rule:** CNN, KNN algoritmasının memory ihtiyacını azaltması için üretildi.

##### B. Silinecek Örnekleri Seçen Metodlar
1. **Tomek Links:** Her bir sınıftan en yakın Öklid uzaklığına sahip birer tane örnek ile pair (çift) duruma gelmesini kural olarak koyar ve bu sınıflar arası oluşan çiftler Tomek linkler olarak adlandırılır.
2. **Edited Nearest Neighbors Rule:** Kısa adı ENN. Veri setindeki belirsiz, gürültülü örnekleri ortadan kaldırmak için kullanılır. Veriden mümkün olduğunda az bilgi kaybına yol açarak yoğunluk sınıfını azaltması sağladığı en büyük faydadır.

##### C. Hibrit Metodlar
1. **One Sided Selection:** Kısa adı OSS. Tomek Link ve CNN rule metodlarını kombinleyen bir metoddur. Tomek linklerinin sınırda ve gürültülü tüm veri örneklerini kaldırmasıyla oluşturduğu alt kümenin ardından CNN karar sınıfından uzaktaki çoğunluk sınıfı örneklerini veri setinden kaldırır.
2. **Neighborhood Cleaning Rule:** CNN ve ENN metodlarını kombinleyen bir metoddur.

---
# Over Sampling Metodları

##### A. Rastgele Oversampling
1. **Rastgele Tekrarlı Örnekleme (Random Oversampling):** Azınlık sınıftaki örnekleri rastgele seçerek artırır.
2. **Rastgele SMOTE (Random SMOTE):** SMOTE yöntemini temel alır ve sentetik örnekler oluşturur, ancak bu işlemde rastgele seçilen örnekler kullanılır.

##### B. Sentetik Oversampling
1. **SMOTE:** Azınlık sınıfındaki örnekleri kullanarak sentetik örnekler oluşturur.
2. **ADASYN (Adaptive Synthetic Sampling):** Örneklerin yoğunluğuna göre sentetik örnekler üretir, özellikle azınlık sınıfındaki zor örnekler üzerinde odaklanır.
3. **Borderline-SMOTE:** Sınıf sınırında yer alan örnekler üzerine odaklanır ve sentetik örnekler bu sınıflarda oluşturulur.

