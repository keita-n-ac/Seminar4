#### 9回目 解答例
##### 事前準備
- コマンド
```bash
!pip install japanize-matplotlib
```

- ファイル読み込み
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import japanize_matplotlib

df = pd.read_csv("tourism-9.csv")

df.head()
```

##### 問題1
```python
df.head()
```

##### 問題2
```python
print(df.shape)
print(df.columns)
```

##### 問題3
```python
print(df.dtypes)
print(df.describe())
```

##### 問題4
```python
selected = df[
    df["visitors"] >= 200
]

print(selected)
print(selected.shape[0])
```

##### 問題5
```python
sapporo = df[
    df["city"] == "札幌"
]

sapporo.head()
```

##### 問題6
```python
city_mean = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

city_mean
```

##### 問題7
```python
plt.bar(
    city_mean["city"],
    city_mean["visitors"]
)

plt.title("都市別平均来訪者数")
plt.xlabel("都市")
plt.ylabel("平均来訪者数")

plt.show()
```

##### 問題8
```python
city_mean.plot(
    x="city",
    y="visitors",
    kind="bar",
    legend=False
)

plt.title("都市別平均来訪者数")
plt.xlabel("都市")
plt.ylabel("平均来訪者数")

plt.show()
```

##### 問題9
```python
sorted_df = city_mean.sort_values(
    "visitors",
    ascending=False
)

print(sorted_df)

sorted_df.plot(
    x="city",
    y="visitors",
    kind="barh",
    legend=False
)

plt.title("都市別平均来訪者数")
plt.xlabel("平均来訪者数")
plt.ylabel("都市")

plt.gca().invert_yaxis()

plt.show()
```

##### 問題10
```python
plt.scatter(
    df["visitors"],
    df["satisfaction"]
)

plt.title("来訪者数と満足度")
plt.xlabel("来訪者数")
plt.ylabel("満足度")

plt.show()
```

##### 問題11
```python
df.plot(
    kind="scatter",
    x="visitors",
    y="satisfaction"
)

plt.title("来訪者数と満足度")
plt.xlabel("来訪者数")
plt.ylabel("満足度")

plt.show()
```

##### 問題12
```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction"
)

plt.title("来訪者数と満足度")
plt.xlabel("来訪者数")
plt.ylabel("満足度")

plt.show()
```

##### 問題13
```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction",
    hue="region"
)

plt.title("地域別：来訪者数と満足度")
plt.xlabel("来訪者数")
plt.ylabel("満足度")

plt.show()
```

##### 問題14
```python
sns.barplot(
    data=df,
    x="region",
    y="spending",
    errorbar=None,
    color="steelblue"
)

plt.title("地域別平均消費金額")
plt.xlabel("地域")
plt.ylabel("平均消費金額（円）")

plt.show()
```

##### 問題15
```python
region_spending = df.groupby(
    "region"
)["spending"].mean()

print(region_spending)

region_spending.plot(
    kind="bar"
)

plt.title("地域別平均消費金額")
plt.xlabel("地域")
plt.ylabel("平均消費金額（円）")

plt.show()
```

##### 問題16
```python
sns.histplot(
    data=df,
    x="spending",
    bins=10,
    color="steelblue"
)

plt.title("消費金額の分布")
plt.xlabel("消費金額（円）")
plt.ylabel("件数")

plt.show()
```

##### 問題17
```python
sns.histplot(
    data=df,
    x="spending",
    bins=10,
    hue="region",
    multiple="stack"
)

plt.title("地域別消費金額の分布")
plt.xlabel("消費金額（円）")
plt.ylabel("件数")

plt.show()
```

##### 問題18
```python
sns.boxplot(
    data=df,
    x="region",
    y="satisfaction"
)

plt.title("地域別満足度")
plt.xlabel("地域")
plt.ylabel("満足度")

plt.show()

df.groupby("region")[
    "satisfaction"
].mean()
```

##### 問題19
```python
sns.lineplot(
    data=df,
    x="month",
    y="visitors",
    errorbar=None
)

plt.title("月別平均来訪者数")
plt.xlabel("月")
plt.ylabel("平均来訪者数")

plt.show()

sns.lineplot(
    data=df,
    x="month",
    y="visitors",
    hue="region",
    errorbar=None
)

plt.title("地域別月別平均来訪者数")
plt.xlabel("月")
plt.ylabel("平均来訪者数")

plt.show()
```

##### 問題20
```python
selected = df[
    (df["city"] == "札幌")
    & (df["satisfaction"] >= 4.0)
]

print(selected)
print(selected.shape[0])

sns.scatterplot(
    data=selected,
    x="stay_days",
    y="spending"
)

plt.title("札幌：宿泊日数と消費金額")
plt.xlabel("宿泊日数")
plt.ylabel("消費金額（円）")

plt.show()
```

##### 発展1
```python
# seaborn
sns.barplot(
    data=df,
    x="season",
    y="spending",
    errorbar=None,
    color="steelblue"
)

plt.title("季節別平均消費金額")
plt.xlabel("季節")
plt.ylabel("平均消費金額（円）")

plt.show()

# pandas
season_mean = df.groupby(
    "season"
)["spending"].mean()

season_mean.plot(
    kind="bar"
)

plt.title("季節別平均消費金額")
plt.xlabel("季節")
plt.ylabel("平均消費金額（円）")

plt.show()
```

##### 発展2
```python
sns.boxplot(
    data=df,
    x="season",
    y="spending"
)

plt.title("季節別消費金額の分布")
plt.xlabel("季節")
plt.ylabel("消費金額（円）")

plt.show()
```

##### 発展3
```python
sns.scatterplot(
    data=df,
    x="stay_days",
    y="spending",
    hue="region"
)

plt.title("地域別：宿泊日数と消費金額")
plt.xlabel("宿泊日数")
plt.ylabel("消費金額（円）")

plt.show()
```

##### 発展4
```python
selected = df[
    df["satisfaction"] >= 4.0
]

region_mean = (
    selected.groupby("region")[
        "spending"
    ]
    .mean()
    .reset_index()
)


sorted_df = region_mean.sort_values(
    "spending",
    ascending=False
)

plt.bar(
    sorted_df["region"],
    sorted_df["spending"]
)

plt.title("満足度4.0以上の地域別平均消費金額")
plt.xlabel("地域")
plt.ylabel("平均消費金額（円）")

plt.show()
```
