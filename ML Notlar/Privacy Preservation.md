1. k-anonymity
2. l-diversity
3. t-closeness
4. Differential privacy

---
# k-Anonymity

Latanya Seeney tarafından 1998 yılında önerilmiştir. Temel amaç, bir bireyin kimlik bilgilerinin başka bireylerin kimlik bilgileriyle birleştirildiğinde ayrıştırılamayacak hale getirilmesidir. Veri setindeki her bir kaydın en k-1 diğer kayıtla aynı olacak şekilde gruplandırılmasını sağlar. Bu sayede verinin tanımlanabilirlik riski azalır.

**Kırmak için**
- **Köşe noktaları tanımlama**
- **İstatistiksel saldırılar:** Örneğin grupların ortalama değerlerini kullanarak tahmin etme.
- **Yeniden tanımlama:** Diğer kaynaklardan elde edilen verileri kullanarak anonimliği çözmek.

---
# l-Diversity
Veri setindeki verilerin tek tipleştirilmesini sağlar. Her grup içindeki hassas veri örnekleri farklılık göstererek tanımlanabilirliği azaltır. L-diversity, çeşitliliği arttırmak için gürültü ekleme, yapay veri oluşturma gibi yöntemler kullanır. K-anonymity'de tek bir sütun kullanılarak çeşitlilik yapılırken l-diversity'de birden fazla sütunda çeşitlilik yapılır.

**Kırmak için**
- **Kombinasyon saldırıları**
- **Köşe noktaları belirleme**
- **İstatistiksel saldırılar**

---
# t-Closeness
Veri setindeki her bir grup içindeki kayıtların hassas özellikler bakımından yeterli bir yakınlık kriteri sağlatır. Bu kriter, grup içindeki verilerin dağılımı ile bir referans dağılım arasındaki farkın 't' eşik değerine yakın olmasını gerektirir. Bu sayede verilerin tanımlanabilirliği azalır. 

---
# Differential Privacy
Veri kümesinin herhangi iki benzer veri kümesi arasında, farklı bir sonuç elde etme olasılığını sınırlayarak çalışır. Veri kümesine gürültü eklenir. Modelin doğruluğunu etkileyebilir.

