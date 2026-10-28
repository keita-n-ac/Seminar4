### ゼミナールⅣ 第12回
#### GeoPandas入門3
##### 観光施設の位置を地図に重ね，地域ごとの施設数を調べよう

##### 1. 今回の目標
第10回では，北海道14振興局・総合振興局の地図を描きました．
第11回では，`area_stats.csv` の数値を地図と `merge()` で結合し，数値に応じて地域を色分けしました．

第12回は，**CSVに記録された緯度・経度から地図上の点を作成し，その点がどの地域にあるかを調べる**ことを学習します．

今回の目標は次の5つです．

1. 緯度・経度と地図上の「点」の関係を説明できる．
2. CSVからGeoDataFrameの点データを作成できる．
3. 北海道の地図と施設の点を重ねて表示できる．
4. `sjoin()` を使って施設が属する地域を調べられる．
5. 地域別の施設件数を集計し，地図上に表現できる．

**今回のゴール：架空の観光施設を北海道の地図に表示し，各振興局・総合振興局の施設数を地図で比較できること．**

※ 距離計算や `buffer()` は，今回の必修内容には含めません．

---

##### 2. 使用するファイル

今回は次の2ファイルを使用します．

| ファイル名 | 内容 | 主な列 |
|---|---|---|
| `hokkaido_areas.geojson` | 第10・11回で使用した北海道14地域の地図 | `area_name`, `geometry` |
| `tourist_spots.csv` | 今回新しく用意した架空の観光施設49件 | `spot_id`, `spot_name`, `category`, `longitude`, `latitude` |

**重要：** `tourist_spots.csv` の施設はすべて授業用に考えた**架空の施設**です．座標は北海道内の都市周辺を参考に設定した学習用の近似値であり，実際の施設の所在地を表すものではありません．実在施設の件数や分布を推定するためには使えません．

今回は `area_stats.csv` は使用しません．前回までの地図ファイルをそのまま利用します．

---

##### 3. Google Colabの準備

最初に必要なライブラリをインストールします．

```python
!pip -q install geopandas japanize-matplotlib
```

続いてライブラリを読み込みます．

```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt
import japanize_matplotlib
```

- `pd`：pandas（CSVの読み込みと集計）
- `gpd`：GeoPandas（地図の読み込みと位置情報の分析）
- `plt`：matplotlib（グラフの設定）

教員から配布された `hokkaido_areas.geojson` と `tourist_spots.csv` をGoogle Colabにアップロードしてください．

```python
from google.colab import files
files.upload()
```

左側のフォルダーアイコンからアップロードしても構いません．

---

##### 4. 地図とCSVを読み込む

地図データを読み込みます．

```python
gdf = gpd.read_file("hokkaido_areas.geojson")
gdf.head()
```

観光施設のCSVも読み込みます．

```python
spots_df = pd.read_csv("tourist_spots.csv")
spots_df.head()
```

`gdf` は地域の形を持つGeoDataFrame，`spots_df` は通常のDataFrameです．

それぞれの行数と列数を確認します．

```python
print("地域データ：", gdf.shape)
print("施設データ：", spots_df.shape)
```

この授業用データでは，地図は **14行×2列**，施設CSVは **49行×5列** です．

---

##### 5. 緯度と経度とは

地球上の場所は，緯度と経度によって表現できます．

- **緯度（latitude）**：南北方向の位置を表す．
- **経度（longitude）**：東西方向の位置を表す．

今回のCSVでは，`longitude` と `latitude` を別々の列として保存しています．

```python
spots_df[["spot_name", "longitude", "latitude"]].head()
```

例えば，札幌付近の座標は，経度がおよそ141度，緯度がおよそ43度です．

**注意：** GeoPandasで点を作るときは，`x=経度`，`y=緯度` の順番で指定します．逆にすると，別の場所に点が作られてしまいます．

---

##### 6. CSVから地図上の点を作る

通常のCSVには施設名や緯度・経度の列がありますが，地図の形を表す `geometry` 列はありません．

そこで，`gpd.points_from_xy()` を使います．

```python
spots = gpd.GeoDataFrame(
    spots_df,
    geometry=gpd.points_from_xy(
        spots_df["longitude"],
        spots_df["latitude"]
    ),
    crs="EPSG:4326"
)

spots.head()
```

主な部分の役割は次のとおりです．

| 書き方 | 意味 |
|---|---|
| `gpd.GeoDataFrame()` | 地理情報を持つ表を作成する |
| `gpd.points_from_xy()` | 経度・緯度から点を作成する |
| `geometry=` | 地図上の形を表す列を指定する |
| `crs="EPSG:4326"` | 緯度・経度の座標系を指定する |

`spots` には新しく `geometry` 列が追加されます．

```python
print(spots.shape)
print(spots.geometry.head())
```

この結果は **49行×6列** になります．

---

##### 7. CRS（座標参照系）を確認する

