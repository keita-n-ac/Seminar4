
# アヤメデータ（iris）のプログラム作成問題（20問）

共通の前提として、特に書かれていない限り以下を最初に実行してよいこととします。

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

iris = sns.load_dataset('iris')
```

---

## 基本の確認

### 問題1
irisデータセットを読み込み、以下の情報をそれぞれ `print` で表示するプログラムを書きなさい。

1. データフレーム全体（`print(iris)`）
2. カラム名（`iris.columns`）
3. データ型（`iris.dtypes`）
4. データフレームの大きさ（`iris.shape`）

---

### 問題2
`sepal_length` 列と `petal_width` 列に対して、`describe()` を用いて統計量を表示するプログラムを書きなさい。  
見やすさのために、カラム名と一緒に出力しなさい（例: `"sepal_length"` の後に `describe()` の結果）。

---

### 問題3
`species` 列に対して、

1. `describe()` を実行し結果を表示する  
2. `unique()` を用いて、どの種類のアヤメが含まれているかを表示する  

以上を行うプログラムを書きなさい。

---

## データの抽出・分割

### 問題4
`iris` から `species` が `"setosa"` の行だけを抽出して、新しいデータフレーム `data_setosa` に代入しなさい。  
さらに、`data_setosa` のインデックスを `reset_index(drop=True)` を使って振り直し、その結果を表示するプログラムを書きなさい。

---

### 問題5
`species` が `"versicolor"` のデータを `data_versicolor`、`"virginica"` のデータを `data_virginica` として抽出し、それぞれインデックスを `reset_index(drop=True)` で振り直すプログラムを書きなさい。  
最後に、各データフレームの先頭5行（`head()`）のみを表示しなさい。

---

### 問題6
`sepal_length` が 6.0 以上の行だけを抽出したデータフレーム `data_long_sepal` を作り、  

- 行数（`len(data_long_sepal)`）  
- `sepal_length` の最小値・最大値（`describe()` を使ってもよい）  

を表示するプログラムを書きなさい。

---

### 問題7
`sepal_width` が 3.0 未満の行だけを抽出し、その中でさらに `species` が `"setosa"` の行だけを抽出したデータフレーム `data_narrow_setosa` を作りなさい。  
`data_narrow_setosa` の全行を表示するプログラムを書きなさい。

---

## ヒストグラム

### 問題8
`sepal_length` について、  

- 全データ（`iris`）のヒストグラムを1つ描くプログラムを書きなさい。  
- x軸ラベルを `"sepal_length"` に設定しなさい。  

ヒント: `iris['sepal_length'].hist()` を用いる。

---

### 問題9
`sepal_length` について、  

- `data_setosa` を青 (`color='b'`)、  
- `data_versicolor` を赤 (`color='r'`)、  
- `data_virginica` を緑 (`color='g'`)、  

とし、同じグラフ上に重ねてヒストグラムを描きなさい。  

- 透過度は `alpha=0.5` としなさい。  
- x軸ラベルは `"sepal_length"` としなさい。

---

### 問題10
`petal_width` について、`data_setosa` / `data_versicolor` / `data_virginica` のヒストグラムを1つのグラフ上に重ねて描くプログラムを書きなさい。  

- 色はそれぞれ `b`, `r`, `g`  
- 透過度は `alpha=0.5`  
- x軸ラベルは `"petal_width"`  

としなさい。  

グラフから、setosa とそれ以外を分けられそうかどうかを、`print` 文で一言コメントしなさい（例: `"setosa and others can be separated by petal_width"` など）。

---

## 箱ひげ図

### 問題11
`petal_width` について、  

- `data_setosa`，`data_versicolor`，`data_virginica` の列を `pd.concat` を使って横に結合し、  
- カラム名をそれぞれ `'setosa'`, `'versicolor'`, `'virginica'` に変更する  

データフレーム `df_pw` を作りなさい。  

さらに、`sns.boxplot(data=df_pw, width=0.5)` を用いて箱ひげ図を描くプログラムを書きなさい。

---

### 問題12
問題11と同様の手順で、`petal_length` について  

- `df_pl` というデータフレームを作り、  
- 種類ごとの箱ひげ図を描きなさい。  

グラフから、どの種類の花が最も花びらが長い傾向にあるかを、`print` 文でコメントしなさい。

---

### 問題13
`sepal_width` について、  

- 種類ごとのデータを `pd.concat` で結合し、  
- `'setosa'`, `'versicolor'`, `'virginica'` というカラム名をつけた `df_sw` を作成、  
- 箱ひげ図を描くプログラムを書きなさい。  

さらに、`setosa` の `sepal_width` の中央値を `print` しなさい（箱ひげ図だけでなく、`median()` を使うこと）。

---

### 問題14
`sepal_length` についても同様に、  

- `df_sl` を作り、  
- 箱ひげ図を描くプログラムを書きなさい。  

箱ひげ図から、外れ値（明らかに他と離れた値）が存在しそうかどうかを `print` 文でコメントしなさい。

---

## 2次元散布図

### 問題15
`sepal_width` を x 軸、`sepal_length` を y 軸にとり、  

- `data_setosa` を青 (`color='b'`)、  
- `data_versicolor` を赤 (`color='r'`)、  
- `data_virginica` を緑 (`color='g'`)、  

として散布図を描きなさい。  

軸ラベルは `xlabel='sepal_width'`, `ylabel='sepal_length'` としなさい。

---

### 問題16
問題15で作成した散布図について、  

- `plt.axvline()` や `plt.axhline()` を用いて、setosa とそれ以外を分けられそうな「縦線」または「横線」を1本描きなさい。  

境界線の値（例: `x=3.0` など）は、自分でグラフを見て決め、コード中に直接書きなさい。

---

### 問題17
`petal_length` を x 軸、`petal_width` を y 軸にとった散布図を作成しなさい。  

- 3 種類のアヤメを色 (`b`, `r`, `g`) で区別すること  
- 軸ラベルを `"petal_length"`, `"petal_width"` とすること  

グラフを見て、`print` 文で「setosa とその他を分ける線が引けそうかどうか」をコメントしなさい。

---

## 3次元散布図

### 問題18
`sepal_width`, `sepal_length`, `petal_length` をそれぞれ x, y, z 軸とした 3 次元散布図を描くプログラムを書きなさい。  

- `from mpl_toolkits.mplot3d import Axes3D` を使うこと  
- `data_setosa`, `data_versicolor`, `data_virginica` をそれぞれ異なる色（`b`, `r`, `g`）で描くこと  
- 軸ラベルは `set_xlabel`, `set_ylabel`, `set_zlabel` を使って設定すること

---

### 問題19
問題18のプログラムを拡張し、  

- グラフの視点を `ax.view_init(elev, azim)` で変更するコードを追加しなさい。  
  - 例として `elev=0`, `azim=240` を指定すること。  
- 視点を変えたときの 3 種類のアヤメの分布の違いを、`print` 文で一言コメントしなさい。

---

## 応用（複数の図・条件を組み合わせる）

### 問題20
次の条件を満たすプログラムを書きなさい。  

1. `petal_width` が 1.0 より小さいデータだけを `data_small_pw` として抽出する。  
2. `data_small_pw` の `species` に対する `unique()` を表示し、どの種類が含まれているかを確認する。  
3. `data_small_pw` について、`sepal_length` のヒストグラムを描く。  
4. 3 次元散布図（`sepal_width`, `sepal_length`, `petal_length`）も描き、`data_small_pw` に含まれる種だけプロットする。  

最後に、`print` 文で  

- 「`petal_width < 1.0` のデータは主にどの species か」  

をコメントしなさい。
