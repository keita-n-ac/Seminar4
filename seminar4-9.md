### ゼミナールⅣ 9回目
#### pandas・matplotlib・seabornによるデータ可視化

##### 1. 今回の目標
これまで，Pythonを使ったグラフ作成のために `matplotlib` を学習し，
表形式のデータを扱うために `pandas` を学習しました．
今回は，これらを組み合わせて，
**データを読み込む → 必要なデータを取り出す → 集計する → グラフにする**
というデータ分析の基本的な流れを学習します．

さらに，データの可視化に便利な
`seaborn`
というライブラリも使用します．

今回の目標は次の3つです．

- pandasで読み込んだデータをグラフにする
- matplotlibとseabornの特徴を理解する
- データに応じて適切なグラフを選択する

---

##### 2. 3つのライブラリの役割

今回使用するライブラリには，それぞれ役割があります．

| ライブラリ | 主な役割 |
|---|---|
| pandas | データの読み込み・整理・抽出・集計 |
| matplotlib | グラフの作成 |
| seaborn | データ分析向けのグラフを簡単に作成 |

例えば，

```text
CSVファイル
    ↓
pandas
    ↓
データの抽出・集計
    ↓
matplotlib / seaborn
    ↓
グラフ
```

という流れになります．

---

##### 3. ライブラリの準備

まず，必要なライブラリを読み込みます．

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import japanize_matplotlib
```

それぞれ，

```python
pd
```

はpandas，

```python
plt
```

はmatplotlib，

```python
sns
```

はseabornを表します．

`japanize_matplotlib` は，グラフに日本語を表示するために使用します．

Google Colabでインストールされていない場合は，

```python
!pip install japanize-matplotlib
```

を最初に実行します．

---

##### 4. CSVファイルを読み込む

今回は，

```text
tourism.csv
```

という観光データを使用するとします．

CSVファイルには，例えば次のような項目が含まれているとします．

| 列 | 内容 |
|---|---|
| city | 都市 |
| region | 地域 |
| visitors | 観光客数 |
| satisfaction | 満足度 |
| spending | 消費金額 |
| stay_days | 宿泊日数 |
| season | 季節 |

pandasでは，

```python
df = pd.read_csv("tourism.csv")
```

でCSVファイルを読み込むことができます．

---

##### 5. データの確認

データを読み込んだら，いきなりグラフを作成するのではなく，まず内容を確認します．

```python
df.head()
```

`head()` は，最初の5行を表示します．

---

データの行数と列数を確認します．

```python
df.shape
```

例えば，

```text
(100, 7)
```

と表示された場合は，

- 100行
- 7列

のデータという意味です．

---

列の名前も確認できます．

```python
df.columns
```

---

データ型を確認する場合は，

```python
df.dtypes
```

を使用します．

---

##### 6. 基本的な統計量を確認する

数値データの特徴を確認する場合には，

```python
df.describe()
```

を使用できます．

例えば，

- 平均値
- 標準偏差
- 最小値
- 最大値
- 四分位数

などを確認できます．

グラフを作る前に，

**どのようなデータなのかを数値で確認する**

ことも重要です．

---

# 7. 1つの列を取り出す

例えば，観光客数だけを取り出します．

```python
df["visitors"]
```

満足度なら，

```python
df["satisfaction"]
```

です．

pandasの列は，そのままmatplotlibに渡すことができます．

---

# 8. pandasとmatplotlib

以前のmatplotlibでは，

```python
city = ["札幌", "函館", "旭川", "小樽"]
visitors = [450, 280, 210, 190]

plt.bar(city, visitors)
plt.show()
```

のように，リストを準備していました．

pandasを使用すると，CSVから読み込んだ列を直接使用できます．

```python
plt.bar(
    df["city"],
    df["visitors"]
)

plt.title("都市別観光客数")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

つまり，

```python
df["city"]
```

が横軸，

```python
df["visitors"]
```

が縦軸になります．

---

# 9. pandasだけでもグラフを作れる

pandasには簡単なグラフ作成機能があります．

```python
df.plot(
    x="city",
    y="visitors",
    kind="bar"
)

plt.title("都市別観光客数")

plt.show()
```

`kind` でグラフの種類を指定します．

例えば，

```text
line
bar
barh
hist
box
scatter
```

などがあります．

---

# 10. pandasのグラフとmatplotlib

pandasのグラフ作成機能は，内部でmatplotlibを使用しています．

そのため，

