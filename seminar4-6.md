### ゼミナールⅣ 6回目
#### pandas復習（1回）
##### 表データをPythonで扱ってみよう

今回は，Pythonで表形式のデータを扱うためのライブラリ **pandas（パンダス）** を使います．

これまでPythonでは，文章を扱ったり，形態素解析をしたりしてきました．

今回は少し方向を変えて，

- 人口
- 観光客数
- 売上
- アンケート結果
- 気温
- 地域ごとの統計

などの，**表になっているデータ**を扱います．

Excelで扱うようなデータを，Pythonから読み込んで分析できるようになることが今回の目標です．

---

##### 1. pandasとは？

pandasは，Pythonでデータ分析をするときによく使われるライブラリです．

例えば，次のような表があるとします．

| city | population | temperature |
|---|---:|---:|
| 札幌 | 1960000 | 9.2 |
| 函館 | 240000 | 10.0 |
| 旭川 | 320000 | 7.8 |
| 小樽 | 110000 | 9.1 |
| 帯広 | 160000 | 8.5 |

Excelであれば，セルをクリックしたり，並べ替えたり，フィルターをかけたりできます．

pandasを使うと，これと似た操作をPythonのプログラムで行うことができます．

例えば，

- 人口が20万人以上の都市だけ表示する
- 人口の多い順に並べる
- 平均人口を求める
- 都道府県ごとに集計する

といったことができます．

---

##### 2. pandasを読み込む

Google Colabでは，pandasは最初から利用できます．

まず，次のプログラムを実行してください．

```python
import pandas as pd
```

この1行でpandasを使えるようになります．

---

##### `as pd` とは？

本来なら，

```python
pandas
```

と毎回書くこともできます．

しかし，pandasはよく使うので，

```python
import pandas as pd
```

として，以降は

```python
pd
```

という短い名前で使うのが一般的です．

今後，

```python
pd.read_csv()
```

や

```python
pd.DataFrame()
```

というプログラムがたくさん出てきます．

---

##### 3. 表をPythonで作ってみよう

まずは，ファイルを使わずに小さな表をPythonの中で作ってみます．

```python
import pandas as pd

data = {
    "city": ["札幌", "函館", "旭川", "小樽", "帯広"],
    "population": [1960000, 240000, 320000, 110000, 160000],
    "temperature": [9.2, 10.0, 7.8, 9.1, 8.5]
}

df = pd.DataFrame(data)

df
```

実行すると，表が表示されます．

---

##### 4. DataFrameとは？

pandasでは，このような表形式のデータを

**DataFrame（データフレーム）**

と呼びます．

今回のプログラムでは，

```python
df = pd.DataFrame(data)
```

によって，`data`をDataFrameに変換しています．

---

##### 5. `df`とは？

`df`は変数名です．

DataFrameを入れる変数として，

```python
df
```

という名前がよく使われます．

特別な意味があるわけではないので，

```python
table
```

などの名前でも構いません．

ただし，教材やWeb上のサンプルでは`df`が非常によく使われます．

---

##### 6. 行と列

表を扱うときには，

- 行
- 列

という言葉が重要です．

例えば，

| city | population | temperature |
|---|---:|---:|
| 札幌 | 1960000 | 9.2 |
| 函館 | 240000 | 10.0 |

では，

```text
city
population
temperature
```

が**列**です．

一方，

```text
札幌   1960000   9.2
```

が1つの**行**です．

---

##### 7. indexとは？

DataFrameを表示すると，左側に

```text
0
1
2
3
4
```

のような数字が表示されます．

この番号を

**index（インデックス）**

と呼びます．

簡単に言えば，

> 各行につけられた番号

と考えて構いません．

---

##### 8. データの先頭を見る

実際のデータ分析では，数千行や数万行のデータを扱うことがあります．

その場合，

```python
df
```

ですべて表示すると大変です．

そこで，

```python
df.head()
```

を使います．

`head()`を使うと，先頭のデータだけ確認できます．

---

##### 表示する行数を指定する

```python
df.head(3)
```

とすると，先頭3行だけ表示できます．

例えば，

```python
df.head(2)
```

```python
df.head(4)
```

のように数字を変えてみてください．

---

##### 9. データの最後を見る

先頭ではなく，最後のデータを見る場合は，

```python
df.tail()
```

を使います．

```python
df.tail(2)
```

のように行数を指定することもできます．

---

##### 10. データの大きさを確認する

DataFrameに何行・何列あるのか確認したい場合は，

```python
df.shape
```

を使います．

今回は，

```text
(5, 3)
```

のように表示されます．

これは，

```text
5行，3列
```

という意味です．

---

##### 11. 列名を確認する

どんな列があるのか確認する場合は，

```python
df.columns
```

を使います．

実行すると，

```text
Index(['city', 'population', 'temperature'], dtype='object')
```

のように表示されます．

ここから，

```text
city
population
temperature
```

という3つの列があることが分かります．

---

##### 12. 1つの列を取り出す

都市名だけを表示してみましょう．

```python
df["city"]
```

人口だけなら，

```python
df["population"]
```

です．

平均気温なら，

```python
df["temperature"]
```

