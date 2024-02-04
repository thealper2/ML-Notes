Yapay sinir ağları (ANN) ailesine ait bir modeldir. MLP, en az bir gizli katman içeren bir yapay sinir ağıdır ve en az bir giriş ve bir çıkış katmanı bulunur. Her katmandaki düğümler bir önceki katmandaki tüm düğümlerle bağlanır ve ağında içindeki bilgi akışını sağlar.

**Çalışma Adımları**
1. MLP modeli oluşturulur.
2. Başlangıç ağırlıkları rastgele atanır.
3. Giriş verisi her bir gizli katmandaki düğümler arasından çıkış katmanına doğru ilerler (forward propagation). Bu işlem, her bir katmandaki düğümlerde aktivasyon fonksiyonunun uygulanmasıyla gerçekleşir.
4. İleri yayılma işleminden sonra tahmin edilen çıktılar ile gerçek değerler arasındaki hata hesaplanır.
5. Hata hesaplamasından sonra geri yayılma (backward propagation) işlemi gerçekleştirilir. Geri yayılma, ağın içindeki hata miktarını geriye doğru hesaplar ve her bir ağırlığın bu hataya katkısını belirler.
6. Gradyan iniş (gardient descent) ile geri yayılma işleminden elde edilen hata miktarına dayanarak, ağdaki ağırlıklar güncellenir.
7. Belirli bir iterasyona kadar bu işlem tekrarlanır.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| hidden_layer_sizes | array-like | (100,) | Gizli katman sayısı. |
| activation | "identity", "logistic", "tanh", "relu" | "relu" | Aktivasyon fonksiyonu. |
| solver | "lbfgs", "sgd", "adam" | "adam" | Ağırlıkları güncellemek için kullanılan optimizasyon algoritması. |
| learning_rate | "constant", "invscaling", "adaptive" | "constant" | Öğrenme oranı. |
| alpha | float | 0.0001 | Ağırlık düzenlemesi için kullanılır. |
| batch_size | int | "auto" | Ağırlık güncellemesi sırasında kullanılan mini-batch sayısını belirler. |
| max_iter | int | 200 | İterasyon sayısı. |