```python
df.plot(
    x="city",
    y="visitors",
    kind="bar"
)

plt.title("都市別観光客数")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

のように，

**pandasでグラフを作成して，matplotlibでタイトルなどを追加する**

ことができます．

---

# 11. pandasとmatplotlibの使い分け

簡単にグラフを確認したい場合には，

```python
df.plot()
```

が便利です．

細かくグラフを設定したい場合には，

```python
plt.bar()
plt.plot()
plt.scatter()
```

などmatplotlibを直接使用します．

例えば，

**データをすぐ確認したい**

場合にはpandas，

**発表資料などのグラフを細かく調整したい**

場合にはmatplotlib，

という使い方ができます．

---

# 12. 条件を指定してからグラフを作る

pandasでは，条件に一致するデータを簡単に取り出すことができます．

例えば，観光客数が200以上のデータを取り出します．

```python
selected = df[
    df["visitors"] >= 200
]
```

内容を確認します．

```python
selected
```

---

このデータだけを棒グラフにします．

```python
plt.bar(
    selected["city"],
    selected["visitors"]
)

plt.title("観光客数200以上の都市")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

以前は `for` 文と `if` 文を使用して，

```python
selected_city = []
selected_visitors = []

for i in range(len(cities)):

    if visitors[i] >= 200:
        selected_city.append(cities[i])
        selected_visitors.append(visitors[i])
```

のような処理を行っていました．

pandasを使用すると，

```python
df[df["visitors"] >= 200]
```

だけで条件に一致するデータを取り出すことができます．

---

# 13. 並べ替えてからグラフを作る

観光客数が多い順に並べてみます．

```python
sorted_df = df.sort_values(
    "visitors",
    ascending=False
)

sorted_df.head()
```

この結果を使ってグラフを作成できます．

```python
plt.bar(
    sorted_df["city"],
    sorted_df["visitors"]
)

plt.title("都市別観光客数")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

棒グラフでは，値の大きい順に並べることで比較しやすくなることがあります．

---

# 14. groupbyとグラフ

pandasでは，カテゴリーごとにデータを集計できます．

例えば，地域ごとの観光客数の平均を計算します．

```python
region_mean = df.groupby(
    "region"
)["visitors"].mean()

region_mean
```

結果をグラフにします．

```python
region_mean.plot(
    kind="bar"
)

plt.title("地域別平均観光客数")
plt.xlabel("地域")
plt.ylabel("平均観光客数")

plt.show()
```

このように，

**pandasで集計 → matplotlibで可視化**

という流れは，データ分析でよく使用します．

---

# 15. seabornとは

`seaborn` は，データの可視化を行うためのPythonライブラリです．

matplotlibを基礎として作られており，特にpandasのDataFrameと組み合わせて使用しやすくなっています．

例えばmatplotlibでは，

```python
plt.scatter(
    df["visitors"],
    df["satisfaction"]
)
```

と書きます．

seabornでは，

```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction"
)
```

と書くことができます．

---

# 16. seabornの基本形

seabornでは，

```python
sns.グラフ名(
    data=データ,
    x="横軸の列",
    y="縦軸の列"
)
```

という形をよく使用します．

例えば，

```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction"
)
```

です．

この書き方では，

```python
data=df
```

で使用するDataFrameを指定し，

```python
x="visitors"
```

で横軸，

```python
y="satisfaction"
```

で縦軸を指定します．

---

# 17. seabornで散布図

観光客数と満足度の関係を調べてみます．

```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction"
)

plt.title("観光客数と満足度")

plt.show()
```

seabornで作成したグラフにも，

```python
plt.title()
```

などmatplotlibの命令を使用できます．

---

# 18. hueでカテゴリーを分ける

seabornの便利な機能の1つが，

```python
hue
```

です．

例えば，地域ごとに点を分けて表示します．

```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction",
    hue="region"
)

plt.title("観光客数と満足度")

plt.show()
```

`hue="region"` を指定すると，地域によって点の表示が分かれます．

これによって，

**2つの数値の関係だけでなく，カテゴリーの違いも同時に確認できます．**

---

# 19. matplotlibとの違い

matplotlibでも同じようなグラフを作成できます．

しかし，地域ごとに表示を分けようとすると，それぞれの地域のデータを取り出してからグラフを作成する必要があります．

seabornでは，

```python
hue="region"
```

と指定するだけでカテゴリーごとに分けることができます．

このようにseabornは，

**表形式のデータをカテゴリーごとに比較する**

場合に便利です．

---

# 20. seabornで棒グラフ

地域ごとの消費金額を比較してみます．

```python
sns.barplot(
    data=df,
    x="region",
    y="spending",
    errorbar=None
)

plt.title("地域別平均消費金額")
plt.xlabel("地域")
plt.ylabel("消費金額")

