# Logaritmic Transformation
Bir değişkenin değerlerini logaritmik bir ölçekte ifade etmeyi ifade eder. Veri dağılımını düzeltmek, değişkenin dağılımını normalleştirmek veya bir değişkenin etkisini dengelemek için kullanılır. Logaritmik dönüşümün kullanılması, özellikle bir değişkenin dağılımı çarpık veya normal dağılıma yakın değilse, normal dağılıma daha yakın bir dağılım elde etmek için tercih edilir. Verilerin ölçeğini küçültür ve daha yönetilebilir hale getirir. Dağılımı normalleştirir ve asimetriyi (çarpıklığı) azaltır. Sıfır değerlerini işleyemez. Verilerin orijinal dağılımı değiştirir. Pozitif değerli verilerin analizini kolaylaştırır.

```python
data[['column_name']] = np.log(data[['column_name']])

# scikit
transformer = FunctionTransformer(np.log, validate=True)

# feature_engine
lt = LogTransformer(variables=['column_name'])
lt.fit(df)
```

# Reciprocal Transformation
Bir değişkenin tersini alarak yeni bir değişken oluşturma işlemidir. Veri setindeki çarpık dağılımları düzeltebilmek veya değişkenler arasındaki ilişkileri değiştirebilmek amacıyla kullanılır. Verilerin ölçeğini küçülterek daha yönetilebilir hale getirir. Dağılımı düzleştirerek asimetriyi azaltır. Sıfır değerlerini işleyemez.

```python
df[['column_name']] = np.reciprocal(df[['column_name']])

# scikit
transformer = FunctionTransformer(np.reciprocal, validate=True)

# feature_engine
rt = ReciprocalTransformer(variables = ['column_name'])
rt.fit(df)
```

# Power Transformation

```python
df[['column_name']] = np.power(df[['column_name']], 0.3)

# scikit
transformer = FunctionTransformer(lambda x: np.power(x, 0.3), validate=True)

# feature_engine
pt = PowerTransformer(variables = ['column_name'], exp=0.3)
pt.fit(df)
```

# Square / Cube Root Transformation

```python
df[['column_name']] = np.sqrt(df[['column_name']])
df[['column_name']] = np.cbrt(df[['column_name']])

# scikit
transformer = FunctionTransformer(np.sqrt, validate=True)
transformer = FunctionTransformer(np.cbrt, validate=True)

# feature_engine
pt = PowerTransformer(variables = ['column_name'], exp=1/2)
pt.fit(df)

pt = PowerTransformer(variables = ['column_name'], exp=1/3)
pt.fit(df)
```

# Box-Cox Transformation
Değişkenlerin dönüşümünde kullanılan parametrik bir yöntemdir. Verinin normal dağılıma daha yakın hale getirilmesini amaçlar. Lambda parametresinin optimal değeri, maksimum olabilirlik tahmini veya aykırı bilgi ölçütlerine göre belirlenir. Dağılımın normalleştirerek asimetriyi azaltır. 
- y^(λ) = (x^(λ) - 1) / λ
- Lambda = 0: Logaritmik dönüşüm.
- Lambda = 0.5: Karekök dönüşüm.
- Lambda = 1: Herhangi bir dönüşüm yok.
- Lambda < 0: Terine güç dönüşümü.

```python
# scikit
transformer = PowerTransformer(method='box-cox', standardize=False)

# scipy
df['column_name'], lambda_ = stats.boxcox(df['column_name'])

# feature_engine
bct = BoxCoxTransformer(variables = ['column_name'])
bct.fit(data)
```

# Yeo-Johnson Transformation
Pozitif veya negatif değerler içeren verilerin ölçeğini küçültmek ve dağılımını normalleştirmek için kullanılan bir matematiksel işlemdir. Bu dönüşüm, Box-Cox dönüşümüne benzerdir, ancak negatif değerleri de işlemek için modifiye edilmiştir.

- x >= 0 ise y^(λ) = (x^(λ) - 1) / λ
- x < 0 ise y^(λ) = -((abs(x))^λ + 2λ - 1) / λ

```python
# scikit
transformer = PowerTransformer(method='yeo-johnson', standardize=False)

# scipy
df['column_name'], lambda_ = stats.yeojohnson(df['column_name'])

# feature_engine
yjt = YeoJohnsonTransformer(variables = ['column_name'])
```

# Quantile Transformation
Verinin dağılımını dönüştürerek normal dağılıma yakın bir dağılım elde etmeyi veya belirli bir olasılık dağılımına uygun hale getirmeyi hedefler. Verilerin dağılımını istenen bir dağılıma dönüştürerek analiz ve modellemeyi kolaylaştırır. Asimetri ve uzun kuyruk gibi sorunları gidererek outlier'ların etkisini azaltır.

```python
# scikit
quantile_transformer = preprocessing.QuantileTransformer(output_distribution='normal', random_state=0)
X_trans = quantile_transformer.fit_transform(X)
quantile_transformer.quantiles_
```

# Binarize
Bir veri setindeki sayısal değerleri belirli bir eşik değeriyle karşılaştırarak iki farklı kategoriye ayırmak veya dönüştürmek anlamına gelir. Bu işlem, sayısal verileri iki kategoriye bölmek için kullanılır: belirlenen eşik değerinin altında olan değerler bir kategoriye, eşik değerinin üstünde olan değerler ise diğer kategoriye atanır.

```python
from sklearn.preprocessing import Binarizer
trf = ColumnTransformer([
    ('bin',Binarizer(copy=False),['family'])
],remainder='passthrough')
```

# Spline Transformer
Verileri, her biri farklı bir eğri ile temsil edilen bir dizi parçaya böler. Veriler, spline'ların uç noktalarını belirlemek için kullanılır. Bu, veri setinin minimum ve maksimum değerlerini bulmak veya eşit aralıklarla bölünmesini sağlayarak yapılabilir. Spline'lar, uç noktalara ve diğer kısıtlamalara göre oluşturulur. Bu, lineer, polinom veya diğer eğriler olabilir. Her veri noktası, en yakın spline'a atanır. Dönüştürülmüş veri seti, her veri noktasının atanmış spline'ın değeridir.

```python
X = np.arange(10).reshape(10, 1)
spline = preprocessing.SplineTransformer(degree=2, n_knots=5)
spline.fit_transform(X)
```