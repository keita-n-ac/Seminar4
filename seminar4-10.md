### ゼミナールⅣ 10回目
#### GeoPandas入門1
##### Pythonで北海道の地図を描いてみよう

##### 1. 今回の目標
これまでの授業では，pandasを使ってCSVファイルを読み込み，条件に合うデータを取り出したり，
matplotlibやseabornを使ってグラフを作成したりしました．

今回は，**GeoPandas（ジオパンダス）** を使って，Pythonで地図を表示します．

今回の目標は次の4つです．

- GeoPandasとpandasの違いを説明できる
- GeoJSON形式の地図データを読み込める
- 地図の色，境界線，タイトルを変更できる
- 特定の振興局・総合振興局の区域だけを表示できる

**今回のゴール：自分で北海道の地図を描き，色や表示する地域を変えられるようになること．**

※ 今回は地図を「表示する」ことに集中します．人口などの統計値による色分けは次回，位置情報を使った分析はその次の回に行います．

---

##### 2. pandasとGeoPandasの違い

pandasでは，次のような表を扱いました．

| city | visitors |
|---|---:|
| 札幌 | 450 |
| 函館 | 280 |
| 旭川 | 210 |

これに対してGeoPandasは，**表のデータと地図上の形を一緒に扱えるライブラリ**です．

GeoPandasで扱う表を **GeoDataFrame（ジオデータフレーム）** と呼びます．通常のDataFrameと同様に，列の取り出しや条件抽出ができます．

重要なのは，地図の形を表す **`geometry` 列**があることです．

| area_name | geometry |
|---|---|
| 石狩振興局 | 地図上の区域の形 |
| 渡島総合振興局 | 地図上の区域の形 |

地図の形を持つので，GeoDataFrameでは `plot()` によって地図を描けます．

---

##### 3. 今回使うデータ

使用ファイル名は **`hokkaido_areas.geojson`** です．

このファイルには，北海道の14の振興局・総合振興局の区域が入っています．地理的な境界線は，国土交通省「国土数値情報（行政区域データ）」をもとにした2026年1月1日基準の公開データを，授業向けに統合・簡略化したものです．小さな島などは元の軽量化処理で省略されている場合があります．

GeoJSONは，地域の形や位置を記録するファイル形式の1つです．CSVのように「表の値だけ」を扱うのではなく，地図に必要な座標も記録しています．

今回は次の列を使用します．

| 列名 | 内容 |
|---|---|
| `area_name` | 振興局・総合振興局の名称 |
| `geometry` | 地図上の区域の形 |

**準備について：** 配布済みの `hokkaido_areas.geojson` をColabにアップロードしてください．配布ファイルがない場合は，添付のColabノートブックの「地図データの準備」セルを先に実行すると生成できます．この準備セルの内容は今回の学習対象ではありません．

---

##### 4. ライブラリを準備する

Google ColabでGeoPandasが使えない場合は，次のセルを実行してインストールします．

```python
!pip -q install geopandas japanize-matplotlib
```

次に，ライブラリを読み込みます．

```python
import geopandas as gpd
import matplotlib.pyplot as plt
import japanize_matplotlib
```

`gpd` はGeoPandas，`plt` はmatplotlibを表します．`japanize_matplotlib` はグラフのタイトルなどを日本語で表示するために使用します．

---

##### 5. GeoJSONを読み込む

GeoPandasでは，地図データを **`read_file()`** で読み込みます．

```python
gdf = gpd.read_file("hokkaido_areas.geojson")

gdf.head()
```

pandasの `pd.read_csv()` と似ていますが，GeoPandasでは `gpd.read_file()` を使います．

`gdf` はGeoDataFrameを保存する変数名です．`head()` の使い方はpandasと同じです．

---

##### 6. 行数・列名を確認する

```python
gdf.shape
```

今回配布するデータは **14行×2列** です．14行は14の振興局・総合振興局に対応します．

列名も確認します．

```python
gdf.columns
```

また，名称だけを取り出すこともできます．

```python
gdf["area_name"]
```

これらの操作は，これまでのpandasの復習です．

---

##### 7. geometryとは？

GeoDataFrameの `geometry` 列には，**地図上の形**が保存されています．

```python
gdf.geometry
```

今回のデータには地域の面を表す `Polygon` や `MultiPolygon` が含まれます．

- `Point`：地点（例：駅や施設の位置）
- `LineString`：線（例：道路や河川）
- `Polygon`：面（例：市町村の区域）
- `MultiPolygon`：離れた複数の面をひとまとまりにした形

今日は面のデータを使います．

---

##### 8. 最初の地図を描く

それでは，北海道の地図を表示します．

```python
gdf.plot()
plt.show()
```

これだけで区域の形を地図として表示できます．

pandasでは `df.plot()` を使って棒グラフなどを作りましたが，GeoPandasの `gdf.plot()` は，`geometry` に記録された位置・形を使って地図を表示します．

---

##### 9. 地図の色を変更する

`color` を使うと，区域の塗りつぶし色を指定できます．

```python
gdf.plot(color="lightblue")
plt.show()
```

