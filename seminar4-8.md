### ゼミナールⅣ 8回目
#### pandas復習（3回）
##### データの集計と結合

これまでの授業では，pandasを使って，

- CSVファイルの読み込み
- DataFrameの確認
- 必要な列の取り出し
- 条件によるデータの抽出
- データの並べ替え
- 新しい列の追加

などを行いました．

今回はpandasの最後として，

- 同じ種類のデータをまとめる
- グループごとに平均や合計を求める
- データの件数を数える
- 複数の集計を一度に行う
- 2つの表を結合する

という処理を行います．

今回も，

```text
tourism.csv
```

を使用します．

---

##### 1. データを読み込む

まずpandasを読み込みます．

```python
import pandas as pd
```

次に，`tourism.csv`を読み込みます．

```python
df = pd.read_csv("tourism.csv")

df.head()
```

---

##### 2. データを確認する

前回までの復習です．

```python
df.shape
```

今回のデータは，

```text
100行 × 5列
```

です．

列名も確認してみましょう．

```python
df.columns
```

次の5つの列があります．

```text
id
city
category
visitors
rating
```

---

##### 3. 同じ値が何件あるか調べる

まず，

```python
df["city"].value_counts()
```

を実行してみましょう．

`value_counts()`は，

> 同じ値が何個あるのか数える

ための命令です．

今回のデータでは，それぞれの都市が何件ずつ含まれているのか確認できます．

---

##### 4. categoryの件数を確認する

```python
df["category"].value_counts()
```

これで，

- 観光
- 飲食
- 宿泊

がそれぞれ何件あるのか確認できます．

---

##### 5. value_counts()の使いどころ

例えばアンケートデータで，

```text
男性
女性
男性
男性
女性
```

というデータがあれば，

```python
df["回答"].value_counts()
```

によって，それぞれの回答数を数えることができます．

つまり，

> カテゴリごとの件数を調べる

ときに便利です．

---

##### 6. groupbyとは？

次に，今回の中心となる

```python
groupby()
```

を使います．

`groupby()`は，

> 同じ種類のデータをグループにまとめる

ための機能です．

例えば，

> 都市ごとに来訪者数の平均を求める

場合は，

```python
df.groupby("city")["visitors"].mean()
```

とします．

---

##### 7. groupbyの基本形

基本的な形は，

```python
df.groupby("グループにする列")["計算する列"].計算()
```

です．

例えば，

```python
df.groupby("city")["visitors"].mean()
```

では，

```text
city
```

ごとにグループを作り，

```text
visitors
```

の平均を求めています．

---

##### 8. 都市ごとの平均来訪者数

実際に実行してみましょう．

```python
df.groupby("city")["visitors"].mean()
```

これで，

> 各都市の平均来訪者数

を求めることができます．

---

##### 9. 都市ごとの来訪者数合計

平均ではなく，合計を求める場合は，

```python
df.groupby("city")["visitors"].sum()
```

とします．

---

##### 10. 都市ごとの最大値

各都市について，最も多かった来訪者数を調べる場合は，

```python
df.groupby("city")["visitors"].max()
```

とします．

---

##### 11. カテゴリごとの平均評価

次は都市ではなく，

```text
category
```

でグループ分けしてみます．

```python
df.groupby("category")["rating"].mean()
```

これで，

- 観光
- 飲食
- 宿泊

それぞれの平均評価を求めることができます．

---

##### 12. カテゴリごとの平均来訪者数

```python
df.groupby("category")["visitors"].mean()
```

これでカテゴリごとの平均来訪者数が分かります．

---

##### 13. 集計結果をDataFrameにする

これまでの結果は少し特殊な形式で表示されます．

例えば，

```python
df.groupby("city")["visitors"].mean()
```

の結果を普通のDataFrameにしたい場合は，

```python
result = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

result
```

とします．

---

##### 14. reset_index()

```python
reset_index()
```

を使うと，

```text
city
visitors
```

