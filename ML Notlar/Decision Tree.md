Karar ağacı, bir veri setini, bir dizi karar uygulayarak daha küçük kümelere bölmek için kullanılan bir yapıdır. Karar ağacında ilk bölünmenin başladığı yere **kök**, dalların uzaması ile gelişen kısımlara **düğüm**, alt uçlara ise **yaprak** denir. Karar ağaçları, en iyi bölünmeyi seçmek için farklı kriterler kullanır. Daha uzun ağaçlar yerine daha kısa ağaçlar tercih edilir. En yaygın olarak kullanılan kriterler.
-  **Bilgi Kazancı (Information Gain):** Bir düğümün bölünmesinin ne kadar bilgi kazandıracağını ölçer. Bilgi kazancı, her alt düğümün belirli bir özellikle ne kadar homojen olduğunu gösteren bir metriktir. Bilgi kazancı, bir özellikle yapılan bölünmenin önceki duruma göre ne kadar daha az belirsizlik (bilgi eksikliği) getirdiğini ölçer. Bu, ağacın daha homojen alt gruplara bölünmesine ve iyi tahminler yapmasına yardımcı olur. Sırasıyla şu adımlar izlenir:
1. Entropi (Entropy): Bir veri kümesinin ne kadar homojen veya heterojen olduğunu ölçen bir kavramdır. Daha yüksek entropi, daha fazla belirsizlik veya bilgi eksiliği anlamına gelir. Entropi şu formülle hesaplanır: E(S) = -p1 * log2(p1) - p2 * log2(p2) - ... - pk * log2(pk), burada p1, p2, ..., pk, S'deki her sınıfın olasılıklarıdır.
2. Dallanma (Split): Bir özellik seçilir ve veri kümesi bu özelliğe göre alt gruplara bölünür. Her alt grup için entropi hesaplanır ve bu alt grupların ağırlıklı ortalaması (weighted average) alınır.
3. Bilgi Kazancı (Information Gain): Entropinin önceki durum ile yeni durum arasındaki farkını ölçer. Information Gain yüksekse, o özellik daha fazla bilgi kazandırır ve ağacın bölünmesinde daha önemli bir rol oynar. 

Çok sayıda farklı kategorik değer alabilen özelliklerde Information Gain yöntemi etkili olmaz.

- Jini Indeksi (Gini Index): Bir düğümün homojenliğini ölçer. Daha küçük bir jini indeksi, daha homojen bir düğümü temsil eder. Sırasıyla şu adımlar izlenir;
1. Veri Bölünmesi (Split): Bir özellik seçilir ve veri bu özelliğe göre alt gruplara bölünür. Her bir alt grup, belirli bir değeri veya sınıfı temsil eder.
2. Gini Indeksi Hesaplaması: Her alt grup için Gini indeksi hesaplanır. Gini İndeksi şu formülle hesaplanır: Gini(S) = 1 - Σ(p_i^2). Burada, S, bölünmüş alt grupları temsil eder ve p_i, her bir alt grubun içinde bulunan farklı sınıfların yüzdesini ifade eder. p_i^2 terimi, bir alt grup içindeki sınıf i'nin olasılığının karesidir.
3. Ağırlıklı Ortalama Hesaplaması: Gini indeksi hesaplandıktan sonra, her alt grup için hesaplanan Gini indeksleri ağırlıklı olarak ortalaması alınır. Her alt grupun büyüklüğüne göre ağırlıklandırılırlar.
4. Bilgi Kazancı: Gini indeksi hesaplandıktan sonra, information gain hesaplanır.

Düğümler:
1. **Internal Node:** Özelliğin adı
2. **Branch:** Bir üstteki özelliğin değeri
3. **Leaf Node:** Tahmin Sınıfı

**Pruning (Budama):** Karar ağacında tahmine yeterince katkı yapmayan dallarda tahmin edici değişkenlerin modelden çıkarılması işlemidir. Post ve Pre olarak ikiye ayrılır. Prepruning, tahmin edici değişkenleri teker teker ele alarak modelin tahmin gücü için hangisinin etkili olacağı kararlaştırılarak adım adım dallanmaların ilerletilmesidir. Postpruning, tamamlanmış bir karar ağacından modele katkı yapmayan dalların tespit edilip modelden çıkarılmasıdır.

# Çalışma Adımları
1. **Veri Toplama:** Özellikler ve hedef değişken belirlenir.
2. **Ağaç Oluşturma:** Ağacın kök düğümü seçilir ve veriler bu düğümde belirli bir özelliğe göre bölünür. Ardından, her alt düğüm için aynı adım tekrarlanır.
3. **Düğüm Bölünmesi:** Düğümler, en iyi bölünme kriterine göre alt düğümlere bölünür. Bölünme kriterleri genellikle bilgi kazancı, gini indeksi veya ortalama hata gibi metrikler kullanılarak belirlenir.
4. **Ağaç Düzenleme:** Ağaç gereğinden fazla dallanma yapabilir. Bu nedenle gereksiz dallar kaldırılmaldır. (pruning)
5. **Tahmin:** Yeni veriler için tahminler yapılır.

# Avantajları
- Yorumlaması kolaydır.
- Kullanılan ağaçlar görselleştirilebilir (sklearn.tree.plot_tree()).
- Değişken seçimi yapabilir.
- Maaliyeti kullanılan veri boyutu ile logaritmiktir.
# Dezavantajları
- Overfitting sorunu. Budama işlemi ile önlenebilir.
- Heterojen veri üzerinde iyi performans göstermez.
- Yalnızca tek bir özellikle ilişkilendirilen ikinci sıra bağımlılıkları yakalayamaz.


# Hiper Parametreler

| Parameters | Types | Default | Description |
| - | - | - | - |
| criterion | "gini", "entropy", "log_loss" | "gini" | Ağaç oluşturma yöntemidir. |
| max_depth | int | None | Ağacın maksimum derinliğini temsil eder. Değer verilmezse limitsiz olur. Overfitting'i önlemek için küçük bir değer girilmelidir. |
| min_samples_split | int/float | 2 | Bir düğümün bölünmeden önceki sahip olması gereken minimum örnek sayısıdır. |
| min_samples_leaf | int/float | 1 | Bir yaprağın sahip olması gereken minimum örnek sayısıdır. |
| min_weight_fraction_leaf | float | 0 | Ağırlıklı örneklerin, toplam örnekler içerisindeki oranını temsil eder. |
| max_leaf_nodes | int | None | Maksimum yaprak sayısıdır. Overfitting'i engellemek için kullanılır. |
| max_features | int/float, "auto", "sqrt", "log2" | None | En iyi bölünme için aranacak feature sayısıdır. | 
