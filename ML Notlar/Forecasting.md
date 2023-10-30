Zaman serisi analizi, zaman içinde gözlenen verileri incelemek ve bu verilerin gelecekteki değerlerini tahmin etmek amacıyla istatistiksel ve veri madenciliği tekniklerinin uygulanmasıdır. Zaman serisi verileri, belirli bir zaman diliminde toplanan verileri temsil eder ve genellikle düzenli zaman aralıklarıyla gözlenir. 

Zaman Serisi Modelleri: 
ARIMA (Oto-Regressif Entegre Hareketli Ortalama), 
GARCH (Genelleştirilmiş Oto-Regressif Koşullu Heteroskedastiklik), 
Exponential Smoothing (Üssel Düzleştirme)

# Zaman Serisi Bileşenleri

### Trend
Trend, zaman içinde sürekli bir artış, azalış veya istikrarlı bir eğilimi ifade eder. Bu, bir zaman serisinin orta veya uzun vadeli değişimini temsil eder.

**Hareketli Ortalama (Moving Average):** Zaman serisindeki gürültüyü azaltmak ve trendi yakalamak için hareketli ortalama yöntemi kullanılabilir. Basit bir hareketli ortalama veya ağırlıklı hareketli ortalama kullanılabilir.

```python
# Basit bir hareketli ortalama hesaplama
rolling_mean = time_series.rolling(window=10).mean()
```

**Lowess Düzleştirmesi:** Lowess (Locally Weighted Scatterplot Smoothing) düzleştirmesi, veriyi yumuşatarak ve yerel eğilimleri yakalayarak trendi belirlemek için kullanılır.

```python
from statsmodels.nonparametric.smoothers_lowess import lowess

# Lowess düzleştirmesi ile trendi hesaplayın
smoothed = lowess(time_series, np.arange(len(time_series)), frac=0.2)

# Lowess düzleştirmesi sonuçlarını görselleştirin
plt.figure(figsize=(12, 6))
plt.plot(time_series, label="Zaman Serisi")
plt.plot(smoothed[:, 0], label="Trend (Lowess Düzleştirmesi)", linestyle="--")
plt.xlabel("Zaman")
plt.ylabel("Değer")
plt.legend()
plt.grid(True)
plt.show()
```

---
### Durağanlık (Stationary)
Durağanlık, bir zaman serisinin istatistiksel özelliklerinin zaman içinde sabit olduğu veya dalgalanmadığı bir durumu ifade eder. Durağan bir zaman serisi, ortalama, varyans ve otokorelasyon gibi özellikler açısından zaman içinde tutarlıdır. 

**İstatistiksel Testler**
- **Augmented Dickey-Fuller (ADF) Testi:** Bir test, bir zaman serisinin birim kök (unit root) varlığını veya yokluğunu belirlemeye yardımcı olur. Birim kök, zaman serisinin durağanlık özelliği olmadığını ifade eder. ADF testi, null hipotezi H0 ve alternatif hipotezi H1;
**H0** = Zaman serisi birim kök içerir ve durağan değildir.
**H1** = Zaman serisi birim kök içermez ve durağandır.

```python
import pandas as pd
from statsmodels.tsa.stattools import adfuller

# Örnek bir zaman serisi verisi oluşturun
data = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Pandas Serisi oluşturun
ts = pd.Series(data)

# ADF testini uygulayın
result = adfuller(ts)

# ADF test sonuçlarını yazdırın
print('ADF İstatistiği:', result[0])
print('p-değeri:', result[1])
print('Kritik değerler:', result[4])

# Sonuçları yorumlayın
if result[1] <= 0.05:
    print('Zaman serisi durağan.')
else:
    print('Zaman serisi durağan değil.')
```

- **Kwiatkowski-Philips-Schmidt-Shin (KPSS Testi):** 
**H0**: Zaman serisi, düzgün (trend-stationary) durağanlık gösterir.
**H1:** Zaman serisi, düzgün durağanlık göstermez (durağanlık göstermeyen birim kök içerir.).

KPSS testi, genellikle iki farklı sürümde uygulanır: düzgün durağanlık testi (Level Stationary Test) ve trend durağanlık testi (Trend Stationary Test). 

Düzgün Durağanlık Testi (Level Stationary Test):
**H0:** Zaman serisi düzgün durağanlık gösterir.
**H1:** Zaman serisi düzgün durağanlık göstermez.

