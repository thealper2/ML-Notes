Kategorik değişkenleri doğrudan işler. Gradient boosting yöntemini kullanır.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| learning_rate |  |  | Öğrenme oranı. |
| iterations |  |  | Boosting aşamasındaki ağaç sayısı. |
| depth |  |  | Her bir ağacın derinliği. |
| l2_leaf_reg |  |  | L2 düzenleme. |
| bagging_temperature |  |  | Seed. Boosting örneklemesi sırasında kullanılır. |
| border_count |  |  | Sayısal özelliklerin kuantize edilmesi. |
| random_strength |  |  | Rastgele örneklemleme sırasında özelliklerin güçlendirilmesi için kullanılan güçlendirme katsayısı. |
| leaf_estimation_method |  |  | Ağaç yapraklarının tahmin yöntemi. |
| grow_policy |  |  | Ağaç büyüme stratejisi. |
