Bir benchmark olarak veya başlangıç noktası olarak karmaşık modellerle karşılaştırma yapmak için bir referans olarak kullanılır. Girdi özelliklerini göz ardı ederek tahminler yapar.

# Hiperparametreler

| Parametre | Type | Default | Açıklama |
| ---- | ---- | ---- | ---- |
| strategy | "most_frequent" <br/> "prior" <br/> "stratified" <br/> "uniform" <br/> "constant" | "prior" | "most_frequent":  Her zaman en sık görülen sınıf etiketini döndürür. <br/> "uniform" her sınıf için eşit olarak tahminler üretir. <br/> "constant" sabit bit etiket tahmin eder. |
| random_state | int | None | Rastgelelik kontrolü. |
| constant | int | None | Tahmin edilecek sabit değer. Eğer strategy parametresi "constant" ise kullanılır. |