Trend Durağanlık Testi (Trend Stationary Test):
**H0:** Zaman serisi eğimli durağanlık gösterir.
**H1:** Zaman serisi eğimli durağanlık göstermez.

```python
from statsmodels.tsa.stattools import kpss

# Örnek bir zaman serisi verisi oluşturun
data = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Pandas Serisi oluşturun
ts = pd.Series(data)

# Düzgün durağanlık testini uygulayın
kpss_stat_level, p_value_level, lags_level, critical_values_level = kpss(ts, regression='c')

# Trend durağanlık testini uygulayın
kpss_stat_trend, p_value_trend, lags_trend, critical_values_trend = kpss(ts, regression='ct')

# Düzgün durağanlık test sonuçlarını yazdırın
print('Düzgün Durağanlık Test İstatistiği:', kpss_stat_level)
print('Düzgün Durağanlık Test p-değeri:', p_value_level)

# Trend durağanlık test sonuçlarını yazdırın
print('Trend Durağanlık Test İstatistiği:', kpss_stat_trend)
print('Trend Durağanlık Test p-değeri:', p_value_trend)

# Sonuçları yorumlayın
if p_value_level <= 0.05:
    print('Zaman serisi düzgün durağan değil.')
else:
    print('Zaman serisi düzgün durağan.')

if p_value_trend <= 0.05:
    print('Zaman serisi trend durağan değil.')
else:
    print('Zaman serisi trend durağan.')
```


- **Philips-Perron Testi:** Zaman serisinin eğilimsiz (trend-stationary) durağanlık özelliğini değerlendirmek için kullanılır.
**H0:** Zaman serisi eğilimsiz durağanlık gösterir.
**H1:** Zaman serisi eğilimsiz durağanlık göstermez.

```python
from statsmodels.tsa.stattools import adfuller

# Örnek bir zaman serisi verisi oluşturun
data = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Pandas Serisi oluşturun
ts = pd.Series(data)

# PP testini uygulayın
result = adfuller(ts, regression='ct')

# PP test sonuçlarını yazdırın
print('PP İstatistiği:', result[0])
print('p-değeri:', result[1])
print('Kritik değerler:', result[4])

# Sonuçları yorumlayın
if result[1] <= 0.05:
    print('Zaman serisi eğilimsiz durağan.')
else:
    print('Zaman serisi eğilimsiz durağan değil.')
```

- **Ljung-Box Testi:** Zaman serisinin otokorelasyonunu (kendi içindeki özbenzerliğini) test etmek için kullanılan bir istatistiksel testtir. Bu test, bir zaman serisinin rastgele gürültü içerip içeermediğini değerlendirmek amacıyla yaygın olarak kullanılır. Otokorelasyon, zaman serisinin kendisi ile belirli gecikmeler arasında pozitif veya negatif bir ilişki gösterip göstermediğini ölçer.
**H0:** Zaman serisinin otokorelasyonu yoktur, yani zaman serisi bağımsızdır.
**H1:** Zaman serisinde otokorelasyon vardır.

Ljung-Box testi, belirli bir gecikme (lag) sayısı için bir test istatistiği hesaplar ve bu istatistiği karşılaştırılabilir bir eleştirel değerle karşılaştırır.

```python
from statsmodels.stats.diagnostic import acorr_ljungbox

# Örnek bir zaman serisi verisi oluşturun
data = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Pandas Serisi oluşturun
ts = pd.Series(data)

# Ljung-Box testini uygulayın
lags = 5  # Test edilecek gecikme sayısı
lb_stat, p_value = acorr_ljungbox(ts, lags=lags)

# Ljung-Box test sonuçlarını yazdırın
print('Ljung-Box İstatistiği:', lb_stat)
print('p-değeri:', p_value)

# Sonuçları yorumlayın
if any(p_value <= 0.05):
    print('Zaman serisinde otokorelasyon vardır.')
else:
    print('Zaman serisinde otokorelasyon yoktur.')
```

---
### Mevsimsel (Seasonal) Değişkenler
Mevsimsel değişkenler, belirli bir dönemde, düzenli aralıklarla tekrar eden belirli bir deseni ifade eder. Mevsimsel değişkenler, zaman serisinin mevsimsel etkilerini veya desenlerini yakalamak için kullanılır. 

