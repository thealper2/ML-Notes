L1 (Lasso) ve L2 (Ridge) düzenlemesinin bir kombinasyonunu kullanır. L1 ve L2 düzenleme terimlerini kontrol etmek için "alpha" parametresini kullanır.
Alpha = 0 ise L2 uygulanır, böylece ElasticNet, Ridge regresyonuna dönüşür. Alpha = 1 ise L1 uygulanır, böylece ElasticNet, Lasso regresyonuna dönüşür.

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| alpha | float | 1.0 | L1 ve L2 regularizasyon birleşimini kontrol eder. |
| l1_ratio | float | 0.5 | L1'in dağılımı. |
| max_iter | int | 1000 | Optimizasyon algoritmasının maksimum iterasyon sayısı. |
| tol | float | 1e-4 | Optimizasyon algoritmasının toleransı. |
