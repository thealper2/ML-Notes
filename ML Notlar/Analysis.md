# Cohort Analizi
Cohort analizi, bir işletmenin müşteri davranışlarını ve performansını daha iyi anlamak için kullanılan bir veri analizi yöntemidir. Bu yöntem, benzer özelliklere sahip müşteri gruplarını (cohort) oluşturarak, bu grupların zaman içindeki davranışlarını izlemeyi sağlar. Cohort analizinin temel amacı, belirli bir dönemde birlikte başlayan ve benzer özelliklere sahip müşteri gruplarını tanımlamak ve bu grupların performansını izlemek için kullanılır. Cohort analizi, özellikle müşteri sadakati, terk oranları ve gelir analizi gibi konularda işletmelere değerli bilgiler sunar.

```python
import pandas as pd

# Örnek bir veri çerçevesi oluşturalım
data = {'Tarih': ['2023-01-01', '2023-01-01', '2023-02-01', '2023-02-01'],
        'Müşteri_ID': [1, 2, 3, 4],
        'Gelir': [100, 150, 200, 50]}

df = pd.DataFrame(data)

# Müşteri kaydı tarihine göre cohort oluşturma
df['Cohort'] = df.groupby('Tarih')['Müşteri_ID'].transform('min')

# Cohort analizi için gruplama
cohorts = df.groupby(['Cohort', 'Tarih'])['Gelir'].sum().unstack()

# Her cohort'ın ilk aydaki performansını hesaplama
cohort_size = cohorts.iloc[:, 0]
cohorts = cohorts.divide(cohort_size, axis=0)

# Sonuçları yazdırma
print(cohorts)
```

---
# RFM Analizi
RFM analizi, bir işletmenin müşterilerini segmentlere ayırmak ve müşteri davranışını daha iyi anlamak amacıyla kullanılan bir pazarlama analizi yöntemidir.
- **Recency (Yenilik):** Müşterinin son aktivitesinin (örneğin, son satın alma) ne kadar yakın zamanda gerçekleştiğini belirtir. Genellikle bu süre içindeki geçmiş tarih ile analiz yapılır.
- **Frequency (Sıklık):** Müşterinin belirli bir zaman diliminde (örneğin, son bir yıl) yaptığı toplam işlem veya etkileşim sayısını belirtir. Bu sıklık, müşterinin işletmeye ne kadar sık geri döndüğünü yansıtır.
- **Monetary (Parasal Değeri):** Müşterinin toplam gelir veya harcama miktarını belirtir. Bu, müşterinin işletmeye ne kadar para harcadığıını yansıtır.

```python
import pandas as pd

# Örnek bir veri çerçevesi oluşturalım
data = {'Müşteri_ID': [1, 2, 3, 4, 5],
        'Tarih': ['2023-09-10', '2023-10-15', '2023-08-20', '2023-07-05', '2023-09-25'],
        'Miktar': [100, 150, 200, 50, 300]}

df = pd.DataFrame(data)
df['Tarih'] = pd.to_datetime(df['Tarih'])

# Recency hesaplama
max_date = df['Tarih'].max()
df['Recency'] = (max_date - df['Tarih']).dt.days

# Frequency hesaplama
frequency = df.groupby('Müşteri_ID')['Tarih'].count().reset_index()
frequency.rename(columns={'Tarih': 'Frequency'}, inplace=True)
df = df.merge(frequency, on='Müşteri_ID', how='left')

# Monetary hesaplama
monetary = df.groupby('Müşteri_ID')['Miktar'].sum().reset_index()
monetary.rename(columns={'Miktar': 'Monetary'}, inplace=True)
df = df.merge(monetary, on='Müşteri_ID', how='left')

# RFM puanlarını hesaplama
# İşletmenizin kendi puanlama ve segmentasyon kriterlerini tanımlamalısınız.

# Örnek: Recency için, daha düşük değerler daha iyi olduğunu varsayalım.
df['RecencyScore'] = pd.qcut(df['Recency'], q=5, labels=False)

# Örnek: Frequency ve Monetary için, daha yüksek değerler daha iyi olduğunu varsayalım.
df['FrequencyScore'] = pd.qcut(df['Frequency'], q=5, labels=False)
df['MonetaryScore'] = pd.qcut(df['Monetary'], q=5, labels=False)

# RFM toplam puanını hesaplama
df['RFMScore'] = df['RecencyScore'] + df['FrequencyScore'] + df['MonetaryScore']

# Sonuçları görüntüleme
print(df)
```

