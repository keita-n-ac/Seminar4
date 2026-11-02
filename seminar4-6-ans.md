#### 6回目解答例

##### 問題1
```python
with open("tourism-6.csv", "r", encoding="utf-8") as f:
    text = f.read()

print(text)
```

##### 問題2
```python
with open("tourism-6.csv", "r", encoding="utf-8") as f:
    line = f.readline()

print(line)
```

##### 問題3
```python
import pandas as pd
```

##### 問題4
```python
import pandas as pd
df = pd.read_csv("tourism-6.csv")
```

##### 問題5
```python
df
```

##### 問題6
```python
df.head()
```

##### 問題7
```python
df.head(10)
```

##### 問題8
```python
df.tail()
```

##### 問題9
```python
df.shape
```

##### 問題10
```python
df.columns
```

##### 問題11
```python
df["city"]
```

##### 問題12
```python
df["visitors"]
```

##### 問題13
```python
df[["city", "visitors"]]
```

##### 問題14
```python
df[["city", "category", "rating"]]
```

##### 問題15
```python
df["visitors"].sum()
```

##### 問題16
```python
df["visitors"].mean()
```

##### 問題17
```python
df["visitors"].max()
```

##### 問題18
```python
print("最大値：", df["rating"].max())
print("最小値：", df["rating"].min())
```

##### 問題19
```python
df.describe()
```

##### 問題20
```python
result = df[["city", "category", "visitors"]]

result.to_csv(
    "tourism_basic.csv",
    index=False
)

df2 = pd.read_csv("tourism_basic.csv")
df2.head()
```

##### 発展1
```python
df["rating"].mean()
```

##### 発展2
```python
df["visitors"].min()
```

##### 発展3
```python
df.tail(10)
```

##### 発展4
```python
esult = df[["city", "rating"]]

result.to_csv(
    "city_rating.csv",
    index=False
)

check = pd.read_csv("city_rating.csv")
check.head()
```

