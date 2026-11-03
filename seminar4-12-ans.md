#### 12回目 解答例
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
spots_df = pd.read_csv("tourist_spots.csv")
print(spots_df.head())
print(spots_df.shape)
```

##### 問題2
```python
print(spots_df["category"].unique())
print(spots_df["category"].value_counts())
```

##### 問題3
```python
spots = gpd.GeoDataFrame(
    spots_df,
    geometry=gpd.points_from_xy(
        spots_df["longitude"],
        spots_df["latitude"]
    ),
    crs="EPSG:4326"
)

print(spots.head())
print(spots.shape)
print(spots.geometry.head())

spots = spots.to_crs(gdf.crs)
```

##### 問題4
```python
ax = gdf.plot(
    figsize=(9, 8),
    color="lightgray",
    edgecolor="black"
)

spots.plot(
    ax=ax,
    color="red",
    markersize=30
)

ax.set_title("北海道の架空観光施設")
ax.set_axis_off()

plt.show()
```

##### 問題5
```python
nature = spots[
    spots["category"] == "自然体験"
]

print(nature.head())

print(nature.shape[0])

ax = gdf.plot(
    figsize=(9, 8),
    color="lightgray",
    edgecolor="black"
)

nature.plot(
    ax=ax,
    color="green",
    markersize=35
)

ax.set_title("自然体験施設（架空データ）の位置")
ax.set_axis_off()

plt.show()
```

##### 問題6
```python
joined = spots.sjoin(
    gdf[["area_name", "geometry"]],
    how="left",
    predicate="within"
)

joined[
    ["spot_name", "area_name"]
]

print(joined["area_name"].isna().sum())
```

##### 問題7
```python
valid_spots = joined.dropna(
    subset=["area_name"]
)

counts = (
    valid_spots.groupby("area_name")
    .size()
    .reset_index(name="spot_count")
)

print(counts)
```

##### 問題8
```python
map_counts = gdf.merge(
    counts,
    on="area_name",
    how="left"
)

map_counts["spot_count"] = (
    map_counts["spot_count"]
    .fillna(0)
    .astype(int)
)

ax = map_counts.plot(
    column="spot_count",
    cmap="YlGnBu",
    legend=True,
    edgecolor="white",
    linewidth=0.8,
    figsize=(9, 8)
)

ax.set_title("地域別・架空施設数")
ax.set_axis_off()

plt.show()
```

##### 発展1
```python
ishikari_spots = joined[
    joined["area_name"] == "石狩振興局"
]

ishikari_spots[
    ["spot_name", "category"]
]

print(ishikari_spots.shape[0])
```

##### 発展2
```python
sorted_counts = counts.sort_values(
    "spot_count",
    ascending=False
)

sorted_counts.head(3)
```

##### 発展3
```python
fig, ax = plt.subplots(
    figsize=(10, 8)
)

map_counts.plot(
    ax=ax,
    column="spot_count",
    cmap="YlGnBu",
    legend=True,
    edgecolor="white",
    linewidth=0.8
)

ax.set_title("地域別・架空施設数")
ax.set_axis_off()

plt.savefig(
    "spot_count_map.png",
    dpi=150,
    bbox_inches="tight"
)

plt.show()
```
