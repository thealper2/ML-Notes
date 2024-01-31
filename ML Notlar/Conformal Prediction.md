Belirsizlik tahmini yapmak için uyumluluk tahmini prensiplerini kullanan bir yaklaşımdır. Bir modelin tahminlerinin güvenirliliğini değerlendirmek ve belirsizlikleri hesaba katmak için kullanılır. Model eğitim verilerini kullanarak bir uyumluluk bölgesi oluşturur. Bu bölge, modelin eğitim verilerinde yakaladığı örüntüleri gösterir. Sınama verileri için bu uyumluluk bölgesine dayanarak bir tahmin yapılır. Böylece belirli bir güven düzeyinde tahminler yapılır.

**Inductive Conformal Predictors**
- Bir modelin eğitim verilerine dayanarak belirli bir güven düzeyinde uyumluluk tahmini yapar.
- Model, eğitim verilerindeki benzer örneklerin dağılımına dayanarak bir güven aralığı hesaplar.
- Her bir tahmin için güven aralığı belirlenir.

**Aggregated Conformal Predictors**
- Birden fazla modelin çıktılarını bir araya getirerek daha güvenilir tahminler elde etmeyi amaçlar.
- Her bir modelin tahminleri, uyumluluk tahminine göre bir araya getirilir. Böylece toplu bir güven aralığı sağlanır.

**Transductive Conformal Prediction**
- Her bir test örneği için, modelin oluşturduğu uyumluluk bölgesine dayanarak bir tahmin yapılır. Bu tahmin için test örneği yanında diğer eğitim örneklerini de kullanır.

