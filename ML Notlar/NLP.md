- Tokenization
- Stemming
- Lemmatizing
- Stopwords
- Part-of-speech (POS) Tagging
- Named-entity-recognition (NER)

# Tokenization
Metinlerin kelimelerine, sembollerine veya cümlelerine ayrılmasını sağlar. Bu işlem, metin verilerini daha işlenebilir hale getirir ve makine öğrenimi veya dil işleme modelleri için daha uygun bir formata dönüştürür.

```python
from nltk.tokenize import word_tokenize

cumle = 'Merhaba dunya! NLP harika bir alandır.'
kelimeler = word_tokenize(cumle)
print(kelimeler)
```

# Stemming
Kelime köklerini bulmayı amaçlar. Kelime kökleri, bir kelimenin çekim ekleri veya ek bilgileri atılarak elde edilen temel kelime formudur. Bu işlem, bir kelimenin farklı varyasyonlarını aynı köke indirgeyerek metinlerdeki veri tutarsızlığını azaltmaya yardımcı olur.

```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()

words = ['running', 'ran', 'run']

for word in words:
	stemmed = stemmer.stem(word)
	print(f'{word} -> {stemmed}')
```

# Lemmatization
Bir kelimeyi gerçek anlamıyla karşılayan ve dilbilgisi kurallarına uygun olan temel veya kök formuna dönüştürmeyi hedefler. 

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = ['running', 'ran', 'run']

for word in words:
	stemmed = lemmatizer.lemmatize(word)
	print(f'{word} -> {stemmed}')
```

# Stopwords
Pek anlam taşımayan veya çok sık kullanılan keliemelerdir. Bu kelimeler genellikle dilin yapı taşları olsa da, genel anlam taşımadıkları veya metnin anlamını çok fazla etkilemedikleri için çıkarılabilirler.

```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

cumle = "Bu örnek cümlede, analiz için gereksiz kelimeler bulunmaktadır."
kelimeler = word_tokenize(cumle)
stop_words = set(stopwords.words('turkish'))
temiz_kelimeler = [kelime for kelime in kelimeler if kelime.lower() not in stop_words]
print(temiz_kelimeler)
```
# POS (Part-of-Speech) Tagging
Bir cümledeki her kelimenin dilbilgisel kategorisini (isim, sıfat, fiil, zarf) belirleme işlemidir.

```python
import nltk
from nltk.tokenize import word_tokenize

cumle = "the cat jumped out of the tree."
kelimeler = word_tokenize(cumle)
pos_tags = nltk.pos_tag(kelimeler)
print(pos_tags)
```

# Named Entity Recognition
Metindeki önemli bilgi parçalarını (ad, yer, tarih) tanımlamak için kullanılır.

```python
import nltk

cumle = "Bill Gates founded Microsoft and lives in Seattle."
tokens = nltk.word_tokenize(cumle)
pos_tags = nltk.pos_tag(tokens)
ner_tags = nltk.ne_chunk(pos_tags)
print(ner_tags)
```

