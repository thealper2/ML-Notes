Hipotez testleri, verilerin istatistiksel olarak anlamlı sonuçlar üreterek, belirli hipotezlerin geçerliliğini veya kabul edilip edilmemesi gerektiğini değerlendirmemize yardımcı olur.
1. **Model Performansı Testleri:** Makine öğrenmesi modellerinin performansını değerlendirmek için hipotez testleri kullanılır.
2. **Özellik Seçimi:** Modelin performansını artırabilecek özelliklerin tespitinde hipotez testleri kullanılır. Gereksiz veya zararlı özellikleri eleme, önemli özellikleri belirlemeye yardımcı olur.
3. **A/B Testleri:** A/B testleri, bir değişikliğin (yeni bir model vb.) mevcut bir sisteme etkisini değerlendirmek için kullanılır. İki grup arasındaki farkın anlamlı olup olmadığını belirlemek için kullanılır hipotez testleri yapılır.

Hipotez testlerinin genel işlevleri;
- **Null (H0) ve alternatif (H1) hipotezler belirleme:** Null hipotezi mevcut bir durumu veya varsayımı ifade ederken, alternatif hipotez, bir değişiklik veya farkı ifade eder. Hipotez testleri, bu iki hipotezi karşılaştırarak bir sonuç çıkarır.
- **Veriye dayalı kararlar alma**
- **Anlamlılığı değerlendirme**

# Hipotez Testi Türleri

1. **Z-Testi ve T-Testi:** Bir örneklem verisi ile bir örneklem ortalama arasındaki farkın anlamlı olup olmadığını belirlemek için kullanılır. Eğer popülasyon standart sapması biliniyorsa Z-testi kullanır; bilinmiyorsa ve örneklem büyüklüğü küçükse T-testi kullanır.
2. **İki Örneklem T-testi:** İki farklı önreklem grubu arasındaki ortalama farkın istatistiksel olarak anlamlı olup olmadığını değerlendirmek için kullanılır.
3. **Tek Yön Testi (one-tailed) ve İki Yön Testi (two-tailed):** Tek yön testi, sonuçların sadece bir yönde anlamlı olup olmadığını değerlendirir. İki yön testi, iki yönde de anlamlı olup olmadığını kontrol eder.
4. **Ki-Kare (Chi-Square) Testi:** İki veya daha fazla kategorik değişken arasındaki bağlantıyı veya bağımsızlık ilişkisini incelemek için kullanılır. Özellikle kategori sayısı yüksek olduğunda örneklem büyüklüğü uygun olduğunda kullanışlıdır.
5. **ANOVA (Varyans Analizi):** Üç veya daha fazla grup arasındaki ortalama farklılıkları değerledirmek için kullanılır. Grupların varyanslarının birbirine göre istatistiksel olarak anlamlı farklılık gösterip göstermediğini kontrol eder.
6. **Mann-Whitney U Testi:** İki grup arasındaki medyan değerlerinin farklı olup olmadığını değerlendirmek için kullanılır. Verilerin normal dağılmadığı veya eşit varyansa sahip olmadığı durumlarda kullanılabilir.
7. **Wilcoxon İşaretli Sıralar Testi:** İki bağımlı grup arasındaki farklılığı değerlendirmek için kullanılır. İki grup arasındaki medyan farklılığına odaklanır.
8. **Pearson Korelasyon Katsayısı Testi:** İki sürekli değişken arasındaki ilişkiyi ölçer. Korelasyon katsayısı, değişkenler arasındaki ilişkinin yönünü ve gücünü belirler.

--- 
# A/B Testi
- A/B Testi, iki veya daha fazla farklı sürümün karşılaştırılması amacıyla kullanılan bir istatistiksel deney tasarımıdır. A/B Testi, işletmelerin, web sitelerinin, uygulamaların veya pazarlama stratejilerinin etkisini değerlendirmek ve karşılaştırmak için yaygın olarak kullanılır. A/B test, hangi sürümün daha etkili veya kullanıcılar için daha çekici olduğunu belirlemek için kullanılır.

**A/B Testi işlevleri:**
1. **Farklı sürümleri karşılaştırma**
2. **İstatistiksel anlamda karar verme:** A/B testi, her iki sürüm arasındaki farkın rastgele varyasyondan kaynaklanıp kaynaklanmadığını belirlemek için istatistiksel yöntemler kullanır. 