---
# CRM Analizi (Customer Relationship Management Analysis)
CRM analizi, müşteri ilişkileri yönetimi süreçlerini incelemek, geliştirmek ve optimize etmek için kullanılan bir veri analizi yöntemidir. CRM Analizi, müşteri ilişkilerini daha iyi anlamak, müşteri memnuniyetini artırmak, satışları artırmak ve işletme karlılığını geliştirmek amacıyla kullanılır.

```python
import pandas as pd

# Örnek bir müşteri veri çerçevesi oluşturalım
data = {'Müşteri_ID': [1, 2, 3, 4, 5],
        'Müşteri_Adı': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
        'Satın_Alma_Miktarı': [100, 150, 200, 50, 300],
        'Şikayet_Sayısı': [2, 0, 1, 3, 0],
        'Ziyaret_Sıklığı': [5, 3, 8, 2, 10]}

df = pd.DataFrame(data)

# Örnek bir CRM analizi yapalım
# İşletmenize özgü analiz kriterlerinizi ve hedeflerinizi burada belirlemeniz gerekmektedir.

# Örnek: Müşteri sadakatini değerlendirmek için "Satın_Alma_Miktarı" ve "Ziyaret_Sıklığı" değerlerini kullanalım
df['Sadakat_Skoru'] = (df['Satın_Alma_Miktarı'] * 0.6) + (df['Ziyaret_Sıklığı'] * 0.4)

# Örnek: Şikayet sayısını inceleyerek hizmet kalitesini değerlendirelim
df['Hizmet_Kalitesi'] = df['Şikayet_Sayısı'].apply(lambda x: 'Kötü' if x > 2 else 'İyi')

# Sonuçları görüntüleme
print(df)
```

---
# CLV Analizi (Customer Lifetime Value)
CLV, bir işletmenin müşterilerinin yaşam boyu gelirini tahmin etmek için kullanılan önemli bir metriktir. CLV, bir müşterinin işletmeyle ilişkisi boyunca yarattığı geliri hesaplayarak, işletmelere, müşterilerini daha iyi anlama, pazarlama stratejilerini optimize etme ve müşteri sadakatini artırma konularında yardımcı olur. CLV Formülü:

```shell
        Müşterinin Ortalama Satın Alma Değeri * Satın Alma Sıklığı * Müşterinin Ömrü 
CLV =  -----------------------------------------------------------------------------
                                        İndirim Oranı
```

Bu formülde:
- **Müşterinin Ortalama Satın Alma Değeri:** Bir müşterinin ortalama bir satın alma işlemi sırasında harcadığı miktar.
- **Satın Alma Sıklığı:** Bir müşterinin belirli bir zaman diliminde (örneğin, bir yıl) ne sıklıkta satın alma işlemi yaptığı.
- **Müşterinin Ömrü:** Bir müşterinin işletme ile ilişkisi boyunca geçirdiği süre (aylar veya yıllar cinsinden).
- **İndirim Oranı:** İşletme tarafından verilen indirimler veya kampanyaların etkisiyle düzeltilen bir faktör. Bazı müşteriler daha fazla indirim alabilir.

```python
# Gerekli kütüphaneleri içe aktaralım
import pandas as pd

# Örnek bir müşteri veri çerçevesi oluşturalım
data = {'Müşteri_ID': [1, 2, 3, 4, 5],
        'Müşteri_Adı': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
        'Toplam_Harcama': [1000, 1500, 2000, 500, 3000],
        'Satın_Alma_Sıklığı': [5, 3, 8, 2, 10],
        'Müşteri_Ömrü': [24, 36, 60, 12, 48]}

df = pd.DataFrame(data)

# Ortalama satın alma değeri hesaplama
df['Ortalama_Satın_Alma_Değeri'] = df['Toplam_Harcama'] / df['Satın_Alma_Sıklığı']

# CLV hesaplama
indirim_oranı = 0.1  # Örnek bir indirim oranı
df['CLV'] = (df['Ortalama_Satın_Alma_Değeri'] * df['Satın_Alma_Sıklığı'] * df['Müşteri_Ömrü']) / (1 + indirim_oranı)

# Sonuçları görüntüleme
print(df)
```

