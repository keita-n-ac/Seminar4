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
tourism-9.csv
```

という観光データを使用します．

このCSVファイルには，北海道の観光に関する架空のデータ100件が保存されています．

列は次の8つです．

| 列 | 内容 |
|---|---|
| city | 都市名 |
| region | 地域 |
| visitors | 来訪者数 |
| satisfaction | 満足度 |
| spending | 1人あたりの消費金額 |
| stay_days | 宿泊日数 |
| season | 季節 |
| month | 月 |

同じ都市が複数行に登場します．そのため，都市ごとのデータを比較する場合には，必要に応じて平均や合計を求めてからグラフにします．

pandasでは，

```python
df = pd.read_csv("tourism-9.csv")
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
(100, 8)
```

と表示された場合は，

- 100行
- 8列

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

##### 7. 1つの列を取り出す

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

##### 8. pandasとmatplotlib

以前のmatplotlibでは，

```python
city = ["札幌", "函館", "旭川", "小樽"]
visitors = [450, 280, 210, 190]

plt.bar(city, visitors)
plt.show()
```

のように，リストを準備していました．

pandasを使用すると，CSVファイルから読み込んだ列をグラフに使用できます．

ただし，今回の `tourism-9.csv` には，同じ都市が複数回登場します．

そのため，

```python
plt.bar(
    df["city"],
    df["visitors"]
)
```

とすると，同じ都市の位置に複数の棒が重なってしまいます．

そこで，都市ごとの平均来訪者数を求めてから棒グラフを作成します．

まず，`groupby()` を使って都市ごとの平均来訪者数を計算します．

```python
city_mean = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