**Terimler:**
1. **Kontrol Grubu (Grup A):** Mevcut sürüm veya mevcut uygulama olan kontrol grubu olarak adlandırılır.
2. **Deneme Grubu (Grup B):** Yeni bir sürüm veya değişiklik içeren deneme grubu olarak adlandırılır.
3. **Metrik:** Değerlendirilmek istenen anahtar performans göstergesi (KPI). Örneğin tıklanma oranı, dönüşüm oranı, gelir vb.
4. **Hipotezler:** Testin temelini oluşturan hipotezler belirlenir. Genellikle null hipotez (H0) ile alternatif hipotez (H1) olarak iki hipotez kullanılır. **Sıfır hipotezi (null hipotez - H0)**, test edilen iki grubun arasındaki farkın önemli olmadığını savunur. Örneğin, A sınıfı ve B sınıfı adında iki sınıf olduğunu, bu sınıflardaki öğrencilerin not ortalamalarının farklı olup olmadığını test etmek istediğimizi varsayalım. Bu durumda sıfır hipotezi "A sınıfının ve B sınıfının not ortalamalarının arasında bir fark yoktur." olur. **Alternatif hipotez (H1)** ise sıfır hipotezinin tersidir. Yani bu durumda alternatif hipotez, "A sınıfının ve B sınıfının not ortalamalarının arasında fark vardır." olur.

**Örnek Kullanım Senaryoları**
- İşletmenizde veya projenizde farklı sürümler veya değişiklikler yapmak istediğinizde.
- Hangi sürümün veya değişikliğin daha iyi sonuçlar getireceğini anlamak istediğinizde.
- Kullanıcı deneyimini veya iş sonuçlarını iyileştirmek için veriye dayalı kararlar almak istediğinizde.

# Örnek Kod

Bu örnek, iki grup arasındaki ortalama farkı t-testi kullanarak test eder ve sonucu istatistiksel olarak değerlendirir. Eğer p değeri 0.05'ten küçükse, deneme grubunun kontrol grubundan istatistiksel olarak anlamlı bir şekilde farklı olduğu sonucuna varılır. P değeri (p-value), bir hipotez testinin sonucunun istatistiksel anlamlılığını ölçen bir metriktir. P değeri, test edilen hipotezin geçerliliği hakkında bilgi verir. P değeri şu şekilde yorumlanır:

- P değeri küçükse (örneğin, p < 0.05), bu, null hipotezin (H0) reddedildiği ve verilerinizin alternatif hipoteze (H1) daha yakın olduğu anlamına gelir. Yani, p değeri düşük olduğunda, sonuçlar genellikle anlamlıdır ve test edilen değişkenler arasında bir fark olduğu gösterilir.    
- P değeri büyükse (örneğin, p > 0.05), bu, null hipotezin reddedilmediği ve verilerinizin alternatif hipoteze daha uzak olduğu anlamına gelir. Yani, p değeri yüksek olduğunda, sonuçlar genellikle anlamlı değildir ve test edilen değişkenler arasında bir fark olmadığı gösterilir.

Yani, p değeri küçüldükçe, sonuçlar daha anlamlı hale gelir. Bu nedenle, p değerinin küçük olması, genellikle hipotez testlerinde tercih edilen bir durumdur, çünkü bu, verilerin test edilen değişkenler arasında bir ilişki olduğunu gösterdiği anlamına gelir.


```python
import numpy as np
import scipy.stats as stats

control_group = [0, 1, 1, 1, 0, 1, 0, 0, 1, 0]
treatment_group = [1, 1, 1, 1, 1, 0, 1, 0, 1, 0]

control_mean = np.mean(control_group)
treatment_mean = np.mean(treatment_group)

# T-testi
t_stat, p_value = stats.ttest_ind(control_group, treatment_group)

if p_value < 0.05:
    print("Deneme grubu istatistiksel olarak anlamlı bir fark yarattı.")
else:
    print("Deneme grubu istatistiksel olarak anlamlı bir fark yaratmadı.")
```

