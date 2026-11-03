#### 11回目 解答例
##### 事前準備
- コマンド
```bash
!pip -q install geopandas japanize-matplotlib
```

- ライブラリ読み込み
```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt
import japanize_matplotlib
```

##### 問題1
```python
gdf = gpd.read_file("hokkaido_areas.geojson")
print(gdf.head())

stats = pd.read_csv("area_stats.csv")
print(stats.head())
```

##### 問題2
```python
print("地図：", gdf.shape)
print("統計：", stats.shape)
print(gdf.columns)
print(stats.columns)
```

##### 問題3
```python
merged = gdf.merge(
    stats,
    on="area_name",
    how="left"
)

print(merged.head())
print(merged.shape)
print(merged["population"].isna().sum())
```

##### 問題4
```python
merged.plot(
    column="visitors",
    cmap="YlOrRd",
    legend=True,
    edgecolor="white"
)

plt.title("地域別来訪回数（架空データ）")

plt.show()
```

##### 問題5
```python
merged.plot(
    column="visitors",
    cmap="Blues",
    legend=True,
    edgecolor="white"
)

plt.title("地域別来訪回数（架空データ）")

plt.show()
```

##### 問題6
```python
merged.plot(
    column="population",
    cmap="Greens",
    legend=True,
    edgecolor="white"
)

plt.title("地域別人口（架空データ）")

plt.show()

```

##### 問題7
```python
merged["visitors_per_10k"] = (
    merged["visitors"]
    / merged["population"]
    * 10000
)

merged[
    [
        "area_name",
        "visitors_per_10k"
    ]
]
```

##### 問題8
```python
merged.plot(
    column="visitors_per_10k",
    cmap="Purples",
    legend=True,
    edgecolor="white"
)

plt.title("人口1万人当たりの来訪回数（架空データ）")

plt.show()
```

##### 発展1
```python
result = merged[
    ["area_name", "visitors"]
]

result.sort_values(
    "visitors",
    ascending=False
).head(3)
```

##### 発展2
```python
merged.plot(
    column="spending",
    cmap="Oranges",
    legend=True,
    edgecolor="white"
)

plt.title("来訪1回当たり平均消費金額（架空データ）")

plt.show()
```


##### 発展3
```python
fig, axes = plt.subplots(
    1, 2,
    figsize=(14, 6)
)

merged.plot(
    ax=axes[0],
    column="visitors",
    cmap="YlOrRd",
    legend=True,
    edgecolor="white"
)

axes[0].set_title("地域別来訪回数")
axes[0].set_axis_off()

merged.plot(
    ax=axes[1],
    column="visitors_per_10k",
    cmap="Purples",
    legend=True,
    edgecolor="white"
)

axes[1].set_title("人口1万人当たりの来訪回数")
axes[1].set_axis_off()

plt.tight_layout()
plt.show()
```
