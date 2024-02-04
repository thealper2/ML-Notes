Doğrusal olmayan regresyon problemlerini çözmek için kullanılır. Temelde, Ridge fonksiyonu ile aynıdır. Sadece düzenleme (regularization) işleminden önce doğrusal olmayan ilişkileri modellemek için özellik vektörlerini doğrusal olmayan bir şekilde dönüştürür. Bu dönüşüm işlemi için çekirdek fonksiyonlarını kullanır.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| alpha | float | 1 | Ridge regresyonundaki düzenleme parametresi. |
| kernel | str | "linear" | Kullanılacak olan çekirdek fonksiyonu. |
| gamma | float | None | RBF ve Polinom çekirdeklerinde kullanılan çekirdek parametresidir. Çekirdek fonksiyonunun esnekliğini belirler. |
| degree | float | 3 | Polinom çekirdeklerinde kullanılır. Polinomun derecesini belirler. |
