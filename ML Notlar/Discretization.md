# Equal Width Discretization
Veri değerlerini belirli genişlik alanlarına bölen bir veri ön işleme tekniğidir. Sürekli bir veri kümesini belirli bir sayıda aralığa (bin) bölerken değerlerin minimum ve maksimum değerleri kullanarak her aralığın genişliğini sabit tutar. Veride çok sayıda farklı değer varsa, bilgi kaybına neden olabilir.

```python
# scikit
ewd = KBinsDiscretizer(n_bins=10, encode='ordinal', strategy='uniform')
ewd.fit(X_train[['column_name']])

# feature_engine
ewd = EqualWidthDiscretiser(bins=10, variables = ['column_name'])
ewd.fit(X_train)
```

# Equal Frequency Discretization
Veri değerlerini belirli bir frekansta eşit sayıda öğe içeren gruplara bölen bir veri ön işleme tekniğidir. Veri değerleri sıralanır ve belirlenen grup sayısına göre her bir grup eşit sayıda veri öğesini içerecek şekilde oluşturulur.

```python
pd.cut(x = X_train['column_name'], bins=intervals)
# scikit
efd = KBinsDiscretizer(n_bins=10, encode='ordinal', strategy='quantile')
efd.fit(X_train[['column_name']])

# feature_engine
efd = EqualFrequencyDiscretiser(q=10, variables = ['column_name'])
efd.fit(X_train)
```

# Arbitrary Interval Discretization
Kullanıcı tarafından belirlenen özel aralıklar veya gruplar ile veri değerlerini gruplara ayırır. Yanlış sınır değerleri sonuçları etkileyebilir. 

# Kmeans Discretization
K-Means kullanarak veri kümesini gruplara ayırır. K-Means veri noktalarını belirli bir sayıda küme merkezi etrafında kümelemek için kullanılır. 

```python
# scikit
kbins = KBinsDiscretizer(n_bins=10, encode='ordinal', strategy='kmeans')
kbins.fit(X_train[['column_name']])
```

