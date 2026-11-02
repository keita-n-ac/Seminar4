#### 8回目 解答例

##### 事前準備
```python
import pandas as pd
df = pd.read_csv("tourism-8.csv")
df.head()
```

##### 問題1
```python
df["city"].value_counts()
```

##### 問題2
```python
df["category"].value_counts()
```

##### 問題3
```python
df.groupby("city")["visitors"].mean()
```

##### 問題4
```python
df.groupby("city")["visitors"].sum()
```

##### 問題5
```python
df.groupby("city")["visitors"].max()
```

##### 問題6
```python
df.groupby("category")["visitors"].mean()
```

##### 問題7
```python
df.groupby("category")["rating"].mean()
```

##### 問題8
```python
df.groupby("city")["rating"].mean()
```

##### 問題9
```python
result = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)
result
```

##### 問題10
```python
result = result.sort_values(
    "visitors",
    ascending=False
)
result
```

##### 問題11
```python
df.groupby("city")["visitors"].agg(
    ["count", "mean", "max", "min"]
)
```

##### 問題12
```python
df.groupby("category")["rating"].agg(
    ["mean", "max", "min"]
)
```

##### 問題13
```python
df.groupby(
    ["city", "category"]
)["visitors"].mean()
```

##### 問題14
```python
result = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)
result.to_csv(
    "city_average.csv",
    index=False
)
check = pd.read_csv("city_average.csv")
check.head()
```

##### 問題15
```python
city_info = pd.read_csv("city_info.csv")
city_info
```


##### 問題16
```python
merged = pd.merge(
    df,
    city_info,
    on="city"
)
merged.head()
```

##### 問題17
```python
merged[
    ["city", "visitors", "population"]
]
```

##### 問題18
```python
merged["visitors_per_10000"] = (
    merged["visitors"]
    / merged["population"]
    * 10000
)

merged[
    [
        "city",
        "visitors",
        "population",
        "visitors_per_10000"
    ]
].head()
```


##### 問題19
```python
result = (
    merged.groupby("city")[
        "visitors_per_10000"
    ]
    .mean()
    .reset_index()
)

result = result.sort_values(
    "visitors_per_10000",
    ascending=False
)

result
```

##### 問題20
```python
merged.to_csv(
    "tourism_merged.csv",
    index=False
)

check = pd.read_csv("tourism_merged.csv")
check.head()
```

##### 発展1
```python
df.groupby("city")[
    ["visitors", "rating"]
].mean()
```

##### 発展2
```python
result = (
    df.groupby("category")["visitors"]
    .mean()
    .reset_index()
)
result.sort_values(
    "visitors",
    ascending=False
)
```

##### 発展3
```python
merged[
    merged["population"] >= 100000
]
```

##### 発展4
```python
large_city = merged[
    merged["population"] >= 100000
]
large_city.groupby("city")[
    "visitors"
].mean()
```
