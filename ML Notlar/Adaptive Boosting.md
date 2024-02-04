Zayıf öğrenicileri bir araya getirerek güçlü bir öğrenici oluşturmak için kullanılan bir toplu öğrenme yöntemidir.

**Çalışma Adımları**
1. Her bit örnek başlangıçta 1/N ağırlığına sahiptir. N, toplam örnek sayısı.
2. Bir zayıf öğrenici eğitilir.
3. Zayıf öğrenicinin doğruluğu hesaplanır.
4. Doğruluğu düşük olan örneklerin ağırlığı arttırılır. Bu, yanlış sınıflandırılan örneklerin daha fazla dikkate alınmasını sağlar. Modelin bu örnekleri daha iyi sınıflandırması beklenir.
5. Ağırlıklandırılmış eğitim veri seti, bir sonraki zayıf öğreniciyi eğitmek için kullanılır. Bu süreç, belli bir iterasyon (boosting round) için tekrarlanır.
6. Her bir zayıf öğrenici, tahminlerin gücüne göre bir ağırlıkla birleştirilir. Bu ağırlıklandırma işlemi, her bir öğreticinin doğruluğuna göre belirlenir. Daha doğru tahminler, daha büyük ağırlığa sahip olur.
7. Zayıf öğrenicilerin bir araya getirilmesiyle güçlü bir öğrenici elde edilir.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| estimator | object | None | Kullanılacak zayıf öğrenici türü. |
| n_estimators | int | 50 | Kullanılacak zayıf öğrenici sayısı. Fazla olması karmaşıklığı ve overfit'i artırabilir. |
| learning_rate | float | 1.0 | Her bir zayıf öğrenicinin katkısını artırmak veya azaltmak için kullanılan parametre. |
| loss | 'linear', 'square', 'exponential' | 'linear' | Kayıp fonksiyonu. |
| random_state | int | None | Rastgelelik kontrolü. |