---
# Z-Testi
 Z testi, bir örneklem verisinin popülasyon parametreleri hakkında istatistiksel bir hipotez testi yapmak için kullanılan bir istatistiksel testtir. Z testi, özellikle popülasyonun standart sapması bilindiğinde veya örneklem büyüklüğü büyük olduğunda kullanılır. İki türü vardır:
- **Tek örneklem Z testi**: Bir popülasyonun ortalama değerinin belirli bir değere eşit olup olmadığını test etmek için kullanılır. Örneklem verisi ile popülasyon parametresi arasındaki farkın anlamlı olup olmadığını değerlendirmek için kullanılır.
- **İki örneklem Z testi**: ;ki farklı örneklem grubunun ortalama değerlerinin birbirine eşit olup olmadığını test etmek için kullanılır. Örneklem verileri arasındaki farkın istatistiksel olarak anlamlı olup olmadığını değerlendirir.

```shell
           Xˉ - μ
Z = -------------------
        (σ / sqrt(n))
```

- Z, Z istatistiğini temsil eder.
- Xˉ, örneklem ortalama değerini temsil eder.
- μ, popülasyon ortalama değerini temsil eder.
- σ, popülasyon standart sapmasını temsil eder.
- n, örneklem büyüklüğünü temsil eder.

**Örnek Kullanım Senaryoları**
- Bir popülasyonun ortalama değerini test etmek istediğinizde. 
- İki örneklem arasındaki ortalama farkı test etmek istediğinizde (iki örneklem Z testi).
- Örneklem büyüklüğü büyükse ve popülasyon standart sapması biliniyorsa.

# Örnek Kod

```python
import numpy as np
from scipy import stats

sample_data = [25, 30, 35, 40, 45, 50]
population_mean = 45
population_stddev = 5

# Örneklem büyüklüğü
n = len(sample_data)

# Z istatistiği
z_statistic = (np.mean(sample_data) - population_mean) / (population_stddev / np.sqrt(n))

# P değeri
p_value = 2 * (1 - stats.norm.cdf(abs(z_statistic)))

print("Z istatistiği:", z_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: Örneklem popülasyon ortalamasından farklıdır.")
else:
    print("Null hipotez kabul edildi: Örneklem popülasyon ortalamasından farklı değildir.")
```

---

