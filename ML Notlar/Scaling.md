# Standardization
Veri kümesindeki değerleri belirli bir ölçüde dönüştürerek ortalamayı 0 yapma ve standart sapmayı 1 yapma işlemidir. Veri setindeki her özellik veya değişken için,o özellik için ortalama değeri çıkararak ve standart sapmaya bölerek dönüştürür. Böylece her özellik aynı ölçekte ve aynı varyansa sahip olur.
z = (x - x_mean) / std
# Normalization
Veri değerlerini belirli bir aralık veya dağılım içinde ölçeklendirir ve farklı özellikler arasındaki büyüklük farklarını azaltır. Veri dağılımı değişmez yalnızca ölçeklendirir. 


# Mean Normalization
X_normalized = (x - x_mean) / (x_max - x_min)

```python
# scikit
ss = StandardScaler(with_mean=True, with_std=False)
```

# Min Max Normalization
X_scaled = (x - x_min) / (x_max - x_min)

```python
# scikit
scaler = MinMaxScaler()
scaler.fit(X_train)
```

# Maximum Absolute Scaling
X_scaled = (x / x_max)

```python
# scikit
scaler = MaxAbsScaler()
scaler.fit(X_train)
```

# Robust Scaling
X_scaled = (x - x_median) / (x.quantile(0.75) - x.quantile(0.25))

```python
# scikit
scaler = RobustScaler()
scaler.fit(X_train)
```