という普通の列を持つDataFrameになります．

この形にしておくと，

- CSVとして保存する
- 並べ替える
- 他の表と結合する

といった処理がしやすくなります．

---

##### 15. 集計結果を並べ替える

都市ごとの平均来訪者数を求めて，多い順に並べてみましょう．

```python
result = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

result = result.sort_values(
    "visitors",
    ascending=False
)

result
```

---

##### 16. 複数の値をまとめて計算する

今度は，

- 平均
- 最大
- 最小

をまとめて計算してみます．

```python
df.groupby("city")["visitors"].agg(
    ["mean", "max", "min"]
)
```

---

##### 17. aggとは？

```python
agg()
```

は，

> 複数の集計処理をまとめて実行する

ときに使います．

例えば，

```python
df.groupby("category")["rating"].agg(
    ["mean", "max", "min"]
)
```

とすれば，

カテゴリごとに，

- 平均評価
- 最大評価
- 最小評価

を一度に確認できます．

---

##### 18. データ数も集計する

`count`を加えることもできます．

```python
df.groupby("city")["visitors"].agg(
    ["count", "mean", "max", "min"]
)
```

これで，

- データ数
- 平均
- 最大
- 最小

をまとめて確認できます．

---

##### 19. 2つの列でグループ分けする

少し発展です．

例えば，

> 都市ごと，さらにカテゴリごと

に平均来訪者数を求めたい場合は，

```python
df.groupby(
    ["city", "category"]
)["visitors"].mean()
```

とします．

---

##### 20. DataFrameとして表示する

```python
result = (
    df.groupby(
        ["city", "category"]
    )["visitors"]
    .mean()
    .reset_index()
)

result
```

これで，

```text
city
category
visitors
```

という3列のDataFrameになります．

---

##### 21. 集計結果をCSVとして保存する

例えば，都市ごとの平均来訪者数を保存します．

```python
result = (
    df.groupby("city")["visitors"]
    .mean()
    .reset_index()
)

result.to_csv(
    "city_average.csv",
    index=False
)
```

---

##### 22. ここからは「表の結合」

pandasでは，2つのDataFrameを結合することもできます．

これは今後GeoPandasを使うときにも非常に重要です．

例えば，

**表A**

| city | visitors |
|---|---:|
| 札幌 | 1700 |
| 函館 | 1200 |
| 旭川 | 1000 |

と，

**表B**

| city | area |
|---|---:|
| 札幌 | 1121 |
| 函館 | 678 |
| 旭川 | 748 |

があるとします．

この2つの表を，

```text
city
```

を基準に結合できます．

---

##### 23. 2つ目のCSVを作る

今回は都市に関する基本情報を，

```text
city_info.csv
```

として作ります．

次のプログラムを実行してください．

```python
text = """city,population,area
札幌,1967000,1121.26
函館,239000,677.87
旭川,318000,747.66
小樽,106000,243.83
帯広,164000,619.34
釧路,157000,1363.29
北見,111000,1427.41
苫小牧,168000,561.57
千歳,98000,594.50
稚内,31000,761.47
"""

with open(
    "city_info.csv",
    "w",
    encoding="utf-8"
) as f:
    f.write(text)
```

※ このデータは授業用のサンプルです．

---

##### 24. city_info.csvを読み込む

```python
city_info = pd.read_csv(
    "city_info.csv"
)

city_info
```

---

##### 25. 2つのDataFrameを確認する

今回使うのは，

```python
df
```

と，

```python
city_info
```

です．

まず，

```python
df.head()
```

を確認します．

次に，

```python
city_info.head()
```

を確認します．

両方に，

```text
city
```

という列があります．

---

##### 26. merge()とは？

2つのDataFrameを結合するには，

```python
merge()
```

を使います．

今回は，

```python
merged = pd.merge(
    df,
    city_info,
    on="city"
)

merged.head()
```

とします．

---

##### 27. on="city"の意味

```python
on="city"
```

は，

