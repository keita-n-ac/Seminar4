**共通ルール**

- グラフ描画には `matplotlib`（必要に応じて `seaborn`）を用いること。
- グラフの **タイトル・軸ラベル・凡例ラベルなどはすべて英語** で書くこと。
---

## Q1: Basic Line Plot

次のデータを折れ線グラフで可視化するプログラムを書きなさい。

- X 軸データ: `[0, 100, 200]`
- Y 軸データ: `[100, 0, 200]`

条件:

- タイトル: `"Sample Line Plot"`
- X 軸ラベル: `"X value"`
- Y 軸ラベル: `"Y value"`
- グラフを表示すること（`plt.show()` を使う）。

---

## Q2: seaborn のスタイル設定

`matplotlib.pyplot` を `plt`、`seaborn` を `sns` としてインポートし、次の条件を満たすプログラムを書きなさい。

1. `sns.set(style="whitegrid")` を使って背景に白ベースのグリッドを表示する。
2. Q1 と同じデータで折れ線グラフを描く。
3. タイトル: `"Line Plot with Whitegrid"`
4. X/Y 軸ラベルも英語でつける。

---

## Q3: ヒストグラム（全列）

次のデータから DataFrame を作成し、**すべての列のヒストグラム** を同時に描画するプログラムを書きなさい。

```python
table_data = [
    [1, 5, 1],
    [10, 5, 2],
    [1, 5, 3],
    [10, 5, 4],
    [1, 6, 7],
    [10, 6, 8],
    [1, 6, 9],
    [10, 6, 10],
]
col = ["ResultA", "ResultB", "ResultC"]
```

条件:

- ビン境界: `bins = [1, 3, 5, 7, 9, 11]`
- タイトル: `"Histogram of All Results"`
- X 軸ラベル: `"Value"`
- Y 軸ラベル: `"Frequency"`

---

## Q4: ヒストグラム（列指定）

Q3 と同じ DataFrame `df` を使い、次の 2 つのヒストグラムを描くプログラムを書きなさい。

1. `"ResultA"` だけのヒストグラム  
   - タイトル: `"Histogram of ResultA"`
2. `"ResultC"` だけのヒストグラム  
   - タイトル: `"Histogram of ResultC"`

いずれもビンは Q3 と同じ `bins` を用いること。

---

## Q5: 棒グラフ（Bar Plot）の基本

次のデータから DataFrame を作成し、棒グラフを描くプログラムを書きなさい。

```python
table_data = [
    ["Sato", 60, 65, 66],
    ["Suzuki", 80, 85, 88],
    ["Takahashi", 100, 100, 100],
]
col = ["Name", "SubjectA", "SubjectB", "SubjectC"]
```

条件:

1. `Name` 列をインデックスに設定してから棒グラフを描くこと。
2. `df.plot.bar()` を用いて、3 科目の点数をまとめて表示すること。
3. タイトル: `"Scores of Each Subject"`

---

## Q6: 棒グラフ（1列だけ）

Q5 の DataFrame を使い、`"SubjectA"` のみを棒グラフで表示するプログラムを書きなさい。

条件:

- `df["SubjectA"].plot.bar()` を使うこと。
- タイトル: `"Scores of SubjectA"`
- X 軸ラベル: `"Student"`
- Y 軸ラベル: `"Score"`

---

## Q7: 折れ線グラフ（複数列）

次のデータから DataFrame を作成し、**3 地域の気温変化** を 1 つの折れ線グラフにまとめて描くプログラムを書きなさい。

```python
table_data = [
    [1, 5.6, 18.1, -3.0],
    [2, 7.2, 20.0, -2.6],
    [3, 10.6, 19.9, 2.5],
    [4, 13.6, 22.3, 8.0],
    [5, 20.0, 24.2, 15.7],
    [6, 21.8, 26.5, 17.4],
    [7, 24.1, 28.9, 21.7],
    [8, 28.4, 29.2, 22.5],
    [9, 25.1, 28.0, 19.3],
    [10, 19.4, 26.0, 13.3],
    [11, 13.1, 23.1, 3.9],
    [12, 8.5, 20.0, -0.8],
]
col = ["Month", "RegionA", "RegionB", "RegionC"]
```

