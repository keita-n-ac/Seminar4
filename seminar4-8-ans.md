### 問題1
```python
import seaborn as sns
iris = sns.load_dataset("iris")
print(iris)
print('Columns', iris.columns)
print('Data Types', iris.dtypes)
print('Shape', iris.shape)
```

### 問題2
```python
import seaborn as sns
iris = sns.load_dataset("iris")
print("sepal_length:")
print(iris["sepal_length"].describe())
print("petal_width:")
print(iris["petal_width"].describe())
```

### 問題3
```python
import seaborn as sns
iris = sns.load_dataset("iris")
print("describe() of species:")
print(iris["species"].describe())
print("unique species:")
print(iris["species"].unique())
```

### 問題4
```python
import seaborn as sns
iris = sns.load_dataset("iris")
data_setosa = iris[iris["species"] == "setosa"]
data_setosa = data_setosa.reset_index(drop=True)
print(data_setosa)
```

### 問題5
```python
import seaborn as sns
iris = sns.load_dataset("iris")
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)
print("data_versicolor (head):")
print(data_versicolor.head())
print("data_virginica (head):")
print(data_virginica.head())
```

### 問題6
```python
import seaborn as sns
iris = sns.load_dataset("iris")
data_long_sepal = iris[iris["sepal_length"] >= 6.0]
print("Number of rows (sepal_length >= 6.0):")
print(len(data_long_sepal))
print("Statistics of sepal_length (sepal_length >= 6.0):")
print(data_long_sepal["sepal_length"].describe())
```

### 問題7
```python
import seaborn as sns
iris = sns.load_dataset("iris")
data_narrow_setosa = iris[(iris["sepal_width"] < 3.0) & (iris["species"] == "setosa")]
print(data_narrow_setosa)
```

### 問題8
```python
import seaborn as sns
import matplotlib.pyplot as plt
iris = sns.load_dataset("iris")
iris['sepal_length'].hist()
plt.xlabel("sepal_length")
plt.show()
```

### 問題9
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

plt.hist(data_setosa['sepal_length'], color='b', alpha=0.5, label='setosa')
plt.hist(data_versicolor['sepal_length'], color='r', alpha=0.5, label='versicolor')
plt.hist(data_virginica['sepal_length'], color='g', alpha=0.5, label='virginica')

plt.xlabel("sepal_length")
plt.legend()
plt.show()
```

### 問題10
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

plt.hist(data_setosa['petal_width'], color='b', alpha=0.5, label='setosa')
plt.hist(data_versicolor['petal_width'], color='r', alpha=0.5, label='versicolor')
plt.hist(data_virginica['petal_width'], color='g', alpha=0.5, label='virginica')

plt.xlabel("petal_width")
plt.legend()
plt.show()

print("setosaはpetal_widthで別の種と分けることができそう")
```

### 問題11
```python
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

df_pw = pd.concat([data_setosa['petal_width'], data_versicolor['petal_width'], data_virginica['petal_width']], axis=1)

df_pw.columns = ['setosa', 'versicolor', 'virginica']

sns.boxplot(data=df_pw, width=0.5)
plt.ylabel("petal_width")
plt.show()
```

### 問題12
```python
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

df_pl = pd.concat([data_setosa['petal_length'], data_versicolor['petal_length'], data_virginica['petal_length']], axis=1)

df_pl.columns = ['setosa', 'versicolor', 'virginica']

sns.boxplot(data=df_pl, width=0.5)
plt.ylabel("petal_length")
plt.show()

print("virginica一番長いpetalを持つ傾向がある")
```

### 問題13
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

df_sw = pd.concat([data_setosa['sepal_width'], data_versicolor['sepal_width'], data_virginica['sepal_width']], axis=1)

df_sw.columns = ['setosa', 'versicolor', 'virginica']
sns.boxplot(data=df_sw, width=0.5)
plt.ylabel("sepal_width")
plt.show()

print("setosaのsepal_widthの中央値:", data_setosa['sepal_width'].median())
```

### 問題14
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

df_sl = pd.concat([data_setosa['sepal_length'], data_versicolor['sepal_length'], data_virginica['sepal_length']], axis=1)

df_sl.columns = ['setosa', 'versicolor', 'virginica']

sns.boxplot(data=df_sl, width=0.5)
plt.ylabel("sepal_length")
plt.show()

print("sepal_lengthに関しては明らかな極端な外れ値は観察されない")
```

