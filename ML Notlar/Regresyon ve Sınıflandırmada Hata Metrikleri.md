# Sınıflandırma Metrikleri

---
#### Karmaşıklık Matrisi (Confusion Matrix):
- Karmaşıklık matrisi, sınıflandırma performasını ölçmek için kullanılır. Sütunlar gerçek verileri, satırlar ise tahmin edilen verileri gösterir.

```shell
# Sütunlar gerçek
# Satırlar Tahmin
[ TP FP ]
[ FN TN ]
```

**True Positive (TP):** Hasta olduğunu düşündünüz ve gerçekten hastasınız.
**True Negative (TN):** Hasta olmadığını düşündünüz ve hasta değilsiniz.
**False Positive (FP):** Hasta olduğunu düşündünüz fakat hasta değilsiniz.
**False Negative (FN):** Hasta olmadığınızı düşündünüz fakat hastasınız.

**False Positive Rate (FPR):** 

```shell
							  FP          FP
False Positive Rate (FPR): --------- = --------
							FP + TN       N 
N => Total Negative
```

**True Positive Rate (TPR):**

```shell
						         TP           TP
True Positive Rate (TPR) = ------------- = -------
								TP + FN       P
P => Total Positive
```

**False Negative Rate (FNR):**

```shell
						         FN           FN
False Negative Rate (FNR) = ------------- = ------
							   TP + FN        P
P => Total Positive
```

**True Negative Rate (TNR):**

```shell
							   TN         TN
True Negative Rate (TNR) = ---------- = -------
							TN + FP        P
P => Total Positive
```


#### Duyarlılık Skoru (Recall Score):
- Duyarlılık, modelinizin pozitif olan verilerin ne kadarını pozitif olarak tahmin ettiğini gösterir. FN tahminlemenin maliyetinin yüksek olduğu durumlarda önemlidir. Duyarlılık yüksekse, model daha fazla gerçek pozitifi tespit edebiliyor demektir.

```shell
		        TP
Recall = -------------------
			  TP + FN
```

#### Kesinlik Skoru (Precision / Sensitivity Score):
- Kesinlik, modelizin pozitif olarak tahmin ettiği verilerin gerçekte ne kadarının pozitif olduğudur. FP tahminlemenin maliyetinin yüksek olduğu durumlarda önemlidir. Precision ile Recall ters orantılıdır ve ikisinin arasında bir denge sağlamak gerekir (precision recall trade-off). Kesinlik yüksekse, modelin pozitif tahminleri genellikle doğru demektir.

```shell
		          TP
Precision = -------------------
				TP + FP
```

#### Precision-Recall Trade-off:
- Modelin kesinlik ve duyarlılık arasındaki dengeyi nasıl ayarladığını gösterir. İdeal bir model, hem yüksek kesinlik hem de yüksek duyarlılık sağlar. Birçok sınıflandırma algoritması, bu dengeyi kurmak için eşik değeri sunar. Eşik değeri değiştikçe, modelin kesinlik ve duyarlılık değerleri değişir. Örneğin eşik değeri yükseltildiğinde kesinlik artar ancak doğruluk düşer. Tam tersi, eşik değeri düşürüldüğünde duyarlılık artar ancak kesinlik düşer. Bir uygulamada, kesinlik ve duyarlılık arasındaki tradeof, problem bağlamına ve hedeflere bağlı olarak ayarlanır. Örneğin, tıbbi bir teşhis uygulamasında daha yüksek bir duyarlılık kritik olabilirken, spam e-posta filtrelemesi gibi bir uygulamada daha yüksek kesinlik öncelikli olabilir.
#### Doğruluk Skoru (Accuracy Score):
- Doğruluk, modelinizin doğru tahmin ettiği verilerin toplam veri kümesine oranını gösterir. 

```shell
		         TP + TN
Accuracy = -------------------
			TP + TN + FP + FN
```

