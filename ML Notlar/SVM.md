Temel amacı, verileri bir hiperdüzlem üzerinde sınıflandırmak veya regresyon analizi yapmaktır.

# Çalışma Prensibi
SVM, bu hiperdüzlemi oluştururken, sınıflar arasındaki en büyük marjı (boşluk) bulmaya çalışır. Marj, hiperdüzleme en yakın veri noktalarından uzaklık olarak tanımlanır ve bu noktalara "destek vektörleri" denir. Hiperdüzlem, bu destek vektörleri arasında yer alır ve iki sınıf arasındaki boşluğu maksimize eder. SVM'nin çalışma prensibi matematiksel olarak iki sınıf için aşağıdaki şekilde ifade edilir:

Veri noktası: (x,y) 
Hiperdüzlem: w . x + b = 0

- w: Hiperdüzlemi belirleyen normal vektör (ağırlıklar).
- x: Veri noktasının özellik vektörü.
- b: Bias terimi.

Sınıf tahminlemesi yapmak için, veri noktasını hiperdüzlem formülüne yerleştiririz:

- Eğer w⋅x+b>0 ise, veri noktası sınıf +1'e aittir.
- Eğer w⋅x+b<0 ise, veri noktası sınıf -1'e aittir.

# Avantajlar
- Etkili performans
- Hem sınıflandırma hem regresyon problemlerinde kullanılır.
# Dezavantajlar
- Büyük veri kümelerinde eğitim süresi uzun olabilir.
- Çoklu sınıf, çoklu özellik sorunlarına karşı performansı düşebilir.

# Hiperparametreler

| Parameters | Types | Default | Description |
| - | - | - | - |
| C | float | 1 | C, SVM'nin bir hiperdüzlemi oluştururken ne kadar hata kabul edeceğinizi kontrol eden bir hiperparametredir. Küçük bir C değeri, daha geniş bir marj ve daha fazla eğim sağlar, ancak bazı veri noktalarının hatalı sınıflandırılmasına neden olabilir. Büyük bir C değeri, daha dar bir marj ve daha az hata kabul eder. C'nin değeri modelin aşırı uyuma (overfitting) karşı hassasiyetini etkiler. C değeri ne kadar büyükse, aşırı uyuma o kadar eğilimli olabilir. |
| kernel | "linear", "poly", "rbf", "sigmoid" | "rbf" | Çekirdek. |
| Gamma | "scale", "auto" | "scale" | Gamma, bir veri noktasının diğer veri noktalarına ne kadar etki etmesini kontrol eder. Küçük bir gamma değeri, uzak noktaların etkisinin büyük olmasını sağlar. Büyük bir gamma değeri ise yakın noktaların etkisinin büyük olmasını sağlar. |
| degree | int | 3 | Polinum çekirdek derecesi. Sadece kernel "poly" ise kullanılır. |