city_mean
```

これによって，都市ごとの平均来訪者数をまとめたDataFrameが作成されます．

次に，このデータを使って棒グラフを作成します．

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

この場合，

```python
city_mean["city"]
```

が横軸，

```python
city_mean["visitors"]
```

が縦軸になります．

このように，同じ項目が複数行に存在する場合には，**必要に応じて集計してからグラフを作成することが重要です．**

---

##### 9. pandasだけでもグラフを作れる

pandasには簡単なグラフ作成機能があります．

先ほど作成した `city_mean` を使って，棒グラフを作成してみましょう．

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

これによって，都市ごとの平均来訪者数を棒グラフで表示できます．

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

今回のように項目ごとの値を比較する場合には，

```python
kind="bar"
```

を使用します．

また，

```python
legend=False
```

は，凡例を表示しないという意味です．

---

##### 10. pandasのグラフとmatplotlib

pandasのグラフ作成機能は，内部でmatplotlibを使用しています．

そのため，pandasでグラフを作成した後に，matplotlibでタイトルや軸の名前を設定できます．

例えば，

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

とします．

このプログラムでは，

```python
city_mean.plot()
```

によってグラフを作成し，

```python
plt.title()
plt.xlabel()
plt.ylabel()
```

によってタイトルや軸の名前を設定しています．

このように，**pandasでグラフを作成して，matplotlibで表示を調整する**ことができます．

---

##### 11. pandasとmatplotlibの使い分け

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

##### 12. 条件を指定してからグラフを作る

pandasでは，条件に一致するデータを簡単に取り出すことができます．

例えば，来訪者数が200人以上のデータを取り出します．

```python
selected = df[
    df["visitors"] >= 200
]
```

内容を確認します．

```python
selected
```

次に，取り出したデータについて，都市ごとの平均来訪者数を求めます．

```python
selected_mean = (
    selected.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

selected_mean
```

この処理では，来訪者数が200人以上のデータだけを使って，都市ごとの平均を計算しています．

最後に棒グラフを作成します．

```python
plt.bar(
    selected_mean["city"],
    selected_mean["visitors"]
)

plt.title("来訪者数200人以上のデータにおける都市別平均")
plt.xlabel("都市")
plt.ylabel("平均来訪者数")

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

さらに，`groupby()` を組み合わせることで，条件に一致するデータだけを集計してグラフにできます．

ただし，**条件を指定する前に平均を求める場合と，条件を指定した後に平均を求める場合では，結果が異なることがあります．**

---

##### 13. 並べ替えてからグラフを作る

次は，都市ごとの平均来訪者数を多い順に並べてみます．

まず，都市ごとの平均を求めます．

```python
city_mean = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)
```

次に，平均来訪者数の多い順に並べます．

```python
sorted_df = city_mean.sort_values(
    "visitors",
    ascending=False
)

sorted_df
```

この結果を使ってグラフを作成します．

```python
plt.bar(
    sorted_df["city"],
    sorted_df["visitors"]
)

plt.title("都市別平均来訪者数")
plt.xlabel("都市")
plt.ylabel("平均来訪者数")

plt.show()
```

これによって，平均来訪者数が多い都市から順に棒グラフを表示できます．

棒グラフでは，**値の大きい順に並べることで，項目同士を比較しやすくなることがあります．**

---

##### 14. groupbyとグラフ

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

##### 15. seabornとは

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

##### 16. seabornの基本形

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

##### 17. seabornで散布図

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

##### 18. hueでカテゴリーを分ける

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

##### 19. matplotlibとの違い

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

##### 20. seabornで棒グラフ

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

##### 21. pandasで計算してから描く方法との比較

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

##### 22. seabornでヒストグラム

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

##### 23. ヒストグラムをカテゴリーで分ける

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

##### 24. 箱ひげ図

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

##### 25. 平均値だけを見る場合との違い

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

##### 26. seabornで折れ線グラフ

時間の変化を見る場合には，

```python
sns.lineplot()
```

を使用できます．

例えば，月別の平均来訪者数を表示します．

今回の `tourism-9.csv` には，同じ月のデータが複数含まれています．

`seaborn` の `lineplot()` は，同じ横軸の値に複数のデータがある場合，既定では平均値を計算して折れ線グラフにします．

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
```

このグラフでは，各月の平均来訪者数を確認できます．

次に，地域ごとに分けてみます．

```python
sns.lineplot(
    data=df,
    x="month",
    y="visitors",
    hue="region",
    errorbar=None
)

plt.title("地域別平均来訪者数の推移")
plt.xlabel("月")
plt.ylabel("平均来訪者数")

plt.show()
```

`hue="region"` を指定すると，地域ごとの平均来訪者数を別々の折れ線で表示できます．

ただし，**このグラフは月ごとの平均値を表しており，来訪者数の合計を表しているわけではありません．**

また，地域によって各月のデータ数が異なる場合があるため，グラフから分かる傾向を考えるときには注意が必要です．

---

##### 27. どのライブラリを使えばよいか

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

##### 28. 3つの方法の特徴

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

##### 29. 実際のデータ分析の流れ

例えば，

**「地域によって観光客の満足度に違いがあるか」**

を調べたいとします．

まずCSVを読み込みます．

```python
df = pd.read_csv(
    "tourism-9.csv"
)
```

データを確認します．

```python
df.head()
```

地域ごとの平均満足度を確認します．

```python
df.groupby(
    "region"
)["satisfaction"].mean()
```

次に，箱ひげ図を作成します．

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

ここで，

- 平均値に違いがあるか
- データのばらつきが大きいか
- 特に高い値や低い値があるか

などを確認します．

平均値だけでは分からないデータの特徴を，箱ひげ図から確認することができます．

---

##### 30. もう1つの分析例

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

##### 31. 条件を絞って分析する

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

##### 32. 複数の条件を指定する

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

##### 33. データを集計してから可視化する

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

##### 34. 「集計」と「そのまま表示」の違い

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

##### 35. グラフを作る前に考えること

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

##### 36. グラフの使い分け

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

##### 37. pandas・matplotlib・seabornの関係

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

##### 38. まとめ

今回使用した主な処理をまとめます．

#### CSVを読み込む

```python
df = pd.read_csv(
    "tourism-9.csv"
)
```

#### 条件で絞り込む

```python
df[
    df["visitors"] >= 200
]
```

#### 集計する

```python
df.groupby(
    "region"
)["visitors"].mean()
```

#### pandasでグラフ

```python
df.plot()
```

#### matplotlib

```python
plt.bar()
plt.plot()
plt.scatter()
plt.hist()
```

#### seaborn

```python
sns.barplot()
sns.lineplot()
sns.scatterplot()
sns.histplot()
sns.boxplot()
```

今回学習したように，pandasでデータを読み込み，必要に応じて抽出や集計を行ってから，matplotlibやseabornでグラフを作成できます．

重要なのは，**グラフを作る前に，どのデータを，どのように集計して表示するのかを考えること**です．

---

##### 39. 最も重要なこと

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

#### 練習問題
##### `tourism-9.csv` を使ってみよう

今回の練習では，授業用に作成した `tourism-9.csv` を使用します．

このCSVには，北海道の観光に関する架空のデータ100件が保存されています．

列は次の8つです．

| 列名 | 内容 |
|---|---|
| `city` | 都市名 |
| `region` | 地域 |
| `visitors` | 来訪者数 |
| `satisfaction` | 満足度 |
| `spending` | 1人あたりの消費金額 |
| `stay_days` | 宿泊日数 |
| `season` | 季節 |
| `month` | 月 |

同じ都市が複数行に登場します．各行は都市・月ごとの観光調査データです．

まずは，必要なライブラリを読み込んでください．

```python
!pip install japanize-matplotlib
```

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import japanize_matplotlib

df = pd.read_csv("tourism-9.csv")
```

---

##### 問題1　データの先頭を確認する

`tourism-9.csv` の先頭5行を表示してください．

---

##### 問題2　データの大きさと列名を確認する

DataFrameの行数・列数と，列名をすべて表示してください．

行数・列数が `(100, 8)` になることを確認してください．

---

##### 問題3　基本的な統計量を確認する

`dtypes` を使って各列のデータ型を表示してください．

さらに，`describe()` を使って数値データの平均値，最小値，最大値などを確認してください．

---

##### 問題4　条件に一致するデータを取り出す

来訪者数が200人以上のデータだけを取り出し，`selected` に保存してください．

さらに，抽出後のデータが何行あるかを確認してください．

---

##### 問題5　都市名で絞り込む

`city` が「札幌」のデータだけを取り出し，`sapporo` に保存してください．

その先頭5行を表示してください．

---

##### 問題6　都市ごとの平均来訪者数を求める

`groupby()` を使って，都市ごとの平均来訪者数を求めてください．

`reset_index()` を使ってDataFrameにし，`city_mean` という変数に保存してください．

---

##### 問題7　matplotlibで棒グラフを作る

問題6で作成した `city_mean` を使用して，都市ごとの平均来訪者数を棒グラフで表示してください．

次の条件を満たしてください．

- 横軸：「都市」
- 縦軸：「平均来訪者数」
- タイトル：「都市別平均来訪者数」

ヒント：`plt.bar()` を使用します．

---

##### 問題8　pandasのグラフ作成機能を使う

問題6で作成した `city_mean` を使用し，pandasの `plot()` で棒グラフを作成してください．

`kind="bar"` を指定し，タイトルを「都市別平均来訪者数」としてください．

---

##### 問題9　並べ替えてグラフにする

問題6で作成した `city_mean` を，平均来訪者数の多い順に並べてください．

その結果を横棒グラフで表示してください．

ヒント：`sort_values()` と `plot(kind="barh")` を使用できます．

---

##### 問題10　matplotlibで散布図を作る

`visitors` と `satisfaction` の関係を散布図で表示してください．

- 横軸：「来訪者数」
- 縦軸：「満足度」
- タイトル：「来訪者数と満足度」

グラフを見て，どのような関係がありそうか考えてください．

---

##### 問題11　pandasで散布図を作る

問題10と同じ散布図を，pandasの `df.plot()` を使って作成してください．

ヒント：`kind="scatter"` を指定します．

---

##### 問題12　seabornで散布図を作る

問題10・11と同じ散布図を，`sns.scatterplot()` で作成してください．

3つの方法の書き方を比較してください．

---

##### 問題13　地域ごとに色分けした散布図を作る

`visitors` と `satisfaction` の散布図を作成し，`region` ごとに点の色を分けてください．

- 横軸：「来訪者数」
- 縦軸：「満足度」
- 色分け：「地域」
- タイトル：「地域別：来訪者数と満足度」

ヒント：`sns.scatterplot()` の `hue` を使用します．

---

##### 問題14　seabornで平均値の棒グラフを作る

`region` ごとの平均消費金額を `sns.barplot()` で表示してください．

- 横軸：「地域」
- 縦軸：「平均消費金額（円）」
- タイトル：「地域別平均消費金額」

誤差範囲は `errorbar=None` で非表示にしてください．

---

##### 問題15　pandasで集計してから棒グラフを作る

問題14と同じ地域別平均消費金額を，今度は `groupby()` で計算してください．

その集計結果をpandasの `plot(kind="bar")` で表示してください．

問題14のグラフと比較してみましょう．

---

##### 問題16　消費金額のヒストグラムを作る

`spending` の分布を `sns.histplot()` で表示してください．

区間数は `bins=10` としてください．

- 横軸：「消費金額（円）」
- 縦軸：「件数」
- タイトル：「消費金額の分布」

---

##### 問題17　地域別のヒストグラムを作る

問題16のヒストグラムを `region` ごとに色分けしてください．

タイトルを「地域別消費金額の分布」としてください．

ヒント：`sns.histplot()` の `hue` を使用します．

---

##### 問題18　地域別の箱ひげ図を作る

`region` ごとの `satisfaction` の分布を箱ひげ図で表示してください．

- 横軸：「地域」
- 縦軸：「満足度」
- タイトル：「地域別満足度」

さらに，`groupby()` で地域ごとの平均満足度を表示し，平均値だけでは分からない特徴がないか考えてください．

---

##### 問題19　月別の折れ線グラフを作る

`month` を横軸，`visitors` を縦軸として `sns.lineplot()` で折れ線グラフを作成してください．

次に，`hue="region"` を追加し，地域ごとの違いを比較してください．

- 横軸：「月」
- 縦軸：「平均来訪者数」
- タイトル：「月別平均来訪者数」

※ 同じ月に複数のデータがあるため，seabornでは既定で月ごとの平均値が折れ線になります．

---

##### 問題20　総合問題

次の操作を順番に行ってください．

1. `city` が「札幌」で，かつ `satisfaction` が4.0以上のデータを抽出してください．
2. 抽出した結果を `selected` という変数に保存してください．
3. `selected` の行数を確認してください．
4. `stay_days` を横軸，`spending` を縦軸とした散布図を `sns.scatterplot()` で作成してください．
5. タイトルを「札幌：宿泊日数と消費金額」としてください．
6. グラフを見て，宿泊日数と消費金額の関係について考えてください．

---

#### 余裕がある人向け

##### 発展問題1　季節別の消費金額

`season` ごとの平均消費金額を求めて，棒グラフで比較してください．

---

##### 発展問題2　季節別の箱ひげ図

`sns.boxplot()` を使い，`season` ごとの消費金額の分布を比較してください．

平均値の棒グラフと箱ひげ図では，分かることにどのような違いがありますか．

---

##### 発展問題3　宿泊日数と消費金額

`stay_days` と `spending` の散布図を作成し，地域ごとに色分けしてください．

宿泊日数が長いほど，消費金額が高くなる傾向があるか確認してください．

---

##### 発展問題4　抽出・集計・グラフを組み合わせる

満足度が4.0以上のデータだけを取り出してください．

次に，そのデータについて地域ごとの平均消費金額を求め，多い順に並べ，棒グラフにしてください．

---

#### 今日のゴール

今回は，

**CSVを読み込む → データを確認する → 抽出・集計する → グラフを作る → 結果を考える**

という一連の流れを練習しました．

特に，同じデータをmatplotlib・pandas・seabornの3つの方法で表示し，書き方や用途の違いを確認してください．

また，棒グラフを作るときは，そのままのデータを表示しているのか，平均値・合計値を表示しているのかを意識することが重要です．
