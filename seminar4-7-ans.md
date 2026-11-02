#### 7回目解答例

##### 事前準備
```python
import pandas as pd
df = pd.read_csv("tourism-7.csv")
df.head()
```

##### 問題1
```python
df[df["visitors"] >= 1000]
```

##### 問題2
```python
df[df["visitors"] < 500]
```

##### 問題3
```python
df[df["rating"] >= 4.0]
```

##### 問題4
```python
df[df["rating"] >= 4.5]
```

##### 問題5
```python
df[df["city"] == "札幌"]
```

##### 問題6
```python
df[df["city"] == "函館"]
```

##### 問題7
```python
df[df["category"] == "飲食"]
```

##### 問題8
```python
df[df["category"] != "宿泊"]
```

##### 問題9
```python
df[
    (df["visitors"] >= 1000)
    & (df["rating"] >= 4.0)
]
```

##### 問題10
```python
df[
    (df["city"] == "札幌")
    & (df["rating"] >= 4.5)
]
```

##### 問題11
```python
df[
    (df["visitors"] >= 1500)
    | (df["rating"] >= 4.5)
]
```

##### 問題12
```python
df.sort_values(
    "visitors",
    ascending=True
)
```

##### 問題13
```python
df.sort_values(
    "visitors",
    ascending=False
)
```

##### 問題14
```python
df.sort_values(
    "rating",
    ascending=False
)
```

##### 問題15
```python
df.sort_values(
    "visitors",
    ascending=False
).head(10)
```

##### 問題16
```python
df.sort_values(
    "rating",
    ascending=False
).head(5)
```

##### 問題17
```python
df["visitors_100"] = df["visitors"] / 100
df.head()
```

##### 問題18
```python
df["rating_score"] = df["rating"] * 100
df.head()
```

##### 問題19
```python
df["visitor_level"] = "少ない"
df.loc[
    df["visitors"] >= 1000,
    "visitor_level"
] = "多い"

df[["city", "visitors", "visitor_level"]]
```

##### 問題20
```python
high_rating = df[
    df["rating"] >= 4.5
]

high_rating.to_csv(
    "high_rating.csv",
    index=False
)

check = pd.read_csv("high_rating.csv")
check.head()
```

##### 発展1
```python
df[
    (df["city"] == "札幌")
    | (df["city"] == "函館")
]
```

##### 発展2
```python
df[
    (df["category"] == "飲食")
    & (df["rating"] >= 4.0)
]
```

##### 発展3
```python
result = df[
    df["visitors"] >= 1000
]

result.sort_values(
    "visitors",
    ascending=False
)
```

##### 発展4
```python
result = df[
    df["rating"] >= 4.0
]

result.to_csv(
    "good_rating.csv",
    index=False
)

check = pd.read_csv("good_rating.csv")
check.head()
```
