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

#### Balanced Accuracy Score 
- Dengesiz veri kümelerinde kullanılır. Her sınıfın doğruluk oranını dengeler ve ardından tüm sınıfların doğruluk oranlarının ortalamasını alır. Her bir sınıfın veri dağılımındaki etkisini eşit şekilde değerlendirir.

```shell
(1 / N) * E(TP / P)
```

#### Top K Accuracy Score
- Modelin en yüksek olasılığı sahip olan k tahmininin doğru sınıfı içerip içermediğini kontrol eder. Genelde çoklu sınıflı sınıflandırma problemlerinde kullanılır. 
```shell
(1 / N) * E(1 => If true class in top-k predictions else 0)
```

#### Average Precision Score
- Dengesiz veri kümelerinde ve precision-recall analizlerinde kullanılır. Modelin gerçek pozitiflerini doğru bir şekilde saptama yeteneği ve yanlış pozitifler oluşturma konusundaki hassasiyetini gösterir. Precision-Recall eğrisi altında kalan alanı ifade eder. Precision-Recall eğrisi farklı kesme noktalarındaki precision ve recall değerlerini gösterir. Average precision, bu eğrinin altındaki alanın ortalamasını alarak hesaplanır. 1'e ne kadar yakınsa model o kadar iyi performans göstermiştir.

```shell
(1 / N) * E(Recall değeri k - Recall değeri k-1) * (Recall değeri k olduğunda Precision)
```

#### Log Loss
- Sınıflandırma modellerinin tahminlerinin olasılık dağılımıyla uyumunu ölçen bir metriktir. Gerçek etiketlerin olasılık dağılımı ve modelin ürettiği olasılık dağılımı arasındaki farkı ölçerek modelin kalitesini değerlendirir. Ne kadar düşükse o kadar iyidir. Modelin tahminleri gerçek etiketlere daha yakınsa, log_loss değeri daha düşük olur. Model ne kadar belirsiz tahminler yapıyorsa log_loss o kadar yüksek olur.

#### Jaccard Score
- İkili sınıflandırma problemleri için kullanılır. Modelin gerçek pozitif ve negatif sınıfları ne kadar iyi tahmin ettiğini ölçer. Gerçek ve tahmin edilen sınıfların kesişimini gerçek ve tahmin edilen sınıfların birleşimine böler. 1'e ne kadar yakınsa o kadar iyidir.

```shell
TP / (TP + FP + FN)
```

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

#### Explained Variance Score
Modelin verideki değişkenliğin ne kadarını açıkladığını ölçer. 1' ne kadar yakınsa o kadar iyidir. Eğer 0 ise model verideki değişkenliği açıklayamıyor demektir. Eğer negatif ise model basit bir ortalama kullanmaktan daha kötü performans gösteriyor demektir. Modelin gerçek değerler üzerinde ne kadar başarılı tahminler yaptığını ve bu tahminlerin gerçek verideki değişkenliği ne kadar açıkladığını anlamak için kullanılır.

```shell
1 - ( (Var(y-y^) / (Var(y)) ) )
```

#### Max Error
Modelin gerçek ve tahmin edilen değerler arasındaki en büyük farkı ölçer. Gerçek ve tahmin edilen değerler arasındaki maksimum mutlak farkı ifade eder. 

```shell
max(|yi - yi^|)
```

# Clustering Metrikleri
---
#### Mutual Info Score
Gerçek sınıf metrikleri ile kümele sonuçları arasındaki ilişkiyi ölçer. Yüksek MIS değeri, kümeleme sonuçlarının gerçek sınıf etiketleriyle güçlü bir şekilde ilişkili olduğunu ve algoritmanın veri yapısını doğru bir şekilde kavradığını gösterir. Düşük MIS değeri, kümeleme sonuçlarının gerçek sınıf etiketlerine göre zayıf bir ilişki içinde olduğunu ve algoritmanın iyileştirilmesi gerektiğini gösterir.

```shell
MutualInfo(X, Y) / sqrt(Entropy(X)*Entropy(Y))
```

#### Rand Score
Doğru olarak eşleştirilen örneklerin toplam örnek sayısına oranını hesaplar. 1'e ne kadar yakınsa o kadar iyi. Yüksek rand score, kümeleme sonuçlarının gerçek sınıf etiketleriyle iyi uyum içinde olduğunu ve doğru örneklerin bir araya getirildiğini gösterir.

```shell
(TP + TN) / (TP + FP + FN + TN)
```

#### Completeness Score
Kümeleme sonuçları içinde aynı gerçek sınıfa ait olan örneklerin aynı kümede bir araya gelip gelmediğini ölçer. 1'e ne kadar yakınsa o kadar iyi. Yüksek Completeness Score, kümeleme sonuçlarının gerçek sınıfları tamamen yakaladığını ve aynı gerçek sınıfa ait olan örneklerin aynı kümede bir araya geldiğini gösterir.

```shell

```

#### Homogenity Score
Her kümenin tek sınıfa ait olup olmadığını ölçer. 1' ne kadar yakınsa o kadar iyi. Yüksek homojenlik, kümeleme sonuçlarının her kümenin tek bir gerçek sınıfa ait olduğunu ve homojen olduğunu gösterir.

```shell
1 - ( (Kümeleme sonuçlarına göre gerçek sınıfların entropi değeri) / (gerçek sınıfların entropi değeri) )
```

#### V-Measure Score
Homojenlik ve tamamlanmışlık skorlarının harmonik ortalamasını alarak birleştirir. Yüksek V-Measure Score, kümeleme sonuçlarının hem homojenlik hem de tamamlanmışlık açısından başarılı olduğunu gösterir.

```shell
2 * ( (homogenity * completeness) / (homogenity + completeness) )
```