条件:

1. `Month` をインデックスに設定してから `df.plot()` で描くこと。
2. タイトル: `"Temperature Change by Region"`
3. X 軸ラベル: `"Month"`
4. Y 軸ラベル: `"Temperature (°C)"`

---

## Q8: 折れ線グラフ（1地域のみ）

Q7 の DataFrame を使い、`"RegionA"` のみの折れ線グラフを描くプログラムを書きなさい。

条件:

- `df["RegionA"].plot()` を用いること。
- タイトル: `"Temperature of RegionA"`
- X 軸ラベル: `"Month"`
- Y 軸ラベル: `"Temperature (°C)"`

---

## Q9: 円グラフ（Pie Chart）の基本

次のデータから DataFrame を作成し、料理 A に対する評価の円グラフを描くプログラムを書きなさい。

```python
table_data = [
    [35, 62],
    [47, 26],
    [18, 12],
]
col = ["DishA", "DishB"]
idx = ["Like", "Neutral", "Dislike"]
```

条件:

1. `DishA` 列のみを使って円グラフを描くこと。
2. デフォルトの設定で `df["DishA"].plot.pie()` を用いること。
3. タイトル: `"Preference for DishA"` をつけること（`plt.title()`）。

---

## Q10: 円グラフ（開始角度と方向・ラベル位置）

Q9 と同じ DataFrame を使い、料理 B に対する評価の円グラフを描きなさい。

条件:

1. `df["DishB"].plot.pie(startangle=90, counterclock=False, labeldistance=0.5)` を用いること。
2. タイトル: `"Preference for DishB"` をつけること。
3. 円グラフが「上から時計回り」に描かれ、ラベルが内側に表示されることを確認するプログラムにしなさい。

---

## Q11: 箱ひげ図（Box Plot）

次のデータから DataFrame を作成し、2 クラスの身長データを箱ひげ図で比較するプログラムを書きなさい。

```python
table_data = [
    [163.6, 166.9],
    [172.6, 172.7],
    [163.7, 166.4],
    [167.1, 173.4],
    [169.9, 169.6],
    [173.9, 171.8],
    [170.1, 166.9],
    [166.2, 168.2],
    [176.7, 166.7],
    [165.4, 169.8],
]
col = ["Class1", "Class2"]
```

条件:

1. `sns.boxplot(data=df, width=0.5)` を用いること。
2. タイトル: `"Height Data of Each Class"`
3. プログラムの最後に `print(df.median())` を書いて、各クラスの中央値を表示すること。

---

## Q12: 散布図（Scatter Plot）

次のデータから DataFrame を作成し、身長と体重の関係を散布図で可視化するプログラムを書きなさい。

```python
table_data = [
    [163.6, 50.5],
    [172.6, 63.3],
    [163.7, 48.5],
    [169.9, 59.8],
    [173.9, 69.8],
    [166.2, 53.7],
    [176.7, 70.3],
    [165.4, 51.2],
]
col = ["Height", "Weight"]
```

条件:

1. `df.plot.scatter(x="Height", y="Weight", c="b")` を用いること。
2. タイトル: `"Relationship between Height and Weight"`
3. X 軸ラベル: `"Height (cm)"`
4. Y 軸ラベル: `"Weight (kg)"`

---

## Q13: 散布図の特定点を強調表示

Q12 の DataFrame を使い、散布図を描いたあとで、インデックス 3 のデータ（4 行目）だけを **赤い三角マーカー** で強調するプログラムを書きなさい。

条件:

1. 散布図は Q12 と同じ条件で描く。
2. その後で  
   `plt.plot(x, y, c="r", marker="^", markersize=10)`  
   の形で 1 点を強調表示すること。
3. タイトルは Q12 と同じにすること。

---

## Q14: 散布図の補助線（axvline, axhline）