plt.show()
```

ここで注意する点があります．

`seaborn` の `barplot()` は，同じカテゴリーのデータが複数存在する場合，

**平均値**

を計算して表示します．

つまり，

```python
sns.barplot(
    data=df,
    x="region",
    y="spending"
)
```

では，地域ごとの平均消費金額が表示されます．

---

# 21. pandasで計算してから描く方法との比較

pandasで同じ処理をすると，

```python
region_spending = df.groupby(
    "region"
)["spending"].mean()
```

として，

```python
region_spending.plot(
    kind="bar"
)

plt.show()
```

となります．

一方，seabornなら，

```python
sns.barplot(
    data=df,
    x="region",
    y="spending",
    errorbar=None
)

plt.show()
```

と書くことができます．

どちらも結果を確認するために使用できます．

---

# 22. seabornでヒストグラム

観光客の消費金額が，どの範囲に多いのか確認してみます．

```python
sns.histplot(
    data=df,
    x="spending"
)

plt.title("消費金額の分布")
plt.xlabel("消費金額")
plt.ylabel("件数")

plt.show()
```

matplotlibでは，

```python
plt.hist(
    df["spending"]
)
```

でした．

seabornでは，

```python
sns.histplot(
    data=df,
    x="spending"
)
```

となります．

---

# 23. ヒストグラムをカテゴリーで分ける

地域ごとに消費金額の分布を比較してみます．

```python
sns.histplot(
    data=df,
    x="spending",
    hue="region"
)

plt.title("地域別消費金額の分布")

plt.show()
```

これによって，

**地域によって消費金額の分布に違いがあるか**

を確認できます．

---

# 24. 箱ひげ図

カテゴリーごとの数値の分布を比較するときには，箱ひげ図も便利です．

例えば，地域ごとの満足度を比較します．

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
```

箱ひげ図では，

- 中央値
- データのばらつき
- 外れ値

などを比較できます．

---

# 25. 平均値だけを見る場合との違い

例えば地域ごとの平均満足度を計算すると，

```python
df.groupby(
    "region"
)["satisfaction"].mean()
```

となります．

しかし，平均値だけでは，

**データがどの程度ばらついているか**

は分かりません．

そのため，

平均値の比較

だけでなく，

```python
sns.boxplot()
```

を使用して分布を見ることも重要です．

---

# 26. seabornで折れ線グラフ

時間の変化を見る場合には，

```python
sns.lineplot()
```

を使用できます．

例えば，月別の観光客数を表示します．

```python
sns.lineplot(
    data=df,
    x="month",
    y="visitors"
)

plt.title("月別観光客数")
plt.xlabel("月")
plt.ylabel("観光客数")

plt.show()
```

---

カテゴリーごとに分ける場合には，

```python
sns.lineplot(
    data=df,
    x="month",
    y="visitors",
    hue="region"
)

plt.title("地域別観光客数の推移")

plt.show()
```

とすることもできます．

---

# 27. どのライブラリを使えばよいか

同じグラフでも，複数の方法で作成できます．

例えば散布図なら，

### matplotlib

```python
plt.scatter(
    df["visitors"],
    df["satisfaction"]
)
```

### pandas

```python
df.plot(
    kind="scatter",
    x="visitors",
    y="satisfaction"
)
```

### seaborn

```python
sns.scatterplot(
    data=df,
    x="visitors",
    y="satisfaction"
)
```

となります．

---

# 28. 3つの方法の特徴

| 方法 | 特徴 |
|---|---|
| matplotlib | 自由度が高く，細かな設定ができる |
| pandas | データを簡単にグラフで確認できる |
| seaborn | DataFrameを使った比較や分析に便利 |

必ず1つだけを使用する必要はありません．

実際には，

**pandasでデータを処理し，seabornでグラフを作成し，matplotlibでタイトルなどを調整する**

という使い方もよく行います．

---

# 29. 実際のデータ分析の流れ

例えば，

**「地域によって観光客の満足度に違いがあるか」**

を調べたいとします．

まずCSVを読み込みます．

```python
df = pd.read_csv(
    "tourism.csv"
)
```

データを確認します．

```python
df.head()
```

---

地域ごとの平均満足度を確認します．

```python
df.groupby(
    "region"
)["satisfaction"].mean()
```

---

箱ひげ図を作成します．

```python
sns.boxplot(
    data=df,
    x="region",
    y="satisfaction"
)

plt.title("地域別満足度")

plt.show()
```

---

ここで，

- 平均値に違いがあるか
- データのばらつきが大きいか
- 特に高い値や低い値があるか

などを確認します．

---

# 30. もう1つの分析例

次に，

