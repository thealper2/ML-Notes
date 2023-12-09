# One Hot Encoding
Kategorik verileri sayısal verilere dönüştürmek için kullanılan bir kodlama tekniğidir. Her bir kategorik değer, ayrı bir sütun olarak temsil edilir ve bu sütunlardaki değerler 1 veya 0 olarak kodlanır. Genellikle kategorik değişkenlerin sınırlı sayıda ve sıralı olmayan durumlarda tercih edilir. Çok sayıda benzersiz değer içeren veya yüksek kardinaliteye (yüksek sayıda farklı değer) içeren kategorik değişkenlerde uygulanırsa ortaya çıkacak olan çok fazla sütun veri setinin boyutunu artırabilir ve modelin karmaşıklığını artırabilir.

```python
pd.get_dummies(X_train[cat_cols], drop_first=True)

# scikit
encoder = OneHotEncoder(categories='auto', drop='first', sparse=False)
encoder.fit(X_train[cat_cols])

# feature_engine
enc = OneHotCategoricalEncoder(top_categories=None, drop_last=True)
ohe_enc.fit(X_train)
```

# Ordinal Encoding
Kategorik değerleri sıralı veya derecelendirilebilir olarak kabul eder ve bu sıralamayı temsil etmek üzere sayısal değerlerle kodlar. Veri setinin boyutunu artırmaz. Kategorik değişkenlerin sırasını korur. Kategorik değişkenler arasındaki eşit aralıklar olduğu varsayımına dayanır fakat bu her zaman doğru olmayabilir.

```python
ordinal_mapping = {k: i for i, k in enumerate(X_train['column_name'].unique(), 0)}
X_train['column_name'] = X_train['column_name'].map(ordinal_mapping)

# scikit
ord_encoder = OrdinalEncoder()
ord_encoder.fit(X_train[cat_cols])

# feature_engine
ord_encoder = OrdinalCategoricalEncoder(encoding_method='arbitrary', variables=cat_cols)
ord_encoder.fit(X_train)
```

# Count Encoding
Her bir kategorik değer, o değerim verinde kaç kez tekrarlandığına bağlı olarak bir sayı ile kodlanır. Kategorik değişkenlerin sıklığına dayalı bilgiyi korur ve sıklıkla tekrarlanan değerlere daha yüksek sayısal değerler atar. Ancak veri setindeki bir değer çok fazla tekrarlanmıyorsa veya nadirse, bu yöntem o değeri temsil eden sayıyı düşük bir sayıda atayabilir. Bu durumda, nadir sınıflar için modelin performansını düşürebilir.

```python
f_map = (X_train['column_name'].value_counts() / len(X_train) ).to_dict()
X_train['column_name'] = X_train['column_name'].map(f_map)

# feature_engine
count_encoder = CountFrequencyCategoricalEncoder(encoding_method='count', variables=None)
count_encoder.fit(X_train)
```

# Label Encoding
Hedef kategorik değişkenin sayısal değerlere dönüştürülmesidir.

```python
le = LabelEncoder()
le.fit(X_train)
```

# Weights of Evidence Encoding (WOE)
Her bir kategorik değeri, o kategoriye ait olasılığı hedef değişkenin iki farklı durumu arasındaki olasılık oranına dönüştürür. Bu oran, hedef değişkenin o kategoriye ait olduğu durumun olasılığını o kategorinin olmadığı durumun olasılığına böler. Hedef değişkenin binary olması gerekir. Kategoriler arasında çok az sayıda veri noktası olduğunda iyi sonuç vermez.

```python
# feature_engine
woe_encoder = WoERatioCategoricalEncoder(encoding_method='woe', variables=['column_name'])
woe_encoder.fit(X_train, y_train)
```