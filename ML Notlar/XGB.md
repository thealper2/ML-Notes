

# Hyperparameters

Hiperparametreleri dörde ayrılır:
1. General parameters
2. Booster parameters
3. Learning task parameters
4. Command line parameters (Sadece konsol ekranında ayarlanır.)

#### General Parameters

| Parameters | Types | Default | Description |
| - | - | - | - |
| booster | gbtree - dart - gblinear | gbtree | Her iterasyonda çalışıtırılcak model türü. Gbtree ve dart tree-based, gblinear linear yapıdadır. |
| verbosity | 0 (silent), 1 (warning), 2 (info), 3 (debug) | 1 | Çıktı |
| nthread | integer | mevcut maksimum iş parçacığı sayısı | Kullanılan iş parçacığı sayısıdır. Bu paralel işleme için kullanılır ve sistemdeki çekirdek sayısı girilmelidir. Eğer tüm çekirdeklerde çalıılmak istenirse değer girilmez, algoritma otomatik olarak ayarlar. |

#### Booster Parameters

| Parameters | Types | Default | Description |
| - | - | - | - |
| eta / learning_rate | [0-1] | 0.3 |  Overfittingi önlemek için kullanılan adım boyutu küçültmesidir. Genelde 0.01-0.2 arasında bir değer verilir. |
| gamma / min_split_loss | [0, inf] | 0 | Kayıp fonksiyonunda pozitif bir azaltma sağlandığında bölünür. |
| max_depth | [0, inf] | 6 | Overfittingi önlemek için kullanılır. Yüksek derinlik, modeli daha karmaşık hale getirerek overfittingi arttıracaktır. Derinlik arttıkça bellek kullanımı artar. CV kullanarak ayarlanmalıdır. Genelde 3-10 arasında değer verilir. |
| min_child_weight | [0, inf] | 1 | Overfittingi önlemek için kullanılır. Yüksek değerler, modelin örneğe özgü olabilecek belirli özellikleri öğrenmesini engelleyebilir. Çok yüksek değerler underfittinge yol açabilir. CV kullanarak ayarlanmalıdır. |
| max_delta_step | [0, inf] | 0 | Genelde kullanılmaz, ancak sınıf aşırı dengesiz olduğunda yardımcı olabilir. Genelde 1-10 arasında kullanılır. |
| subsample | (0, 1] | 1 | Rastgele örneklenecek gözlemlerin oranını belirtir. 0.5 olarak ayarlanırsa, eğitim verilerinin yarısını örnekleyeceği anlamına gelir, bu da overfittingi önler. Düşük olması overfittingi önler, çok küçük olması underfittinge yol açabilir. Gnenelde 0.5-1 arasında değer verilir. |
| colsample_bytree <br/> colsample_by_level <br/> colsample_by_node | (0, 1] | 1 | Sütunların alt örnekleme oranı. |
| lambda / reg_lambda | int | 1 | L2 regülasyon düzenlemesi. | 
| alpha / reg_alpha | int | 0 | L1 regülasyon düzenlemesi | 
| tree_method | auto, exact, approx, hist, gpu_hist | auto | Ağaç oluşturma algoritması. auto'da kullanılması önerilir. Küçük-orta veri setlerinde "exact", büyük veri setlerinde "approx".  hist, optimize edilmiş algoritma. |
| scale_pos_weight | int | 1 | Pozitif-negatif ağırlık dengesi. Dengesiz sınıflarda kullanışlıdır. toplam(negatif) / toplam(pozitif) kullanılmalı. |
| max_leaves | int | 0 | Eklenecek maksimum düğüm sayısı. |

#### Learning Task Parameters

| Parameters | Types | Default | Description |
| - | - | - | - |
| objective | reg:squarederror <br/> reg:squaredlogerror <br/> reg:logistic <br/> binary:logistic <br/> binary:hinge <br/> multi:softmax <br/> multi:softprob | reg:squarederror | Minimize edilecek kayıp fonksiyonu |
| eval_metric | rmse, ame, logloss, error, merror, mlogloss, auc, aucpr | regression için rmse <br/> classification için error <br/> ranking için mae | Doğrulama verileri için kullanılacak metrik. |
| seed | int | 0 | Random seed. |