色を `lightgreen` や `orange` に変えることもできます．

```python
gdf.plot(color="lightgreen")
plt.show()
```

---

##### 10. 境界線の色と太さを変更する

`edgecolor` は区域の境界線の色，`linewidth` は線の太さです．

```python
gdf.plot(
    color="lightblue",
    edgecolor="black",
    linewidth=0.8
)

plt.show()
```

`linewidth=0.3` と `linewidth=2` を比べると，線の太さによる見え方の違いが分かります．

---

##### 11. 地図の大きさとタイトルを変更する

matplotlibの `figsize` を使うと，図の大きさを変更できます．

```python
fig, ax = plt.subplots(figsize=(9, 7))

gdf.plot(
    ax=ax,
    color="lightblue",
    edgecolor="black",
    linewidth=0.8
)

ax.set_title("北海道の振興局・総合振興局")
plt.show()
```

`figsize=(9, 7)` は図の横・縦の大きさ（インチ）です．

`ax=ax` は，matplotlibで用意した描画場所に地図を表示するという意味です．

---

##### 12. 地図の周りの目盛りを消す

地域の形だけを見せたい場合には，軸の目盛りを非表示にできます．

```python
fig, ax = plt.subplots(figsize=(9, 7))

gdf.plot(
    ax=ax,
    color="lightblue",
    edgecolor="black",
    linewidth=0.8
)

ax.set_title("北海道の地図")
ax.set_axis_off()

plt.show()
```

`set_axis_off()` は，地図の外側にある軸や目盛りを消す命令です．

---

##### 13. 1つの地域だけを取り出す

GeoDataFrameでも，pandasと同じように条件抽出ができます．

例えば，石狩振興局のデータだけを取り出します．

```python
ishikari = gdf[
    gdf["area_name"] == "石狩振興局"
]

ishikari
```

抽出した地域だけを地図に描きます．

```python
ishikari.plot(
    color="orange",
    edgecolor="black"
)

plt.title("石狩振興局")
plt.show()
```

別の地域名を指定すれば，その地域だけを表示できます．

---

##### 14. 元の地図に特定地域を重ねる（発展的な実演）

2つの地図を同じ描画場所に重ねることもできます．

```python
fig, ax = plt.subplots(figsize=(9, 7))

gdf.plot(
    ax=ax,
    color="lightgray",
    edgecolor="white",
    linewidth=0.6
)

ishikari.plot(
    ax=ax,
    color="orange",
    edgecolor="black"
)

ax.set_title("石狩振興局の位置")
ax.set_axis_off()

plt.show()
```

最初に全域を灰色で描き，その上に石狩振興局だけをオレンジ色で重ねています．

---

##### 15. 今回のまとめ

今回は，次の処理を学習しました．

```python
# 読み込む
gdf = gpd.read_file("hokkaido_areas.geojson")

# データを確認する
gdf.head()
gdf.shape
gdf.columns

# 地図を表示する
gdf.plot()
plt.show()

# 1つの地域を取り出す
ishikari = gdf[gdf["area_name"] == "石狩振興局"]
```

今回の重要な点は，**GeoDataFrameはpandasの表と同じように扱え，さらに地図として表示できる**ということです．

---

#### 練習問題

`hokkaido_areas.geojson` を使用して，次の問題に取り組んでください．問題1〜8が基本問題です．問題9以降は余裕がある人向けです．

##### 問題1　GeoJSONを読み込む
GeoPandasを使用して `hokkaido_areas.geojson` を読み込み，`gdf` に保存してください．

##### 問題2　データを確認する
`gdf` の先頭5行，行数・列数，列名を表示してください．

##### 問題3　地域名を確認する
`area_name` 列だけを表示し，どのような名称があるか確認してください．

##### 問題4　北海道の地図を表示する
`gdf.plot()` を使って北海道の区域を地図に表示してください．

##### 問題5　地図の塗りつぶし色を変更する
すべての区域を `lightgreen` で表示してください．

##### 問題6　境界線を変更する
塗りつぶし色を `lightblue`，境界線を `black`，線の太さを `1.5` にして表示してください．

##### 問題7　大きさとタイトルを設定する
`figsize=(10, 8)` として地図を描いてください．タイトルは「北海道の地域区分」としてください．

##### 問題8　目盛りを消す
問題7の地図について，軸と目盛りを消して表示してください．

---

#### 余裕がある人向け

##### 発展問題1　地域の抽出
`area_name` が「渡島総合振興局」のデータだけを取り出し，`oshima` に保存してください．その区域だけをオレンジ色で描いてください．

##### 発展問題2　地域を強調する
北海道全域を `lightgray` で描いてから，「石狩振興局」を `red` で重ねて表示してください．地図のタイトルは「石狩振興局の位置」としてください．

##### 発展問題3　地図を画像として保存する
自分で色とタイトルを設定した北海道の地図を `hokkaido_map.png` という名前で保存してください．ヒント：`fig.savefig("hokkaido_map.png", dpi=150, bbox_inches="tight")` を `plt.show()` の前に実行します．

---

