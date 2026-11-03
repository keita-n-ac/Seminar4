#### 10回目 解答例
##### 事前準備
- コマンド
```bash
!pip -q install geopandas japanize-matplotlib
```

- ライブラリ読み込み
```python
import geopandas as gpd
import matplotlib.pyplot as plt
import japanize_matplotlib
```

##### 問題1
```python
gdf = gpd.read_file("hokkaido_areas.geojson")
```

##### 問題2
```python
print(gdf.head())
print(gdf.shape)
print(gdf.columns)
```

##### 問題3
```python
gdf["area_name"]
```

##### 問題4
```python
gdf.plot()
plt.show()
```

##### 問題5
```python
gdf.plot(
    color="lightgreen"
)
plt.show()
```

##### 問題6
```python
gdf.plot(
    color="lightblue",
    edgecolor="black",
    linewidth=1.5
)

plt.show()
```

##### 問題7
```python
fig, ax = plt.subplots(
    figsize=(10, 8)
)

gdf.plot(
    ax=ax,
    color="lightblue",
    edgecolor="black"
)

ax.set_title("北海道の地域区分")

plt.show()
```

##### 問題8
```python
fig, ax = plt.subplots(
    figsize=(10, 8)
)

gdf.plot(
    ax=ax,
    color="lightblue",
    edgecolor="black"
)

ax.set_title("北海道の地域区分")
ax.set_axis_off()
plt.show()
```

##### 発展1
```python
oshima = gdf[
    gdf["area_name"] == "渡島総合振興局"
]

print(oshima)

oshima.plot(
    color="orange",
    edgecolor="black"
)

plt.title("渡島総合振興局")

plt.show()
```

##### 発展2
```python
ishikari = gdf[
    gdf["area_name"] == "石狩振興局"
]

fig, ax = plt.subplots(
    figsize=(9, 7)
)

gdf.plot(
    ax=ax,
    color="lightgray",
    edgecolor="white",
    linewidth=0.6
)

ishikari.plot(
    ax=ax,
    color="red",
    edgecolor="black"
)

ax.set_title("石狩振興局の位置")
ax.set_axis_off()

plt.show()
```

##### 発展3
```python
fig, ax = plt.subplots(
    figsize=(10, 8)
)

gdf.plot(
    ax=ax,
    color="lightgreen",
    edgecolor="black",
    linewidth=0.8
)

ax.set_title("北海道の地図")
ax.set_axis_off()

fig.savefig(
    "hokkaido_map.png",
    dpi=150,
    bbox_inches="tight"
)

plt.show()
```