> city列を基準にして2つの表を結合する

という意味です．

例えば，

```text
札幌
```

というデータ同士，

```text
函館
```

というデータ同士が結び付けられます．

---

##### 28. 結合後のデータ

結合すると，

元の

```text
id
city
category
visitors
rating
```

に加えて，

```text
population
area
```

が追加されます．

確認してみましょう．

```python
merged.columns
```

---

##### 29. 必要な列だけを見る

```python
merged[
    [
        "city",
        "category",
        "visitors",
        "population",
        "area"
    ]
].head()
```

---

##### 30. 結合すると何ができる？

例えば元の観光データには，

```text
population
```

がありませんでした．

しかし，`city_info.csv`と結合することで，

> 観光データ ＋ 人口データ

として扱えるようになります．

これは実際のデータ分析でも非常によく使います．

---

##### 31. 人口1万人あたりの来訪者数を作る

結合したデータを使って，新しい列を作ることもできます．

```python
merged["visitors_per_10000"] = (
    merged["visitors"]
    / merged["population"]
    * 10000
)
```

確認します．

```python
merged[
    [
        "city",
        "visitors",
        "population",
        "visitors_per_10000"
    ]
].head()
```

---

##### 32. 結合後のデータを集計する

都市ごとの人口1万人あたり平均来訪者数を求めてみます．

```python
result = (
    merged.groupby("city")[
        "visitors_per_10000"
    ]
    .mean()
    .reset_index()
)

result
```

---

##### 33. 多い順に並べる

```python
result.sort_values(
    "visitors_per_10000",
    ascending=False
)
```

このように，

> 別々のデータを結合して新しい指標を作る

こともできます．

---

##### 34. merge()がGeoPandasにつながる

次回から扱うGeoPandasでは，

```text
市町村名
人口
```

のような表と，

```text
市町村名
地図の形
```

を結合します．

考え方は今回の，

```python
pd.merge()
```

とほぼ同じです．

つまり，

```text
統計データ
        ＋
地図データ
        ↓
統計情報を持つ地図
```

という形にします．

---

#### 今回のまとめ

##### 件数を調べる

```python
df["city"].value_counts()
```

---

##### グループごとの平均

```python
df.groupby("city")[
    "visitors"
].mean()
```

---

##### グループごとの合計

```python
df.groupby("city")[
    "visitors"
].sum()
```

---

##### 複数の集計

```python
df.groupby("city")[
    "visitors"
].agg(
    ["mean", "max", "min"]
)
```

---

##### DataFrameに戻す

```python
df.groupby("city")[
    "visitors"
].mean().reset_index()
```

---

##### 2つの表を結合

```python
pd.merge(
    df,
    city_info,
    on="city"
)
```

---

#### 練習問題

まず，

```python
import pandas as pd

df = pd.read_csv(
    "tourism.csv"
)
```

を実行してください．

---

##### 問題1

`city`列について，それぞれの都市が何件ずつあるか調べてください．

---

##### 問題2

`category`列について，それぞれのカテゴリが何件ずつあるか調べてください．

---

##### 問題3

都市ごとの平均来訪者数を求めてください．

---

##### 問題4

都市ごとの来訪者数合計を求めてください．

---

##### 問題5

都市ごとの来訪者数最大値を求めてください．

---

##### 問題6

カテゴリごとの平均来訪者数を求めてください．

---

##### 問題7

カテゴリごとの平均評価を求めてください．

---

##### 問題8

都市ごとの平均評価を求めてください．

---

##### 問題9

都市ごとの平均来訪者数を求め，その結果を`reset_index()`を使ってDataFrameにしてください．

---

##### 問題10

問題9の結果を，平均来訪者数の多い順に並べてください．

---

##### 問題11

都市ごとの来訪者数について，

- データ数
- 平均
- 最大
- 最小

を一度に求めてください．

---

##### 問題12

カテゴリごとの評価について，

- 平均
- 最大
- 最小

を一度に求めてください．