Q13 のプログラムを拡張し、強調した点を通る縦線・横線の補助線を追加しなさい。

条件:

1. 縦線: `plt.axvline(x, c="r", linestyle=":")`
2. 横線: `plt.axhline(y, c="r", linestyle=":")`
3. タイトル: `"Relationship between Height and Weight (with guides)"`

---

## Q15: 相関係数の計算

次のデータから DataFrame を作成し、科目間の相関を見るための散布図と相関係数の計算を行うプログラムを書きなさい。

```python
table_data = [
    [100, 94, 80],
    [85, 90, 88],
    [90, 95, 70],
    [95, 90, 62],
    [80, 85, 86],
    [80, 80, 70],
    [75, 75, 79],
    [65, 70, 65],
    [65, 60, 75],
    [60, 60, 67],
    [55, 50, 75],
    [45, 50, 68],
    [45, 48, 60],
]
col = ["SubA", "SubB", "SubC"]
```

条件:

1. `SubA` vs `SubB` の散布図を描き、タイトルを `"SubA vs SubB"` とする。
2. `SubA` vs `SubC` の散布図を描き、タイトルを `"SubA vs SubC"` とする。
3. `df.corr()["SubA"]["SubB"]` と `df.corr()["SubA"]["SubC"]` を計算・表示すること。

---

## Q16: 回帰直線（regplot）

Q15 と同じ DataFrame を使い、seaborn の `regplot` で回帰直線を描くプログラムを書きなさい。

条件:

1. `sns.regplot(data=df, x="SubA", y="SubB", line_kws={"color": "g"})`
2. `sns.regplot(data=df, x="SubA", y="SubC", line_kws={"color": "r"})`
3. それぞれタイトルを `"SubA vs SubB (Regression)"`, `"SubA vs SubC (Regression)"` とする。

---

## Q17: jointplot の利用

Q16 のプログラムをもとに、`sns.jointplot` を使って **散布図＋回帰直線＋ヒストグラム** を同時に表示するプログラムを書きなさい。

条件:

1. `sns.jointplot(data=df, x="SubA", y="SubB", kind="reg", line_kws={"color": "g"})`
2. `sns.jointplot(data=df, x="SubA", y="SubC", kind="reg", line_kws={"color": "r"})`
3. 各 jointplot のあとに `plt.show()` を呼ぶこと。

---

## Q18: 相関行列のヒートマップ

Q15 の DataFrame を用い、相関行列のヒートマップを描くプログラムを書きなさい。

条件:

1. `sns.heatmap(df.corr())` を用いて基本的なヒートマップを描く。
2. そのあと、  
   `sns.heatmap(df.corr(), annot=True, vmax=1, vmin=-1, center=0)`  
   を用いて、相関係数の値を表示しつつ、色の範囲を -1〜1 に固定したヒートマップも描く。
3. 各ヒートマップを表示すること（`plt.show()`）。

---

## Q19: 散布図行列（pairplot）

Q15 の DataFrame を使い、seaborn の `pairplot` を用いて散布図行列を描くプログラムを書きなさい。

条件:

1. `sns.pairplot(data=df)` を実行して、基本的な散布図行列を描く。
2. 続けて `sns.pairplot(data=df, kind="reg")` を実行して、対角以外の部分に回帰直線付きの散布図行列を描く。
3. それぞれのあとに `plt.show()` を呼ぶこと。

---

## Q20: 総合問題（ミニ分析スクリプト）

次の手順を 1 つの Python スクリプトとしてまとめなさい。

1. Q15 と同じ `table_data` と `col` を使って DataFrame を作成する。
2. `describe()` を用いて、3 科目の基本統計量（平均・標準偏差など）を表示する。
3. 各科目のヒストグラムを 1 つの図に重ねて描く（色を変えるなど工夫してよい）。
4. `SubA` vs `SubB`、`SubA` vs `SubC` の散布図を描く。
5. 相関行列のヒートマップを描く。
6. すべてのタイトル・軸ラベルは英語でつけること。


---
