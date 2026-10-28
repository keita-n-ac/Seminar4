### ゼミナールⅣ 第11回
#### GeoPandas入門2
##### 北海道の統計データを地図の色で表そう


##### 1. 今回の目標
第10回では，`hokkaido_areas.geojson` を読み込んで北海道の地図を表示し，色や境界線を変更しました．
今回は，前回の地図データに **CSVファイルの統計データを結合**して，数値の大きさを色の濃淡で表します．
今回の目標は次の5つです．

- GeoJSONとCSVの役割を説明できる
- 共通する地域名を使ってデータを結合できる
- 地図上の地域を数値の大きさで色分けできる
- 凡例を表示し，地図の色の意味を読み取れる
- 合計の大きさと人口当たりの指標を区別できる

**今回のゴール：北海道の14振興局・総合振興局を，人口や来訪者数に応じて色分けした地図を描けるようになること．**

※ 今回は地図上の位置関係による結合（空間結合）を扱いません．第12回に学習します．

---

##### 2. 使用するファイル

今回は，次の2つのファイルを使用します．

| ファイル名 | 内容 | 主な列 |
|---|---|---|
| `hokkaido_areas.geojson` | 第10回で使用した北海道14地域の地図 | `area_name`, `geometry` |
| `area_stats.csv` | 14地域の授業用統計データ | `area_name`, `population`, `visitors`, `spending` |

**重要：** `area_stats.csv` の人口・来訪者数・消費金額は，授業の練習のために作成した**架空の数値**です．実際の統計情報や予測値ではありません．

統計CSVの列は次のとおりです．

| 列名 | 内容 | 単位 |
|---|---|---|
| `area_name` | 振興局・総合振興局の名称 | ― |
| `population` | 人口（架空） | 人 |
| `visitors` | 年間延べ来訪回数（架空） | 回 |
| `spending` | 来訪1回当たりの平均消費金額（架空） | 円／回 |

地域名を示す `area_name` は，**2つのファイルに共通する列**です．

GeoJSONには地図の形があり，CSVには人口や来訪回数などの数値があります．これらを組み合わせると，数値に応じた地図を作成できます．

---

##### 3. Google Colabの準備

Google Colabで次のセルを実行します．

```python
!pip -q install geopandas japanize-matplotlib
```

続けてライブラリを読み込みます．

```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt
import japanize_matplotlib
```

`pd` はpandas，`gpd` はGeoPandas，`plt` はmatplotlibを表します．

教員から配布された **`hokkaido_areas.geojson` と `area_stats.csv` の2ファイル**をColabにアップロードしてください．

左側のフォルダーアイコンからアップロードするほか，次のコードも使用できます．

```python
from google.colab import files
files.upload()
```

ファイルを読み込みます．

```python
gdf = gpd.read_file("hokkaido_areas.geojson")
stats = pd.read_csv("area_stats.csv")
```

`gdf` は地図の形を持つGeoDataFrame，`stats` は数値を保存したDataFrameです．

---

##### 4. 2つのデータを確認する

地図データを確認します．

```python
gdf.head()
```

統計データも確認します．

```python
stats.head()
```

行数と列数を確認してみましょう．

```python
print("地図：", gdf.shape)
print("統計：", stats.shape)
```

この授業用データでは，地図が **14行×2列**，統計が **14行×4列** です．

列名も確認します．

```python
print(gdf.columns)
print(stats.columns)
```

両方に `area_name` が含まれていることを確認してください．

---

##### 5. なぜ2つのファイルを結合するのか

地図には，区域の形が保存されています．一方，統計CSVには人口や来訪回数が保存されています．

例えば，次のような2つの表があるとします．

**地図データ（一部）**

| area_name | geometry |
|---|---|
| 石狩振興局 | 区域の形 |
| 渡島総合振興局 | 区域の形 |

**統計データ（一部）**

| area_name | population | visitors |
|---|---:|---:|
| 石狩振興局 | 2380000 | 5300000 |
| 渡島総合振興局 | 355000 | 1970000 |

`area_name` を基準に結合すると，各地域について **地図の形と統計値を1つの表にまとめられます．**

ここで使用している数値は架空です．

---

##### 6. `merge()` でデータを結合する（結合：15分）

第8回で学習した `merge()` を使います．

```python
merged = gdf.merge(
    stats,
    on="area_name",
    how="left"
)

merged.head()
```

`on="area_name"` は，2つの表の `area_name` が一致する行を結び付けるという意味です．

`how="left"` は，**左側の `gdf` にある地域を残す**結合方法です．

結合後の `merged` は，地図の `geometry` 列を持つGeoDataFrameなので，そのまま `plot()` で地図を描けます．

今回のデータでは，`merged.shape` が **`(14, 5)`** になります．

```python
merged.shape
```