---

##### 問題13

`city`と`category`の2つでグループ分けして，平均来訪者数を求めてください．

---

##### 問題14

都市ごとの平均来訪者数を，

```text
city_average.csv
```

として保存してください．

indexは保存しないものとします．

---

##### 問題15

`city_info.csv`を読み込んで，

```python
city_info
```

という変数に保存してください．

---

##### 問題16

`tourism.csv`のデータと`city_info.csv`のデータを，

```text
city
```

を基準に結合してください．

結合した結果を，

```python
merged
```

という変数に保存してください．

---

##### 問題17

`merged`から，

- `city`
- `visitors`
- `population`

の3列だけを表示してください．

---

##### 問題18

`merged`に，

```text
visitors_per_10000
```

という新しい列を作ってください．

計算方法は，

```text
visitors ÷ population × 10000
```

とします．

---

##### 問題19

都市ごとの`visitors_per_10000`の平均を求めてください．

さらに，多い順に並べてください．

---

##### 問題20

結合した`merged`を，

```text
tourism_merged.csv
```

という名前で保存してください．

indexは保存しないものとします．

---


#### 余裕がある人向け

##### 発展問題1

都市ごとに，

- 平均来訪者数
- 平均評価

の両方を求めてみましょう．

```python
df.groupby("city")[
    ["visitors", "rating"]
].mean()
```

---

##### 発展問題2

カテゴリごとの平均来訪者数を求めて，多い順に並べてください．

```python
result = (
    df.groupby("category")[
        "visitors"
    ]
    .mean()
    .reset_index()
)

result.sort_values(
    "visitors",
    ascending=False
)
```

---

##### 発展問題3

`merged`を使って，人口10万人以上の都市だけを取り出してください．

```python
merged[
    merged["population"] >= 100000
]
```

---

##### 発展問題4

人口10万人以上の都市について，都市ごとの平均来訪者数を求めてください．

```python
large_city = merged[
    merged["population"] >= 100000
]

large_city.groupby("city")[
    "visitors"
].mean()
```

---

### pandas 3回分のまとめ

3回の授業で，次の操作を学びました．

#### 第1回

```text
CSVを読み込む
↓
データを確認する
↓
必要な列を取り出す
↓
基本的な統計量を求める
```

主な命令：

```python
pd.read_csv()
df.head()
df.tail()
df.shape
df.columns
df["列名"]
df.describe()
```

---

#### 第2回

```text
条件を指定する
↓
必要な行を取り出す
↓
並べ替える
↓
新しい列を作る
```

主な命令：

```python
df[df["列名"] >= 値]

df.sort_values()

df["新しい列"] = ...

df.loc[]
```

---

#### 第3回

```text
同じ種類のデータをまとめる
↓
グループごとに集計する
↓
別の表と結合する
```

主な命令：

```python
value_counts()

groupby()

agg()

reset_index()

pd.merge()
```

---

##### ここまでできれば

例えば，

```text
1000件の観光データ
```

があったとしても，

pandasを使えば，

```text
必要なデータだけ抽出
        ↓
都市ごとに集計
        ↓
平均値を計算
        ↓
人口データと結合
        ↓
分析結果をCSVとして保存
```

という一連の処理ができます．

これがPythonを使ったデータ分析の基本になります．

---

#### 次回から

次回からは，

**GeoPandas**

を使います．

これまで扱ってきたpandasは，

```text
都市名
人口
来訪者数
評価
```

のような表を扱いました．

GeoPandasでは，これに，

```text
地図上の位置や形
```

を追加します．

つまり，

```text
pandas

都市名
人口
来訪者数

        ＋

地理情報

        ↓

GeoPandas

都市名
人口
来訪者数
地図上の形
```

となります．

今回学習した，

```python
pd.merge()
```

による表の結合は，GeoPandasでも非常によく使います．

次回はまず，

> Pythonで地図データを読み込み，北海道などの地図を表示する

ところから始めます．
