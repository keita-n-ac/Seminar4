## A
### 1
```python
import seaborn as sns
df = sns.load_dataset("iris")
print(df.head())
```

### 2
```python
import seaborn as sns
df = sns.load_dataset("iris")
print('shape:', df.shape)
print('columns:', df.columns)
```

### 3
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
print(df_num.head())

```

### 4
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
print(df_num.corr())
```

### 5
```python
import seaborn as sns
df = sns.load_dataset("iris")
print(df.dtypes)
```

### 6
```python
import seaborn as sns
df = sns.load_dataset("iris")
print("df['species'].unique()")
print(df["species"].unique())
print()
print("df['species'].value_counts()")
print(df["species"].value_counts())
```

### 7
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
print(df_num.describe())
```

## B
### 8
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
sns.heatmap(df_num.corr(), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (df_num)")
plt.show()
```

### 9
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
sns.heatmap(df_num.corr().round(2), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (whitegrid)")
plt.show()
```

### 10
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
sns.heatmap(df_num.corr(), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (round(2))")
plt.show()
```

### 11
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
print(df_num.corr()["petal_length"])
```

### 12
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
print(df_num.corr()["petal_length"].abs().sort_values(ascending=False))
```

### 13
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
data = df[df["species"] == "setosa"].drop(columns="species")
sns.heatmap(data.corr(), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (setosa)")
plt.show()
```

### 14
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
data2 = df[df["species"] == "versicolor"].drop(columns="species")
sns.heatmap(data2.corr(), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (versicolor)")
plt.show()

data3 = df[df["species"] == "virginica"].drop(columns="species")
sns.heatmap(data3.corr(), annot=True, vmin=-1, vmax=1, center=0)
plt.title("Correlation Heatmap (virginica)")
plt.show()
```

## C
### 15
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_num = df.drop(columns="species")
sns.pairplot(data=df_num)
plt.show()
```

### 16
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.pairplot(data=df)
plt.show()
```

### 17
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.pairplot(data=df, hue="species")
plt.show()
```

### 18
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_sepal = df[["sepal_length", "sepal_width", "species"]]
sns.pairplot(data=df_sepal, hue="species")
plt.show()
```

### 19
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_petal = df[["petal_length", "petal_width", "species"]]
sns.pairplot(data=df_petal, hue="species")
plt.show()
```

### 20
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_setosa_num = df[df["species"] == "setosa"].drop(columns="species")
sns.pairplot(data=df_setosa_num, kind="reg")
plt.show()
```

### 21
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_versicolor_num = df[df["species"] == "versicolor"].drop(columns="species")
sns.pairplot(data=df_versicolor_num, kind="reg")
plt.show()
```

### 22
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df_virginica_num = df[df["species"] == "virginica"].drop(columns="species")
sns.pairplot(data=df_virginica_num, kind="reg")
plt.show()
```

### 23
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.scatterplot(data=df, x="sepal_length", y="petal_length")
plt.title("Sepal Length vs Petal Length")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Petal Length (cm)")
plt.show()
```

### 24
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.scatterplot(data=df, x="sepal_length", y="petal_length", hue="species")
plt.title("Sepal Length vs Petal Length by Species")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Petal Length (cm)")
plt.show()
```

## D
### 25
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
plt.hist(df["petal_length"], bins=20)
plt.title("Histogram of Petal Length")
plt.xlabel("Petal Length (cm)")
plt.ylabel("Frequency")
plt.show()
```

### 26
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.histplot(data=df, x="petal_length", hue="species", bins=20)
plt.title("Histogram of Petal Length by Species")
plt.xlabel("Petal Length (cm)")
plt.ylabel("Count")
plt.show()
```

### 27
```python
import seaborn as sns
df = sns.load_dataset("iris")
print(df.groupby("species").mean(numeric_only=True))
```

### 28
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
data = df.groupby("species").mean(numeric_only=True)
data["petal_length"].plot.bar()
plt.title("Mean Petal Length by Species")
plt.xlabel("Species")
plt.ylabel("Mean Petal Length (cm)")
plt.show()
```

### 29
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.boxplot(data=df, x="species", y="sepal_width", width=0.5)
plt.title("Sepal Width by Species")
plt.xlabel("Species")
plt.ylabel("Sepal Width (cm)")
plt.show()
```

### 30
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
sns.boxplot(data=df, x="species", y="petal_width", width=0.5)
plt.title("Petal Width by Species")
plt.xlabel("Species")
plt.ylabel("Petal Width (cm)")
plt.show()
```

### 31
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_sl6 = df[df["sepal_length"] >= 6.0]
print("Number of rows:", df_sl6.shape[0])
print(df_sl6.head())
```

### 32
```python
import seaborn as sns
df = sns.load_dataset("iris")
df_cond = df[(df["sepal_length"] >= 6.0) & (df["petal_width"] >= 1.5)]
print(df_cond["species"].value_counts())
```

## E
### 33
```python
import seaborn as sns
df = sns.load_dataset("iris")
df["sepal_ratio"] = df["sepal_length"] / df["sepal_width"]
print(df.head())
```

### 34
```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("iris")
df["sepal_ratio"] = df["sepal_length"] / df["sepal_width"]
plt.hist(df["sepal_ratio"], bins=20)
plt.title("Histogram of Sepal Ratio")
plt.xlabel("Sepal Length / Sepal Width")
plt.ylabel("Frequency")
plt.show()
```

### 35
```python
import seaborn as sns
df = sns.load_dataset("iris")
df["sepal_ratio"] = df["sepal_length"] / df["sepal_width"]
df.to_csv("iris_dataset.csv", index=False)
df_loaded = pd.read_csv("iris_dataset.csv")
print(df_loaded.head())
```