結合前後の列を比較してください．

```python
merged.columns
```

---

##### 7. 正しく結合できたか確認する

結合後に，人口が不明な地域がないか確認します．

```python
merged["population"].isna().sum()
```

正しく結合できていれば，結果は `0` になります．

```python
merged[["area_name", "population", "visitors"]]
```

のように，地域名と統計値をまとめて確認できます．

もし欠損値がある場合は，GeoJSONとCSVの地域名が一致しているかを確認してください．例えば，末尾に余分な空白がある場合や，「振興局」と「総合振興局」を間違えた場合は結合されません．

---

##### 8. 数値によって地図を塗り分ける（階級区分図：20分）

第10回では，地図全体を同じ色で塗りました．

```python
gdf.plot(
    color="lightblue",
    edgecolor="black"
)
plt.show()
```

今回は，**来訪回数の大きさによって色を変えて**みます．

```python
merged.plot(
    column="visitors",
    cmap="YlOrRd",
    legend=True,
    edgecolor="white",
    linewidth=0.8
)

plt.show()
```

- `column="visitors"`：色分けする数値の列
- `cmap="YlOrRd"`：黄色から赤系のカラーマップ
- `legend=True`：値と色の関係を示す凡例を表示
- `edgecolor="white"`：地域の境界線を白色にする

このように，**地域別の数値を色の濃淡で表す地図**を階級区分図（コロプレス図）と呼びます．今回の設定では，連続的な色の濃淡で値を表しています．

---

##### 9. `cmap` を変更してみる

地図の色は `cmap` で変更できます．

```python
merged.plot(
    column="visitors",
    cmap="Blues",
    legend=True,
    edgecolor="white"
)

plt.show()
```

例えば，次のようなカラーマップもあります．

| カラーマップ | 色の傾向 |
|---|---|
| `Blues` | 白から青系 |
| `Greens` | 白から緑系 |
| `YlOrRd` | 黄色から赤系 |
| `Purples` | 白から紫系 |

原則として，**数値が小さい地域は薄く，大きい地域は濃く**表示されます．

---

##### 10. 地図の大きさ・タイトル・目盛りを設定する

第10回で学習したmatplotlibと組み合わせます．

```python
fig, ax = plt.subplots(figsize=(10, 8))

merged.plot(
    ax=ax,
    column="visitors",
    cmap="YlOrRd",
    legend=True,
    edgecolor="white",
    linewidth=0.8
)

ax.set_title("北海道：地域別の年間延べ来訪回数（架空データ）")
ax.set_axis_off()

plt.show()
```

第10回と同様に `figsize` は図の大きさ，`ax.set_title()` はタイトル，`ax.set_axis_off()` は軸や目盛りの非表示です．

---

##### 11. 別の数値でも色分けしてみる

人口で色分けする場合は，`column` を変更するだけです．

```python
fig, ax = plt.subplots(figsize=(10, 8))

merged.plot(
    ax=ax,
    column="population",
    cmap="Blues",
    legend=True,
    edgecolor="white"
)

ax.set_title("北海道：地域別人口（架空データ）")
ax.set_axis_off()

plt.show()
```

地図の形は同じでも，**何の数値を使うかによって見え方が変わります．**

---

##### 12. 地図の色と実際の数値を確認する

来訪回数が大きい地域を確かめます．

```python
merged[["area_name", "visitors"]].sort_values(
    "visitors",
    ascending=False
).head()
```

数値の大きい地域が，地図でも濃い色になっているか確認してください．

**注意：** この地図が示すのはあくまで **地域ごとの来訪回数の大きさ**であり，「住民1人当たりの来訪回数」や「来訪者の割合」ではありません．

---

##### 13. 人口当たりの値を作る

人口が大きい地域では，来訪回数の総量も大きくなりやすいことがあります．

そこで，「人口1万人当たりの年間延べ来訪回数」という新しい数値を作ってみます．

計算式は次のとおりです．

**人口1万人当たりの延べ来訪回数 ＝ 年間延べ来訪回数 ÷ 人口 × 10000**

```python
merged["visitors_per_10k"] = (
    merged["visitors"] / merged["population"] * 10000
)

merged[["area_name", "visitors_per_10k"]].head()
```

例えば，年間延べ来訪回数が200000回，人口が100000人の地域の場合，人口1万人当たり20000回となります．

この指標は地域間比較のための計算例であり，**住民の訪問回数や観光客の割合を表しているわけではありません．**

---

##### 14. 人口当たりの値を地図で表示する

```python
fig, ax = plt.subplots(figsize=(10, 8))

merged.plot(
    ax=ax,
    column="visitors_per_10k",
    cmap="Greens",
    legend=True,
    edgecolor="white"
)

ax.set_title("北海道：人口1万人当たりの延べ来訪回数（架空データ）")
ax.set_axis_off()

plt.show()
```