#### F1 Skoru (F1 Score):
- F1, kesinlik ve duyarlılık skorlarının harmonik ortalamasını gösterir. Harmonik olmasının sebebi; eğer basit bir ortalama hesaplansaydı Precision Değeri 1 ve Recall Değeri 0 olan bir modelin skoru 0.5 olacaktır ve bu bizi yanıltacaktır. Eşit dağılmayan veri kümelerinde (imbalanced) hatalı bir model seçimi yapmamak için accuracy yerine f1 değerine bakılır.

```shell
		       Precision * Recall
F1 = 2 * -------------------
			   Precision + Recall
```

#### ROC - AUC Eğrisi (ROC-AUC Curve)
- ROC modelin TPR ile FPR cinsinden ne kadar iyi ayrım yapabildiğini açıklar. AUC, ROC eğrisinin altında kalan alanı verir, 0-1 arasındadır. 0'ise bütün tahminler yanlıştır. 1'e yaklaştıkça modelin performansı iyileşir. ROC-AUC 0.5 ise, modelin performansı rastgele tahmin etmekle (yazı-tura tahmini %50-%50) aynıdır.

# Regresyon Metrikleri

---
#### R-Squared (R-Kare)
- R2, bağımlı değişkenin varyansının bağımsız değişkenler tarafından ne kadar açıklandığını gösterir. 0 ile 1 arasında değer alır. En iyi R2 değeri 1'dir. Daha yüksek R2 değerleri modelin veriyi daha iyi açıkladığını gösterir. R2 eksi değer alırsa, modelin underfit edildiğini gösterir. Multivariate Regression'da R2 yerine adjusted-r2 değerine bakılır.

```shell
			MSE(model)
R2 = 1 - ---------------
			MSE(mean)
```
 
#### Mean Squared Error (MSE)
- MSE, bir regresyon modelinin tahminlerinin gerçek değerlerden ne kadar sapma gösterdiğini ölçer. Her bir gözlem için hata karelerinin ortalaması alınır. Daha yüksek MSE değerleri, daha büyük hata anlamına gelir. MSE değeri ne kadar düşükse, modelin tahminlerinin gerçek değerlere o kadar yakın olduğunu gösterir. MSE sıfıra yaklaştıkça model daha iyi performans gösterir.

```shell
MSE = (1/n) * Σ(yi - ŷi)², n gözlem sayısını, yi gerçek değeri, ŷi tahmini değeri temsil eder.
```

#### Mean Absolute Error (MAE):
- MAE, bir regresyon modelinin tahminlerinin gerçek değerlerden ortalama mutlak sapma gösterdiğini ölçer. Her bir gözlem için mutlak hataların ortalaması alınır. Düşük MAE değeri, modelin tahminlerinin gerçek değerlere yakın olduğunu gösterir. MAE sıfıra yaklaştıkça model daha iyi performans gösterir.

```shell
MAE = (1/n) * Σ|yi - ŷi|, n gözlem sayısını, yi gerçek değeri, ŷi tahmini değeri temsil eder.
```
#### Root Mean Squared Error (RMSE):
- RMSE, MSE'nin kareköküdür. MSE'den farkı, hataların karelerinin büyüklüklerini daha iyi ifade etmesidir. RMSE değeri ne kadar düşükse, modelin tahminlerinin gerçek değerlere o kadar yakın olduğunu gösterir. RMSE sıfıra yaklaştıkça model daha iyi performans gösterir.

```shell
RMSE = √MSE
```

#### Mean Percentage Error (MPE):
- MPE, tahmin hatalarının gerçek değerlere göre yüzde olarak ne kadar sapma gösterdiğini ölçer. Pozitif ve negatif hataların etkisi birbirini sıfırlayabilir. MPE değeri ne kadar düşükse, modelin tahminlerinin gerçek değerlere ne kadar yakın olduğunu gösterir. MPE sıfıra yaklaştıkça model daha iyi performans gösterir.

```shell
MPE = (1/n) * Σ((yi - ŷi) / yi) * 100, n gözlem sayısını, yi gerçek değeri, ŷi tahmini değeri temsil eder.
```