**「宿泊日数が長い人ほど消費金額が高いのか」**

を調べてみます．

まず必要な列を確認します．

```python
df[
    ["stay_days", "spending"]
].head()
```

---

散布図を作成します．

```python
sns.scatterplot(
    data=df,
    x="stay_days",
    y="spending"
)

plt.title("宿泊日数と消費金額")
plt.xlabel("宿泊日数")
plt.ylabel("消費金額")

plt.show()
```

点が右上がりに並んでいれば，

**宿泊日数が長いほど消費金額も高くなる傾向**

がある可能性があります．

ただし，

**グラフだけで原因と結果を決めることはできません．**

---

# 31. 条件を絞って分析する

例えば，札幌のデータだけを分析することもできます．

```python
sapporo = df[
    df["city"] == "札幌"
]
```

内容を確認します．

```python
sapporo.head()
```

散布図を作成します．

```python
sns.scatterplot(
    data=sapporo,
    x="stay_days",
    y="spending"
)

plt.title("札幌：宿泊日数と消費金額")

plt.show()
```

pandasで必要なデータを取り出してから，seabornで可視化することができます．

---

# 32. 複数の条件を指定する

例えば，

- 札幌
- 満足度4以上

のデータを取り出します．

```python
selected = df[
    (df["city"] == "札幌")
    &
    (df["satisfaction"] >= 4)
]
```

結果を確認します．

```python
selected
```

この結果についてグラフを作ることもできます．

---

# 33. データを集計してから可視化する

例えば，地域別の観光客数の合計を計算します．

```python
region_total = df.groupby(
    "region"
)["visitors"].sum()

region_total
```

棒グラフにします．

```python
region_total.plot(
    kind="bar"
)

plt.title("地域別観光客数")
plt.xlabel("地域")
plt.ylabel("観光客数")

plt.show()
```

---

# 34. 「集計」と「そのまま表示」の違い

グラフを作るときには，

**何を1つの値として表示しているのか**

を考える必要があります．

例えば，

```python
df.groupby("region")["visitors"].sum()
```

なら，

**地域ごとの合計**

です．

一方，

```python
df.groupby("region")["visitors"].mean()
```

なら，

**地域ごとの平均**

です．

同じ棒グラフであっても，表示する値によって意味が変わります．

---

# 35. グラフを作る前に考えること

グラフを作成するときには，最初に，

**何を知りたいのか**

を考えます．

例えば，

### 時間による変化を知りたい

→ 折れ線グラフ

### 項目ごとの大きさを比較したい

→ 棒グラフ

### 数値の分布を知りたい

→ ヒストグラム

### グループごとの分布を比較したい

→ 箱ひげ図

### 2つの数値の関係を調べたい

→ 散布図

となります．

---

# 36. グラフの使い分け

| 知りたいこと | グラフ |
|---|---|
| 時間による変化 | 折れ線グラフ |
| 項目の比較 | 棒グラフ |
| 数値の分布 | ヒストグラム |
| グループごとの分布 | 箱ひげ図 |
| 2つの数値の関係 | 散布図 |
| 割合 | 円グラフ・帯グラフ |

seabornを使用する場合でも，グラフそのものの意味はmatplotlibで学習したものと同じです．

---

# 37. pandas・matplotlib・seabornの関係

今回の重要なポイントは，

**3つを別々に覚えることではありません．**

それぞれの役割を組み合わせます．

```text
pandas
データを読み込む
        ↓
pandas
データを確認・抽出・集計する
        ↓
matplotlib / seaborn
グラフを作成する
        ↓
グラフを読み取る
```

という流れになります．

---

# 38. まとめ

今回使用した主な処理をまとめます．

### CSVを読み込む

```python
df = pd.read_csv(
    "tourism.csv"
)
```

### 条件で絞り込む

```python
df[
    df["visitors"] >= 200
]
```

### 集計する

```python
df.groupby(
    "region"
)["visitors"].mean()
```

### pandasでグラフ

```python
df.plot()
```

### matplotlib

```python
plt.bar()
plt.plot()
plt.scatter()
plt.hist()
```

### seaborn

```python
sns.barplot()
sns.lineplot()
sns.scatterplot()
sns.histplot()
sns.boxplot()
```

---

# 39. 最も重要なこと

データ分析では，

**とりあえずグラフを作る**

のではなく，

1. 何を知りたいのか考える
2. 必要なデータを取り出す
3. 必要に応じてデータを集計する
4. 目的に合ったグラフを選ぶ
5. グラフから分かることを考える

という流れが重要です．

pandas，matplotlib，seabornは，

**データから特徴や傾向を見つけるための道具**

として使用します．