です．

基本形は，

```python
df["列名"]
```

です．

---

##### 13. 複数の列を取り出す

都市名と人口の2列を表示してみます．

```python
df[["city", "population"]]
```

1つの列の場合は，

```python
df["city"]
```

複数の列の場合は，

```python
df[["city", "population"]]
```

となります．

---

##### 14. ファイル入出力の復習

ここからは，Pythonのファイル入出力を使います．

まず，PythonからCSVファイルを作ってみましょう．

---

##### 15. `open()`でファイルを作る

次のプログラムを実行してください．

```python
text = """city,population,temperature
札幌,1960000,9.2
函館,240000,10.0
旭川,320000,7.8
小樽,110000,9.1
帯広,160000,8.5
"""

with open("city.csv", "w", encoding="utf-8") as f:
    f.write(text)
```

これで，

```text
city.csv
```

というファイルが作成されます．

---

##### 16. `with open()`の復習

基本形は，

```python
with open("ファイル名", "モード", encoding="utf-8") as f:
    処理
```

です．

今回の

```python
"w"
```

は，

**write**

の`w`で，

> ファイルに書き込む

という意味です．

---

##### 17. 作成したファイルを読み込む

今度は，作成した`city.csv`を普通のPythonで読み込んでみます．

```python
with open("city.csv", "r", encoding="utf-8") as f:
    text = f.read()

print(text)
```

`"r"`は，

**read**

の`r`です．

> ファイルを読み込む

という意味です．

---

##### 18. CSVファイルとは？

先ほど作成したファイルの中身は，

```text
city,population,temperature
札幌,1960000,9.2
函館,240000,10.0
旭川,320000,7.8
小樽,110000,9.1
帯広,160000,8.5
```

となっています．

CSVは，

**Comma-Separated Values**

の略です．

値が，

```text
,
```

カンマで区切られています．

---

##### 19. pandasでCSVを読み込む

ここからpandasを使います．

先ほど作成した`city.csv`を読み込んでみましょう．

```python
df = pd.read_csv("city.csv")

df
```

これだけで，CSVファイルが表として読み込まれます．

---

##### 20. `read_csv()`とは？

```python
pd.read_csv()
```

は，

> CSVファイルを読み込んでDataFrameに変換する

ための命令です．

基本形は，

```python
pd.read_csv("ファイル名")
```

です．

---

##### 21. 普通のファイル読み込みとの違い

普通のPythonで，

```python
with open("city.csv", "r", encoding="utf-8") as f:
    text = f.read()
```

とすると，ファイル全体が**文字列**として読み込まれます．

一方，

```python
df = pd.read_csv("city.csv")
```

とすると，CSVの内容を自動的に区切って，

**DataFrame**

として読み込んでくれます．

これがpandasの便利なところです．

---

##### 22. CSVを読み込んだら確認する

CSVを読み込んだら，最初に中身を確認します．

```python
df.head()
```

次に，

```python
df.shape
```

さらに，

```python
df.columns
```

も確認します．

この3つは今後もよく使います．

---

##### 23. 数値の列を計算する

pandasでは，数値の列に対して簡単な計算ができます．

人口の合計は，

```python
df["population"].sum()
```

です．

人口の平均は，

```python
df["population"].mean()
```

最大値は，

```python
df["population"].max()
```

最小値は，

```python
df["population"].min()
```

です．

---

##### 24. pandasからCSVを書き出す

pandasでは，DataFrameをCSVファイルとして保存することもできます．

```python
df.to_csv("output.csv", index=False)
```

これで，

```text
output.csv
```

というファイルが作成されます．

---

##### 25. `index=False`とは？

何も指定しないで，

```python
df.to_csv("output.csv")
```

とすると，DataFrameのindexもCSVに保存されます．

今回はindexを保存する必要がないため，

```python
index=False
```

を指定します．

---

##### 26. 保存したCSVを確認する

先ほど保存した`output.csv`を，普通のPythonで読み込んでみましょう．

```python
with open("output.csv", "r", encoding="utf-8") as f:
    text = f.read()

print(text)
```

DataFrameの内容がCSV形式で保存されていることを確認できます．

---

##### 27. ファイル入出力の流れ

今回扱った流れを整理すると，

```text
Pythonでファイルを書く
        ↓
CSVファイル
        ↓
pandasで読み込む
        ↓
DataFrame
        ↓
データを処理する
        ↓
CSVファイルとして保存する
```

となります．

---

##### 28. 今回のまとめ

pandasを読み込むには，

```python
import pandas as pd
```

DataFrameを作るには，

```python
df = pd.DataFrame(data)
```

データの先頭を見るには，

```python
df.head()
```

行数・列数を見るには，

```python
df.shape
```

列名を見るには，

```python
df.columns
```

1つの列を取り出すには，

```python
df["city"]
```

複数の列を取り出すには，

```python
df[["city", "population"]]
```

CSVを読み込むには，

```python
df = pd.read_csv("city.csv")
```

CSVを書き出すには，

```python
df.to_csv("output.csv", index=False)
```

を使います．

---

#### 練習問題
##### `tourism-6.csv`を使ってみよう

