KNN, veri noktalarının komşularına dayalı olarak sınıflandırılmasını veya tahmin edilmesini sağlayan bir algoritmadır. Temel fikir, bir veri noktasının sınıfını veya değerini belirlemek için, bu noktanın en yakın komşularının sınıfını veya değerlerini kullanmaktır. 

# Çalışma Prensibi

Tahmin yapılacak yeni veri noktası ile eğitim verilerindeki diğer noktalar arasındaki uzaklığı hesaplanır. Genellikle kullanılan uzaklık ölçüleri;
- **Euclidean (Öklidyen):** İki nokta arasındaki doğru mesafeyi ölçer.
- **Manhattan:** İki nokta arasındaki yolların toplam uzunluğunu ölçer.
- **Chebyshev:** Vektörler arasındaki mutlak farkın maksimumunu alır.
Daha sonra en yakın "k" komşusu seçilir. k, bir hiperparametredir ve kullanıcı tarafından belirlenmelidir.

- **Sınıflandırma Problemi:** Eğer KNN sınıflandırma amaçlı kullanılıyorsa, en yakın k komşunun sınıfları incelenir ve yeni veri noktasının sınıfı, bu k komşunun sınıfının çoğunluğu (modu) olarak tahmin edilir. Örneğin, eğer 3 en yakın komşu sınıfları "A", "A", ve "B" ise, yeni veri noktasının tahmini sınıfı "A" olur.
- **Regresyon Problemi:** Eğer KNN regresyon amaçlı kullanılıyorsa, en yakın k komşunun hedef değerleri kullanılarak yeni veri noktasının hedef değeri tahmin edilir. Genellikle bu değerlerin ortalaması veya ağırlıklı ortalaması kullanılır.

# Avantajlar
- Hızlı eğitim süresi
- Hem sınıflandırma hem regresyon problemlerinde kullanılabilir.

# Dezavantajlar
- Yüksek boyutlu verilerde sorun yaşayabilir çünkü uzaklık hesaplamaları artar.
- "k" sayısı yanlış seçilirse sonuçlar değişebilir.
- Eşit uzaklığa sahip birden fazla komşu olması durumunda sınıflandırma sonuçları belirsiz olabilir.

# Hiperparametreler

| Parameters | Types | Default | Description |
| - | - | - | - |
| n_neighbors | | | Komşu sayısını belirtir. Çok büyük k overfit'e çok küçük k underfit'e sebep olabilir. |
| weights | | | Komşuların etkisinin hesaplanma yöntemini belirtir. "uniform", tüm komşular eşit ağırlığa sahiptir. "distance" komşuların uzaklıklarına göre ağırlık verilir. |
| p | | | Uzaklık ölçümüü için kullanılacak metriği seçer. P=1 Manhattan uzaklık, P=2 Euclidean uzaklık olarak kullanılır. |