# T-Testi
T testi (Student's t-test), iki grup arasındaki ortalamaların istatistiksel olarak anlamlı bir farklılık gösterip göstermediğini değerlendirmek için kullanılan bir istatistiksel test türüdür. T testi, örneklem verilerinin popülasyon parametreleri hakkında istatistiksel bir hipotez testi yapmak için kullanılır. T testi, özellikle popülasyon standart sapması bilinmediğinde veya örneklem büyüklüğü küçük olduğunda kullanışlıdır. İki türü vardır:
- **Bağımsız Örneklem T-Testi:** İki farklı bağımsız örneklem grubunun ortalama değerleri arasındaki farkı test etmek için kullanılır. Örneğin, iki farklı grup arasındaki ortalama yaş farkını değerlendirmek istendiğinde bağımsız örneklem t-testi kullanılabilir.
- **Bağımlı Örneklem T-Testi (Eşleştirilmiş T-Test):** Aynı örneklemden alınan iki farklı örneklem grubunun ortalama değerleri arasındaki farkı test etmek için kullanılır. Örneğin, aynı kişilerin kilo kaybı ölçümleri arasındaki farkı değerlendirmek için bağımlı örneklem t-testi kullanılabilir.

# Örnek Kod

```python
import numpy as np
from scipy import stats

group1 = [25, 30, 35, 40, 45]
group2 = [30, 35, 40, 45, 50]

# Bağımsız örneklem T-testi
t_statistic, p_value = stats.ttest_ind(group1, group2)

print("T istatistiği:", t_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: İki grup arasında istatistiksel olarak anlamlı bir fark vardır.")
else:
    print("Null hipotez kabul edildi: İki grup arasında istatistiksel olarak anlamlı bir fark yoktur.")
```

---

# Tek Yön Testi (One-Tailed Test)

  
Tek yönlü test (one-tailed test), hipotez testleri sırasında, anlamlılık düzeyini bir yönde değerlendirmenize olanak tanır. Yani, test edilen hipotez, sadece bir yönde anlamlılık aranmasına dayanır. Tek yönlü testler, hipotezinizin yönünü ve beklenen sonucu önceden belirlediğinizde kullanışlıdır. Tek yönlü testlerin iki temel türü vardır:

-  **Sağa Tek Yönlü Test (Right-Tailed Test):** Sağa tek yönlü testlerde, hipotez, popülasyon parametresinin belirli bir değerden büyük olduğunu test eder. Örneğin, bir yeni tedavi yöntemi ile ilgili hipotez, tedavi grubunun kontrol grubundan daha iyi olduğunu iddia ediyorsa, sağa tek yönlü bir test kullanılabilir.
- **Sola Tek Yönlü Test (Left-Tailed Test):** Sola tek yönlü testlerde, hipotez, popülasyon parametresinin belirli bir değerden küçük olduğunu test eder. Örneğin, bir yeni ilacın yan etkileri ile ilgili hipotez, ilacın yan etkilerinin kontrol grubundan daha düşük olduğunu iddia ediyorsa, sola tek yönlü bir test kullanılabilir.

# Örnek Kod

```python
import numpy as np
from scipy import stats

data = [25, 30, 35, 40, 45, 50]
population_mean = 40  # Hipotez: Ortalama popülasyon değeri 40'tan büyüktür

# T testi yapın (sağa tek yönlü test)
t_statistic, p_value = stats.ttest_1samp(data, population_mean)

print("T istatistiği:", t_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: Ortalama popülasyon değeri 40'tan büyüktür.")
else:
    print("Null hipotez kabul edildi: Ortalama popülasyon değeri 40'tan büyük değildir.")
```

---

# İki Yön Testi (Two-Tailed Test)
  
İki yönlü test (two-tailed test), hipotez testleri sırasında, anlamlılık düzeyini her iki yönde de değerlendirmenize olanak tanır. Yani, test edilen hipotez, popülasyon parametresinin belirli bir değerden farklı olduğunu test eder, ancak farkın hangi yönde olduğu önceden belirli değildir. İki yönlü testler, hipotezinizin yönünü önceden belirlemediğiniz ve iki yönde de anlamlılığı değerlendirmek istediğiniz durumlarda kullanışlıdır. İki yönlü testlerin iki temel türü vardır:

- **Sağa ve Sola İki Yönlü Test (Two-Tailed Test):** İki yönlü testlerde, hipotez, popülasyon parametresinin belirli bir değerden farklı olduğunu test eder, ancak bu farkın hangi yönde olduğu önceden belirli değildir. Bu testler iki yönde anlamlılığı değerlendirirler.  
- **Yüzde 50 Oranlı İki Yönlü Test (Two-Tailed Test):** Bu tür bir iki yönlü test, hipotezinizi yalnızca bir yönde değil, iki yönde de test etmek istediğinizde kullanılır. Örneğin, bir yeni tedavi yönteminin kontrol grubuna göre daha iyi veya daha kötü olup olmadığını değerlendirmek için kullanılabilir.  

İki yönlü testler, hipotezinizin yönünü önceden belirlemediğinizde ve hangi yönde anlamlılığı değerlendirmek istediğinizde kullanışlıdır.

# Örnek Kod

```python
import numpy as np
from scipy import stats

group1 = [25, 30, 35, 40, 45]
group2 = [30, 35, 40, 45, 50]

# İki yönlü T testi
t_statistic, p_value = stats.ttest_ind(group1, group2)

print("T istatistiği:", t_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: İki grup arasında istatistiksel olarak anlamlı bir fark vardır.")
else:
    print("Null hipotez kabul edildi: İki grup arasında istatistiksel olarak anlamlı bir fark yoktur.")
```

---
# Ki-Kare Testi (Chi-Square Test)

Ki-kare testi (Chi-Square test), iki veya daha fazla kategorik değişken arasındaki ilişkiyi veya bağımsızlık ilişkisini değerlendirmek için kullanılan bir istatistiksel testtir. Ki-kare testi, veri seti içindeki gözlemleri ve beklenen frekansları karşılaştırarak, değişkenler arasındaki bağlantıyı veya bağımsızlığı değerlendirir. Ki-kare testi, verilerin ayrık (kategorik) olduğu durumlar için kullanışlıdır. Ki-kare testinin iki temel türü vardır:
- **Ki-Kare Bağımsızlık Testi (Chi-Square Independence Test):** Bu test, iki veya daha fazla kategorik değişkenin bağımsızlık ilişkisini değerlendirir. Örneğin, bir ürünün tercih edilme durumu ile cinsiyet arasındaki ilişkiyi incelemek için bu testi kullanabilirsiniz.
- **Ki-Kare Uyum Testi (Chi-Square Goodness-of-Fit Test):** Bu test, bir örneklem verisinin belirli bir teorik dağılıma uyup uymadığını değerlendirir. Örneğin, bir zarın adil olup olmadığını test etmek için bu testi kullanabilirsiniz.

# Örnek Kod

```python
import numpy as np
from scipy import stats

observed_data = np.array([[30, 10], [20, 25]])
# Ki-Kare
chi2, p, _, _ = stats.chi2_contingency(observed_data)

print("Ki-kare istatistiği:", chi2)
print("P değeri:", p)

alpha = 0.05
if p < alpha:
    print("Null hipotez reddedildi: İki değişken arasında bağımsızlık yoktur.")
else:
    print("Null hipotez kabul edildi: İki değişken arasında bağımsızlık vardır.")
```

---

# ANOVA (Analysis of Variance) Test
ANOVA (Analysis of Variance), birden fazla grup arasındaki istatistiksel anlamlılığı değerlendirmek için kullanılan bir istatistiksel analiz tekniğidir. ANOVA, grupların ortalamaları arasındaki farklılıkları inceleyerek, gruplar arasında anlamlı bir fark olup olmadığını belirler. ANOVA, özellikle gruplar arasındaki varyansı karşılaştırır. ANOVA'nın iki temel türü vardır:
- **Tek Yönlü ANOVA (One-Way ANOVA):** Tek bir bağımsız değişkenin (grup) birden fazla düzeyi arasındaki farkı test etmek için kullanılır. Örneğin, farklı dozaj seviyelerine sahip üç farklı ilaç grubu arasındaki etkileri karşılaştırmak için tek yönlü ANOVA kullanabilirsiniz.
- **İki Yönlü ANOVA (Two-Way ANOVA):** İki bağımsız değişkenin (grup ve faktör) etkilerini incelemek için kullanılır. İki yönlü ANOVA, gruplar arası ve faktörler arası etkileri ayrı ayrı ve etkileşim etkisini de değerlendirir.

# Örnek Kod

```python
import numpy as np
from scipy import stats

group1 = [65, 72, 75, 68, 69]
group2 = [72, 78, 82, 74, 70]
group3 = [60, 65, 73, 68, 75]

# Tek yönlü ANOVA 
f_statistic, p_value = stats.f_oneway(group1, group2, group3)

print("F istatistiği:", f_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: Gruplar arasında anlamlı bir fark vardır.")
else:
    print("Null hipotez kabul edildi: Gruplar arasında anlamlı bir fark yoktur.")
```

---

# Mann-Whitney U Testi

Mann-Whitney U testi, iki bağımsız örneklem grubunun medyan değerleri arasındaki istatistiksel anlamlılığı değerlendirmek için kullanılan bir non-parametrik hipotez testidir. Mann-Whitney U testi, verilerin dağılımının normalliğini karşılamadığında veya sıralı verilerle çalışıldığında kullanışlıdır. Bu test, grupların merkezi eğilimlerini karşılaştırır ve gruplar arasındaki farkı test eder. Mann-Whitney U testinin iki ana türü vardır:
- **Bağımsız Mann-Whitney U Testi:** İki bağımsız örneklem grubunun medyan değerleri arasındaki farkı test etmek için kullanılır. Bu test, gruplar arasındaki medyan değerlerinin farklı olup olmadığını değerlendirir.
- **İçiçe Mann-Whitney U Testi:** Aynı örneklem grubunun farklı koşullar altında elde edilen verilerinin medyan değerlerini karşılaştırmak için kullanılır. Bu test, aynı grup içindeki iki koşulun medyan değerleri arasındaki farkı test eder.

# Örnek Kod

```python
import numpy as np
from scipy import stats

group1 = [25, 30, 35, 40, 45]
group2 = [30, 35, 40, 45, 50]

# Bağımsız Mann-Whitney U Testi
U_statistic, p_value = stats.mannwhitneyu(group1, group2)

print("U istatistiği:", U_statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: Gruplar arasında anlamlı bir medyan farkı vardır.")
else:
    print("Null hipotez kabul edildi: Gruplar arasında anlamlı bir medyan farkı yoktur.")
```

---

# Wilcoxon İşaretli Sıralar Testi  
Wilcoxon İşaretli Sıralar Testi (Wilcoxon Signed-Rank Test), bir grup içindeki iki bağımlı örneklem arasındaki medyan farkını değerlendirmek için kullanılan bir non-parametrik hipotez testidir. Bu test, gruplar arasındaki merkezi eğilimin farklı olup olmadığını belirlemek amacıyla kullanılır. Wilcoxon İşaretli Sıralar Testi, verilerin normallik varsayımını karşılayamadığında veya sıralı verilerle çalışıldığında tercih edilir. Wilcoxon İşaretli Sıralar Testi'nin iki temel türü vardır:

- **İki Örneklem Wilcoxon İşaretli Sıralar Testi:** İki bağımlı grup arasındaki medyan farkını test etmek için kullanılır. Bu test, aynı gruptaki iki farklı koşul altında elde edilen verilerin medyanlarını karşılaştırır.
- **Bir Örneklem Wilcoxon İşaretli Sıralar Testi:** Bir grup içindeki örneklem verilerinin medyan değeri ile bir teorik medyan değerini karşılaştırmak için kullanılır. Bu test, bir grup içindeki verilerin bir teorik dağılıma uygunluğunu değerlendirir.

# Örnek Kod

```python
import numpy as np
from scipy import stats

group1 = [25, 30, 35, 40, 45]
group2 = [30, 35, 40, 45, 50]

# İki örneklem Wilcoxon İşaretli Sıralar Testi
statistic, p_value = stats.wilcoxon(group1, group2)

print("Test istatistiği:", statistic)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Null hipotez reddedildi: Gruplar arasında anlamlı bir medyan farkı vardır.")
else:
    print("Null hipotez kabul edildi: Gruplar arasında anlamlı bir medyan farkı yoktur.")
```

---

# Pearsons Korelasyon Testi
Pearson Korelasyon Testi, iki sürekli değişken arasındaki ilişkiyi değerlendirmek için kullanılan bir parametrik istatistiksel testtir. Pearson Korelasyonu, bu iki değişken arasındaki lineer ilişkiyi ölçer ve bu ilişkinin ne kadar güçlü olduğunu ifade eder. Korelasyon, iki değişkenin nasıl birlikte değiştiğini incelemek için kullanılır. Pearson korelasyonunun iki ana formülü vardır:
- **Pearson Korelasyon Katsayısı (r):** Bu, iki sürekli değişken arasındaki lineer ilişkiyi ölçer. Pearson korelasyonu, -1 ile 1 arasında bir değere sahiptir. -1, tam tersi bir ilişkiyi, 1 ise mükemmel bir pozitif ilişkiyi ifade eder. 0 ise ilişki olmadığını gösterir.   
- **Pearson Korelasyon Katsayısı İnferansı:** Korelasyon katsayısının anlamlılığını değerlendirmek için kullanılır. Bu, korelasyonun rastgele mi yoksa gerçek bir ilişkiyi yansıttığını belirlemeye yardımcı olur.

# Örnek Kod

```python
import numpy as np
from scipy import stats

x = np.array([2, 4, 6, 8, 10])
y = np.array([1, 3, 5, 7, 9])

# Pearson Korelasyon Katsayısı ve p değeri
correlation_coefficient, p_value = stats.pearsonr(x, y)

print("Pearson Korelasyon Katsayısı (r):", correlation_coefficient)
print("P değeri:", p_value)

alpha = 0.05
if p_value < alpha:
    print("Korelasyon anlamlıdır: İki değişken arasında anlamlı bir lineer ilişki vardır.")
else:
    print("Korelasyon anlamlı değildir: İki değişken arasında anlamlı bir lineer ilişki yoktur.")
```