今回の練習では，授業で配布した

```text
tourism-6.csv
```

を使用します．

このCSVには，北海道の観光に関する**架空のデータ100件**が保存されています．

列は次の5つです．

| 列名 | 内容 |
|---|---|
| `id` | データ番号 |
| `city` | 都市名 |
| `category` | カテゴリ |
| `visitors` | 来訪者数 |
| `rating` | 評価 |

まずは，`tourism-6.csv`がプログラムと同じ場所にあることを確認してください．

---

##### 問題1

Pythonのファイル入出力を使って，`tourism-6.csv`を読み込んでください．

読み込んだ内容を`print()`で表示してください．

##### ヒント

```python
with open(...)
```

を使います．

---

##### 問題2

Pythonのファイル入出力を使って，`tourism-6.csv`の**1行目だけ**を読み込んで表示してください．

##### ヒント

```python
f.readline()
```

を使うことができます．

---

##### 問題3

pandasを

```python
pd
```

という名前で使用できるように読み込んでください．

---

##### 問題4

pandasを使って`tourism.csv`を読み込み，

```python
df
```

という変数に保存してください．

---

##### 問題5

`df`をそのまま表示してください．

普通のファイル入出力で読み込んだ場合と，表示のされ方を比較してみてください．

---

##### 問題6

`tourism-6.csv`の**先頭5行**を表示してください．

---

##### 問題7

`tourism-6.csv`の**先頭10行**を表示してください．

---

##### 問題8

`tourism-6.csv`の**最後の5行**を表示してください．

---

##### 問題9

`tourism-6.csv`が何行・何列のデータなのか確認してください．

実行結果が，

```text
(100, 5)
```

になることを確認してください．

---

##### 問題10

`tourism-6.csv`に含まれている列名をすべて表示してください．

---

##### 問題11

`city`列だけを取り出して表示してください．

---

##### 問題12

`visitors`列だけを取り出して表示してください．

---

##### 問題13

次の2列だけを取り出して表示してください．

- `city`
- `visitors`

---

##### 問題14

次の3列だけを取り出して表示してください．

- `city`
- `category`
- `rating`

---

##### 問題15

`visitors`列に保存されている来訪者数の**合計**を求めてください．

##### ヒント

```python
.sum()
```

を使います．

---

##### 問題16

`visitors`列に保存されている来訪者数の**平均**を求めてください．

---

##### 問題17

`visitors`列の**最大値**を求めてください．

---

##### 問題18

次の2つをそれぞれ求めてください．

1. `rating`の最大値
2. `rating`の最小値

---

##### 問題19

`describe()`を使って，`tourism-6.csv`の数値データについて基本的な統計情報をまとめて表示してください．

表示された結果から，

- `count`
- `mean`
- `min`
- `max`

がどこに表示されているか探してみてください．

---

##### 問題20

`df`から，

- `city`
- `category`
- `visitors`

の3列だけを取り出してください．

そして，そのデータを

```text
tourism_basic.csv
```

という名前で保存してください．

ただし，DataFrameのindexは保存しないものとします．

保存した後，もう一度

```python
pd.read_csv()
```

を使って`tourism_basic.csv`を読み込み，中身を確認してください．

---

#### 余裕がある人向け

20問が終わった人は，次の処理も試してみましょう．

##### 1. `rating`の平均値

```python
df["rating"].mean()
```

##### 2. `visitors`の最小値

```python
df["visitors"].min()
```

##### 3. 最後の10件を表示

```python
df.tail(10)
```

##### 4. `city`と`rating`だけを別のCSVに保存

```python
result = df[["city", "rating"]]

result.to_csv(
    "city_rating.csv",
    index=False
)
```

---

# 今回できるようになってほしいこと

今回の練習で特に覚えてほしいのは，次の操作です．

```python
pd.read_csv("tourism-6.csv")
```

CSVを読み込む．

```python
df.head()
```

データの先頭を見る．

```python
df.tail()
```

データの最後を見る．

```python
df.shape
```

データの大きさを確認する．

```python
df.columns
```

列名を確認する．

```python
df["visitors"]
```

1つの列を取り出す．

```python
df[["city", "visitors"]]
```

複数の列を取り出す．

```python
df["visitors"].mean()
```

簡単な集計をする．

```python
df.to_csv(
    "output.csv",
    index=False
)
```

CSVとして保存する．

次回は，この100件のデータから，

> 来訪者数が1000人以上のデータだけ取り出す

> 評価が4.0以上のデータだけ取り出す

> 来訪者数の多い順に並べる

といった，**条件によるデータの抽出と並べ替え**を行います．


---

##### 今日のゴール

今回の授業では，

> PythonでCSVファイルを作り，pandasで読み込み，必要な列を取り出し，再びCSVとして保存する

ことができれば十分です．

特に，

```python
with open(...)
```

によるファイル入出力と，

```python
pd.read_csv(...)
```

によるpandasの読み込みの違いを確認してください．

次回は，

- 条件によるデータの絞り込み
- データの並べ替え
- 新しい列の追加

を行います．

例えば，

> 人口20万人以上の都市だけ表示する

といった処理ができるようになります．
