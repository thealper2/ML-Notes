İsmini matematikteki, lojistik (sigmoid) fonksiyondan alır. Bir bağımlı değişkenin (genellikle kategorik) olasılığını tahmin etmek veya sınıflandırmak için kullanılan bir istatistiksel modeldir. Temel amacı, bir girdi örneğini belirli bir sınıfa ait olma olasılığını tahmin etmektir. Lineer regresyon ile arasındaki fark, Lineer regreson optimum çizgiyi çizmek için "**En Küçük Kareler Yöntemi (Least Squares)**", lojistik regreson "**Maksimum Olabilirlik (Maksimum Likelihood)**" kullanır. **Sigmoid Fonksiyonu**, verileri 0 ile 1 arasında sıkıştırmak için kullanılan fonksiyondur. 

# Çalışma Adımları

Sigmoid Fonksiyon:
P(Y=1) = 1 / (1 + e^(-z))

Bu denklemde:

- P(Y=1), bağımlı değişkenin 1 (başarı, pozitif sınıf) olma olasılığını temsil eder.
- e, Euler sayısı (yaklaşık olarak 2.71828) olarak bilinir.
- z, lojit (log-odds) değeridir ve şu şekilde hesaplanır: z = b0 + b1_x1 + b2_x2 + ... + bn*xn
    - b0, kesme terimidir.
    - b1, b2, ..., bn, bağımsız değişkenlerin katsayılarıdır.
    - x1, x2, ..., xn, bağımsız değişkenlerin değerleridir.

1. **Örnekleri Sınıflandırma:** Her bir örneği sınıflandırmak için bağımsız değişkenlerin ağırlıklı toplamını ve lojistik fonksiyonu kullanır. Bu sonuç, 0 ile 1 arasında bir olasılık değeridir.
2. **Eşik Değer Karşılaştırması:** Elde edilen olasılık değeri, belirli bir eşik değer (0.5) üezrindeyse örnek "1" sınıfına atanır, değilse "0" sınıfına atanır.
3. **Model Eğitimi:** Model, eğitim verileri üzerinde eğitilir.
# Avantajları
- Basit ve hızlıdır.
- Kolay yorumlanabilir.
- Olasılık tahminleri sunar.

# Dezavantajları
- Sadece doğrusal ilişkileri modelleyebilir.
- Overfitting riski vardır.
- Sadece sınıflandırma problemlerinde kullanılır.

# Hiperparametreler

| Parameters | Types | Default | Description |
| - | - | - | - |
| penalty | "l1", "l2", "elasticnet" | | Düzenleme fonksiyonu | 
| C | float | 1 | Düzenleme kuvvetini kontrol eder. Çok büyük olması overfit'e küçük olması underfit'e yol açabilir. |
| solver | "lbfgs" <br/> "liblinear" <br/> "newton-cg" <br/> "newton-cholesky" <br/> "sag" <br/> "saga" | "lbfgs" | Çözücü. Küçük veri seti için "liblinear". Büyük veri seti için "saga" ve "sag". Çok sınıflılar için kalanlar. |
| max_iter | int | 100 | Maksimum iterasyon sayısı. Büyük veri setleri için arttırmak gerekir. |
| multi_class | "auto", "ovr", "multinomial" | "auto" | |
| class_weight | dict / "balanced" | None | Sınıf ağırlığı. |
| tol | float | 1e-4 | Durdurma kriterleri için tolerans. |
| warm_start | bool | False | True olarak ayarlandığında, önceki fit çağrısının çözümünü başlatma olarak yeniden kullanır, aksi takdirde önceki çözümü siler. |