CRS（Coordinate Reference System）は，座標の値が地球上のどの位置を表すのかを決める情報です．

今回は，緯度・経度を表す `EPSG:4326` を使用しています．

まず，地図と施設のCRSを確認します．

```python
print("地域データ：", gdf.crs)
print("施設データ：", spots.crs)
```

地図と点を重ねたり，どの地域に属するかを判定したりするには，**両方のCRSを一致させる必要があります．**

```python
spots = spots.to_crs(gdf.crs)
```

`to_crs()` は，座標系を変換する命令です．地図と点の座標系がもともと同じであっても，このコードは実行できます．

※ `set_crs()` はCRSの情報を設定する処理であり，`to_crs()` のように座標値を変換する処理とは異なります．

---

##### 8. 北海道の地図を描く

第10回と同じように，まず地域の地図を表示します．

```python
ax = gdf.plot(
    figsize=(9, 8),
    color="lightgray",
    edgecolor="black"
)

ax.set_axis_off()
plt.title("北海道の地域区分")
plt.show()
```

`ax` は描画先のAxes（グラフの領域）を表します．

今回は次に点を重ねるので，この `ax` を活用します．

---

##### 9. 地図に施設の点を重ねる

先ほど作成した `spots` を地図上に表示します．

```python
ax = gdf.plot(
    figsize=(9, 8),
    color="lightgray",
    edgecolor="black"
)

spots.plot(
    ax=ax,
    color="red",
    markersize=20
)

ax.set_axis_off()
plt.title("北海道の架空観光施設")
plt.show()
```

- `ax=ax`：すでに描いた地図に重ねて描く．
- `color="red"`：施設の点を赤色にする．
- `markersize=20`：点の大きさを指定する．

**重要：** 地図と点を別々のグラフにしてしまうと，位置を比べられません．`ax=ax` を指定して，同じ地図上に重ねてください．

---

##### 10. 条件に一致する施設だけを表示する

pandasで学んだ条件抽出はGeoDataFrameでも使えます．

例えば，`category` が「文化施設」のデータだけを取り出します．

```python
culture = spots[
    spots["category"] == "文化施設"
]

culture.head()
```

抽出した点を地図に重ねます．

```python
ax = gdf.plot(
    figsize=(9, 8),
    color="lightgray",
    edgecolor="black"
)

culture.plot(
    ax=ax,
    color="blue",
    markersize=35
)

ax.set_axis_off()
plt.title("文化施設（架空データ）の位置")
plt.show()
```

このように，**条件抽出 → 地図への表示**という流れも行えます．

---

##### 11. `merge()` と `sjoin()` の違い

第11回では，`area_name` という共通の列を使い，`merge()` によって2つの表を結合しました．

今回は，`spots` に地域名の列がありません．そのため，列の値の一致では結合できません．

そこで **空間結合（spatial join）** を使用します．

空間結合では，「この点はどの区域の中にあるか」といった**位置関係**に基づいて情報を結び付けます．

| 結合方法 | 何を比較するか | 例 |
|---|---|---|
| `merge()` | 共通する列の値 | 地域名が同じ行を結合する |
| `sjoin()` | 地図上の位置関係 | 施設の点が入る区域を調べる |

GeoPandasでは，次のように `sjoin()` を使用します．

```python
joined = spots.sjoin(
    gdf[["area_name", "geometry"]],
    how="left",
    predicate="within"
)

joined[["spot_name", "area_name", "category"]].head()
```

- `how="left"`：元の施設データを残す．
- `predicate="within"`：施設の点が地域の区域内にあるかを判定する．
- `area_name`：判定した地域名が追加される．

これで，**緯度・経度しか持たなかった施設データに地域名を追加できました．**

---

##### 12. 空間結合の結果を確認する

まず，施設名と判定した地域名を表示します．

```python
joined[["spot_name", "area_name"]].head(10)
```

どの地域にも結び付かなかった施設がないか確認します．

```python
print("地域が判定できなかった施設数：", joined["area_name"].isna().sum())
```

地域が判定できなかった場合は，点の座標や座標系を確認します．`within` は区域の境界線上の点を「内部」と判定しないことにも注意してください．

今回は学習用の座標を使用するため，元のGeoJSONの境界の簡略化などによっては，ごく一部の点が判定できない可能性があります．その場合も `isna()` で確認できます．

---

##### 13. 地域ごとの施設数を集計する

空間結合した結果から，地域ごとの施設数を計算します．

```python
counts = (
    joined.dropna(subset=["area_name"])
    .groupby("area_name")
    .size()
    .reset_index(name="spot_count")
)

counts
```

`groupby("area_name")` は地域ごとにデータをまとめ，`size()` は各地域の行数を数えます．

ここで求めているのは**授業用の架空の施設数**であり，北海道の実際の施設数ではありません．

---

##### 14. 施設数を地図に表示する