### 問題15
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

plt.scatter(data_setosa['sepal_width'], data_setosa['sepal_length'], color='b', label='setosa')
plt.scatter(data_versicolor['sepal_width'], data_versicolor['sepal_length'], color='r', label='versicolor')
plt.scatter(data_virginica['sepal_width'], data_virginica['sepal_length'], color='g', label='virginica')

plt.xlabel('sepal_width')
plt.ylabel('sepal_length')
plt.legend()
plt.show()
```

### 問題16
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

plt.scatter(data_setosa['sepal_width'], data_setosa['sepal_length'], color='b', label='setosa')
plt.scatter(data_versicolor['sepal_width'], data_versicolor['sepal_length'], color='r', label='versicolor')
plt.scatter(data_virginica['sepal_width'], data_virginica['sepal_length'], color='g', label='virginica')

plt.axvline(x=3.0, color='k', linestyle='--', label='boundary_x')
plt.axhline(y=6.0, color='k', linestyle='--', label='boundary_y')

plt.xlabel('sepal_width')
plt.ylabel('sepal_length')
plt.legend()
plt.show()
```

### 問題17
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

plt.scatter(data_setosa['petal_length'], data_setosa['petal_width'], color='b', label='setosa')
plt.scatter(data_versicolor['petal_length'], data_versicolor['petal_width'], color='r', label='versicolor')
plt.scatter(data_virginica['petal_length'], data_virginica['petal_width'], color='g', label='virginica')

plt.xlabel('petal_length')
plt.ylabel('petal_width')
plt.legend()
plt.show()

# グラフから分かることをコメント
print("setosaと他の種は簡単な境界線で分けられる")
```

### 問題18
```python
import seaborn as sns
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

ax.scatter(data_setosa['sepal_width'], data_setosa['sepal_length'], data_setosa['petal_length'], color='b', label='setosa')
ax.scatter(data_versicolor['sepal_width'], data_versicolor['sepal_length'], data_versicolor['petal_length'], color='r', label='versicolor')
ax.scatter(data_virginica['sepal_width'], data_virginica['sepal_length'], data_virginica['petal_length'], color='g', label='virginica')

ax.set_xlabel('sepal_width')
ax.set_ylabel('sepal_length')
ax.set_zlabel('petal_length')
ax.legend()
plt.show()
```

### 問題19
```python
import seaborn as sns
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

iris = sns.load_dataset("iris")

data_setosa = iris[iris["species"] == "setosa"].reset_index(drop=True)
data_versicolor = iris[iris["species"] == "versicolor"].reset_index(drop=True)
data_virginica = iris[iris["species"] == "virginica"].reset_index(drop=True)

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

ax.scatter(data_setosa['sepal_width'], data_setosa['sepal_length'], data_setosa['petal_length'], color='b', label='setosa')
ax.scatter(data_versicolor['sepal_width'], data_versicolor['sepal_length'], data_versicolor['petal_length'], color='r', label='versicolor')
ax.scatter(data_virginica['sepal_width'], data_virginica['sepal_length'], data_virginica['petal_length'], color='g', label='virginica')

# 視点を変更
ax.view_init(elev=0, azim=240)

ax.legend()
plt.show()

# 視点を変えたときの分布の違いをコメント
print("視点を変えてもsetosaは分けることができるが，versicolorとvirginicaは部分的に重なっている")
```

### 問題20
```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

iris = sns.load_dataset("iris")

data_small_pw = iris[iris['petal_width'] < 1.0].reset_index(drop=True)
print("unique species in data_small_pw:", data_small_pw['species'].unique())

data_small_pw['sepal_length'].hist()
plt.xlabel("sepal_length")
plt.ylabel("frequency")
plt.title("Histogram of sepal_length (petal_width < 1.0)")
plt.show()

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
species_colors = {'setosa': 'b', 'versicolor': 'r', 'virginica': 'g'}
for sp in data_small_pw['species'].unique():
    tmp = data_small_pw[data_small_pw['species'] == sp]
    ax.scatter(tmp['sepal_width'], tmp['sepal_length'], tmp['petal_length'],
               color=species_colors[sp], label=sp)

ax.set_xlabel('sepal_width')
ax.set_ylabel('sepal_length')
ax.set_zlabel('petal_length')
ax.legend()
plt.show()

print("petal_width が 1.0 より小さいデータはsetosaである.")
```