**Aralık Tablosu (Seasonal Decomposition of Time Series - STL):** Bu yöntem, zaman serisini trend, mevsimsel ve rastgele bileşenlere ayırmak için kullanılır. 

```python
from statsmodels.tsa.seasonal import seasonal_decompose

# Zaman serisinin mevsimsel bileşenlerini çıkartın
result = seasonal_decompose(time_series, model='additive')

# Mevsimsel bileşenleri görselleştirin
result.seasonal.plot()
```

**ACF (Autocorrelation Function) ve PACF (Partial Autocorrelation Function):** 

```python
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf

# ACF grafiğini çizdirin
plot_acf(time_series, lags=50)

# PACF grafiğini çizdirin
plot_pacf(time_series, lags=50)
```

**Differencing (Fark Alma):** Zaman serisinde mevsimsel değişkenler varsa, veriyi fark alma (differencing) yöntemi kullanarak mevsimsel desenlerden arındırabilirsiniz. İlk fark, bir mevsimsel periyot boyunca (örneğin, bir yıl) yapılan farkı ifade eder. İkinci fark, ilk farkı fark alarak mevsimsel etkileri daha da azaltır.

```python
# Birinci fark
first_difference = time_series - time_series.shift(1)

# İkinci fark
second_difference = first_difference - first_difference.shift(1)
```

**Exponential Smoothing (Üstel Düzleştirme):** Üstel düzleştirme yöntemleri (örneğin, Holt-Winters) mevsimsel değişkenleri modellemek için kullanılabilir. Bu yöntemler, verinin mevsimsel bileşenlerini ve mevsimsel desenlerini tahmin etmeye yardımcı olur.

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Holt-Winters üstel düzleştirme modelini kullanarak mevsimsel değişkenleri tahmin edin
model = ExponentialSmoothing(time_series, seasonal='add', seasonal_periods=12)
result = model.fit()

# Mevsimsel tahminleri alın
seasonal_forecast = result.forecast(steps)
```

**Fourier Dönüşümleri:** Fourier dönüşümleri, mevsimsel desenleri modellendirmek için kullanılabilir. Bu yöntem, karmaşık mevsimsel desenleri yakalamak için sinüs ve kosinüs fonksiyonlarını kullanır.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.fftpack import fft

# Örnek bir mevsimsel zaman serisi oluşturun
t = np.linspace(0, 10, 1000) # Zaman aralığı: 0-10 frequency = 0.2 # Mekanizmanın frekansı amplitude = 5 # Amplitüd seasonal_component = amplitude * np.sin(2 * np.pi * frequency * t) # Mevsimsel bileşen # Zaman serisini oluşturun time_series = np.random.randn(1000) + seasonal_component

# Zaman serisinin Fourier dönüşümünü alın
fourier_transform = fft(time_series)

# Fourier dönüşümünün büyüklüğünü alın
magnitude = np.abs(fourier_transform)

# Mevsimsel frekansı bulun
seasonal_frequency = np.argmax(magnitude[1:]) / t[-1]  # İlk eleman hariç en büyük magnitude'ın indeksi

print(f"Mevsimsel frekans: {seasonal_frequency:.2f} periyot biriminde")

# Mevsimsel bileşeni ayırın
seasonal_component = amplitude * np.sin(2 * np.pi * seasonal_frequency * t)

# Mevsimsel bileşen dışındaki zaman serisini elde edin
non_seasonal_component = time_series - seasonal_component

# Mevsimsel bileşen ve geriye kalan zaman serisini görselleştirin
plt.figure(figsize=(12, 6))
plt.plot(t, time_series, label="Mevsimsel Zaman Serisi")
plt.plot(t, seasonal_component, label="Mevsimsel Bileşen", linestyle="--")
plt.plot(t, non_seasonal_component, label="Mevsimsel Dışı Bileşen", linestyle="--")
plt.xlabel("Zaman")
plt.ylabel("Değer")
plt.legend()
plt.grid(True)
plt.show()
```

---
### Rastgele Gürültü (Noise)
Rastgele gürültü, zaman serisindeki tahmin edilemeyen, rastgele veya stokastik dalgalanmalardır. Genellikle, trend ve mevsimsel desenlerin dışında kalan değişkenliklerin neden olduğu dalgalanmalar olarak düşünülür. Rastgele gürültü, zaman serisindeki diğer bileşenlerin modelleme ve tahmininde dikkate alınmaz.

