Light Gradient Boosting Machine, ağaç tabanlıdır. Gradient boosting yöntemini kullanır. Ağaçları düşey olarak büyütür. Bu, her ağacın yalnızca veri kümesinin belirli bir alt kümesinde odaklanmasını sağlar böylece hesaplama süresi azalır.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| num_leaves |  |  | Bir ağaçtaki her seviyedeki maksimum yaprak sayısı. |
| max_depth |  |  | Bir ağacın maksimum derinliği. |
| learning_rate |  |  | Gradient güncellemeleri sırasında kullanılan öğrenme oranı. |
| n_estimators |  |  | Oluşturulacak ağaç sayısı. |
| min_child_samples |  |  | Bir yaprağın altındaki minimum örnek sayısı. |
| subsample |  |  | Her ağaç için kullanılacak alt örnekleme oranı. |
| colsample_bytree |  |  | Her ağaç için kullanılan özelliklerin yüzdesi. |
| reg_alpha |  |  | L1 düzenleme |
| reg_lambda |  |  | L2 düzenleme |
