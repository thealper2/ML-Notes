# ARLStem
Arapça metinler için kullanılır. Kullanılması için tüm metinlerin unicode olarak kodlanması gerekir.

```python
from nltk.stem.arlstem import ARLSTem
```
# ISRIStemmer
Arapça metinler için kullanılır.

```python
from nltk.stem.isri import ISRIStemmer
```
# LancasterStemmer
İngilizce metinler için kullanılır. 

```python
from nltk.stem.lancaster import LancasterStemmer
```
# PorterStemmer
İngilizce metinler için kullanılır. PorterStemmer, daha basit bir kural tabanlı yaklaşım kullanır. Bu nedenle, daha hızlı ve verimli bir şekilde çalışır. İstisnaları yakalamada başarısız olabilir.

```python
from nltk.stem.porter import PorterStemmer
```
# RSLPStemmer
Portekizce metinler için kullanılır.

```python
from nltk.stem.rslp import RSLPStemmer
```
# RegexpStemmer
Belirli bir regex ile eşleşen kelimelerin köklerini bulmak için kullanılır.

```python
from nltk.stem.regexp import RegexpStemmer
```
# SnowballStemmer
Çeşitli diller için farklı stemmer versiyonları içerir. 

```python
from nltk.stem.snowball import SnowballStemmer
```
# WordNetLemmatizer
WordNetLemmatizer, WordNet adlı bir dil işleme veritabanını kullanarak çalışır. WordNet, sözcüklerin gruplandırıldığı ve anlamsal ilişkilerin bulunduğu bir veritabanıdır. Lemmatizer, kelimenin WordNet'teki eş anlamlı gruplarına bakarak kelimenin kökünü bulur. Anlamsal olarak doğru kökleri bulma konusunda oldukça etkilidir. Sözcüklerin gerçek dildeki anlamını korumaya çalışır. Yavaştır.

```python
from nltk.stem.wordnet import WordNetLemmatizer
```