「来訪回数そのもの」の地図と「人口当たりの来訪回数」の地図を比較してください．

たとえば人口の少ない地域でも，来訪回数を人口で割ると比較的大きな値になることがあります．

また，人口で割った数値が大きいからといって，「住民の観光への関心が高い」とは結論付けられません．

---

##### 15. グラフを読み取るときの注意

色の濃い地域が多く見えるだけで結論を出さず，次の点を確認してください．

1. 地図は何を表しているか（人口，来訪回数，人口当たりの値など）．
2. **単位**は何か（人，回，円／回など）．
3. **凡例**から数値と色の対応を確認できるか．
4. 数値は実測値か，授業用の架空データか．
5. 合計の数値か，平均・比率などの値か．

地図の色が変わっても，もとの地図の面積や区域が変化したわけではありません．

---

##### 16. 練習問題

ここからは，**`hokkaido_areas.geojson` と `area_stats.csv`** を使用して自分でプログラムを作成します．

問題1〜8が基本問題です．終わった人は発展問題に進んでください．

##### 問題1　2つのファイルを読み込む

GeoJSONファイルを `gdf`，CSVファイルを `stats` という変数に読み込んでください．

さらに，それぞれの先頭5行を表示してください．

---

##### 問題2　行数・列数と列名を確認する

`gdf` と `stats` の行数・列数，列名をそれぞれ表示してください．

`gdf` が `(14, 2)`，`stats` が `(14, 4)` となることを確認してください．

---

##### 問題3　2つのデータを結合する

`area_name` を基準に `gdf` と `stats` を結合し，結果を `merged` に保存してください．

`how="left"` を指定し，結合結果が `(14, 5)` になることを確認してください．

---

##### 問題4　来訪回数に応じて地図を色分けする

`merged.plot()` を用いて，`visitors` の数値で地図を色分けしてください．

次の条件を満たしてください．

- カラーマップ：`YlOrRd`
- 凡例：表示する
- 境界線：白
- タイトル：「地域別来訪回数（架空データ）」

---

##### 問題5　カラーマップを変更する

問題4と同じ来訪回数の地図を，`cmap="Blues"` で表示してください．

色が変わっても，表示される数値が同じであることを確認してください．

---

##### 問題6　人口を地図で比較する

`population` を使って，地域別人口の地図を作成してください．

- カラーマップ：`Greens`
- 凡例：表示する
- タイトル：「地域別人口（架空データ）」

---

##### 問題7　新しい列を計算する

次の式を使い，人口1万人当たりの年間延べ来訪回数を求めてください．

**`visitors / population * 10000`**

結果を `visitors_per_10k` という列に保存し，地域名と計算結果を表示してください．

---

##### 問題8　人口当たりの値を地図にする

`visitors_per_10k` の値を使い，地域ごとに色分けした地図を作成してください．

- カラーマップ：`Purples`
- 凡例：表示する
- タイトル：「人口1万人当たりの来訪回数（架空データ）」

問題4の地図と比べ，色の濃い地域が同じかどうか考えてください．

---

#### 余裕がある人向け

##### 発展問題1　来訪回数上位3地域

`sort_values()` と `head()` を使い，来訪回数の多い順に3地域を表示してください．

---

##### 発展問題2　平均消費金額の地図

`spending` の値を使って地図を色分けしてください．

- カラーマップ：`Oranges`
- 凡例：表示する
- タイトル：「来訪1回当たり平均消費金額（架空データ）」

---

##### 発展問題3　2つの地図を並べて比べる

`plt.subplots(1, 2, figsize=(14, 6))` を使い，左に `visitors`，右に `visitors_per_10k` の地図を表示してください．

それぞれタイトルと凡例を付けてください．

---

#### 17. 今日のまとめ
今回学習した主な処理は次のとおりです．

```python
# 地図と統計を読み込む
gdf = gpd.read_file("hokkaido_areas.geojson")
stats = pd.read_csv("area_stats.csv")

# 名前で結合する
merged = gdf.merge(stats, on="area_name", how="left")

# 数値によって地域を色分けする
merged.plot(column="visitors", cmap="YlOrRd", legend=True)
plt.show()
```

**第10回：地図を描けた．第11回：統計データを地図の色で表せた．**

次回の第12回では，緯度・経度から施設の位置を地図に重ね，**位置関係に基づく空間結合**を学習します．

**地図データの出典：** 国土交通省「国土数値情報（行政区域データ）」を軽量化した [ricewin/simplify-japan-geojson](https://github.com/ricewin/simplify-japan-geojson) に基づく，第10回配布用の14地域GeoJSONを利用．

**統計CSVの出典：** 授業用に新規作成した架空データであり，実際の統計値ではありません．