第11回で学んだ `merge()` を使って，集計結果を地図に結合します．

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
```

`.fillna(0)` は，施設が集計されなかった地域を0件として扱うための処理です．

数値の大きさに応じて色分けします．

```python
ax = map_counts.plot(
    column="spot_count",
    cmap="YlGnBu",
    legend=True,
    edgecolor="white",
    linewidth=0.8,
    figsize=(9, 8)
)

ax.set_axis_off()
plt.title("地域別・架空施設数")
plt.show()
```

第10回の「地図を描く」と第11回の「数値で色分けする」が組み合わさり，**施設の点の位置から新しい集計結果を作れるようになりました．**

---

##### 15. 集計結果を表でも確認する

地図だけでなく，施設数を多い順に並べて確認します．

```python
counts.sort_values(
    "spot_count",
    ascending=False
)
```

地図は位置や地域的な広がりを読み取るのに向いています．一方，表は各地域の値を正確に確認するのに向いています．

**地図と表の両方で確認する**ことも大切です．

---

##### 16. 今回の重要な流れ

```text
観光施設のCSV（経度・緯度）
          ↓
GeoDataFrameに変換（点）
          ↓
北海道の地図に重ねる
          ↓
空間結合 sjoin() で地域名を取得
          ↓
groupby() で地域ごとの件数を計算
          ↓
merge() で地図に集計結果を結合
          ↓
色分けした地図を描く
```

この流れが今回の中心です．

---

##### 17. 練習問題

**使用するファイル：`hokkaido_areas.geojson`，`tourist_spots.csv`**

説明で使用した `gdf`，`spots_df`，`spots`，`joined`，`counts` などは，先ほど作成した変数をそのまま使用して構いません．ただし，課題の指定に応じて別の変数を作っても構いません．

##### 問題1　CSVを確認する

`tourist_spots.csv` を読み込み，先頭5行を表示してください．また，行数と列数を確認してください．

##### 問題2　施設の種類を確認する

`category` 列にどのような種類があるか，`unique()` を使って確認してください．

##### 問題3　点データを作成する

`gpd.points_from_xy()` を使い，経度・緯度から施設のGeoDataFrameを作成してください．変数名は `spots` とし，CRSは `EPSG:4326` としてください．

##### 問題4　地図に点を重ねる

北海道の地図を薄い灰色，施設の点を赤色で表示してください．点の大きさは `markersize=30` としてください．タイトルは「北海道の架空観光施設」としてください．

##### 問題5　特定カテゴリーの施設だけを描く

`category` が「自然体験」の施設だけを取り出し，緑色の点で地図に重ねてください．

##### 問題6　空間結合を実行する

`predicate="within"` を使用し，施設の点に `area_name` を追加してください．`joined` に保存し，施設名と地域名を表示してください．

##### 問題7　地域ごとの施設数を求める

`groupby()` と `size()` を使い，地域ごとの施設数を求めてください．列名は `spot_count` としてください．

##### 問題8　施設数で地図を塗り分ける

問題7の結果を `gdf` に結合し，`spot_count` に応じて地図を色分けしてください．`cmap="YlGnBu"` と `legend=True` を指定してください．タイトルは「地域別・架空施設数」としてください．

---

##### 余裕がある人向け（発展問題）

##### 発展問題1　特定地域に含まれる施設を確認する

空間結合後の `joined` から `area_name` が「石狩振興局」の施設だけを取り出し，施設名とカテゴリーを表示してください．

##### 発展問題2　施設数の多い地域を調べる

地域ごとの施設数を多い順に並べ，上位3地域の地域名と施設数を表示してください．

##### 発展問題3　地図を画像として保存する

地域別の施設数を色分けした地図を作成し，`plt.savefig("spot_count_map.png", dpi=150, bbox_inches="tight")` を使って画像ファイルに保存してください．保存処理は `plt.show()` より前に行ってください．

---

##### 18. まとめ

第10回では，GeoJSONを読み込んで地図を表示しました．

第11回では，CSVの統計値を地図と結合し，地域を色分けしました．

今回の第12回では，**CSVの緯度・経度から点を作成し，空間結合を使って地域別の数を集計**しました．

今回の重要な命令は，次のとおりです．

| 命令 | 用途 |
|---|---|
| `pd.read_csv()` | CSVの読み込み |
| `gpd.read_file()` | GeoJSONの読み込み |
| `gpd.points_from_xy()` | 経度・緯度から点を作成 |
| `gpd.GeoDataFrame()` | 地図上の形を持つ表を作成 |
| `to_crs()` | 座標系を変換 |
| `plot(ax=ax)` | 同じ地図に重ね描き |
| `sjoin()` | 位置関係でデータを結合 |
| `groupby()`・`size()` | 地域ごとの件数を集計 |
| `merge()` | 地図と集計結果を列名で結合 |

**3回のGeoPandas学習のゴールは，地図を表示するだけでなく，位置情報を利用してデータを分析できるようになることです．**
