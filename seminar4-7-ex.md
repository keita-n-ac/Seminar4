## A. データ読み込みと基本操作（1〜7）

1. seaborn の `load_dataset("iris")` を使って Iris データを DataFrame `df` に読み込み，`df.head()` を表示するプログラムを書きなさい。
2. `df.shape` と `df.columns` を表示し，行数・列数と列名一覧を確認するプログラムを書きなさい。
3. `df` から `species` 列を削除して数値データだけの DataFrame `df_num` を作成し，`df_num.head()` を表示しなさい。
4. `df_num.corr()` を用いて相関係数行列を計算し，その結果を `print` で表示しなさい。
5. `df.dtypes` を使って，各列のデータ型を表示するプログラムを書きなさい。
6. `df["species"].unique()` を表示し，さらに `df["species"].value_counts()` を表示するプログラムを書きなさい。
7. `df_num.describe()` を表示して基本統計量を確認するプログラムを書きなさい。

## B. ヒートマップと相関（8〜14）

8. `df_num.corr()` を `sns.heatmap` でヒートマップとして描画しなさい。  
   その際 `annot=True`, `vmin=-1`, `vmax=1`, `center=0` を指定しなさい。
9. 問8に加えて `sns.set(style="whitegrid")` を指定してからヒートマップを表示しなさい。
10. `df_num.corr().round(2)` を作成し，その行列を使ってヒートマップを描画しなさい。
11. `df_num.corr()` から `petal_length` 列に関する相関係数だけを取り出して表示しなさい。
12. 問11の結果を絶対値の大きい順に並べ替えて表示するプログラムを書きなさい。
13. `species == "setosa"` の行だけを抽出し，`species` 列を削除した数値データに対して相関ヒートマップを描画しなさい。
14. `"versicolor"` と `"virginica"` についても同様に抽出し，それぞれ相関ヒートマップを描画しなさい。

## C. pairplot と散布図（15〜24）

15. `df_num` に対して `sns.pairplot` を描画しなさい。
16. `df`（species を含む全列）に対して `sns.pairplot` を描画しなさい。
17. `sns.pairplot(data=df, hue="species")` を描画しなさい。
18. `sepal_length`, `sepal_width`, `species` の3列だけを抜き出し，`hue="species"` で pairplot を描画しなさい。
19. `petal_length`, `petal_width`, `species` の3列で同様に pairplot を描画しなさい。
20. `"setosa"` だけを抽出し，数値データに対して `kind="reg"` を指定した pairplot を描画しなさい。
21. `"versicolor"` について問20と同様に実行しなさい。
22. `"virginica"` について問20と同様に実行しなさい。
23. x 軸に `sepal_length`，y 軸に `petal_length` を取った散布図を描画し，  
    軸ラベルとタイトルをすべて英語で設定しなさい。
24. 問23と同じ散布図を `hue="species"` を指定して色分けしたものとして描画しなさい。

## D. ヒストグラム・箱ひげ図・groupby（25〜32）

25. `petal_length` のヒストグラムを 20 ビンで描画し，軸ラベルとタイトルを英語でつけなさい。
26. `sns.histplot` を使い，`petal_length` を `hue="species"` で色分けしたヒストグラムを描画しなさい。
27. `df.groupby("species")` を使って，各 species ごとに4つの数値特徴量の平均値を計算し結果を表示しなさい。
28. 問27で求めた平均値のうち `petal_length` だけを取り出し，  
    species を横軸とした棒グラフとして表示しなさい（ラベルは英語）。
29. `sepal_width` の species ごとの箱ひげ図を描画しなさい（ラベルは英語）。
30. `petal_width` の species ごとの箱ひげ図を描画しなさい（ラベルは英語）。
31. `sepal_length >= 6.0` の行を抽出し，抽出後の行数と先頭5行を表示するプログラムを書きなさい。
32. `sepal_length >= 6.0` かつ `petal_width >= 1.5` の行を抽出し，  
    その `species` の件数を `value_counts()` で表示しなさい。

## E. その他の数値処理・保存（33〜35）

33. `sepal_length / sepal_width` の値を新しい列 `sepal_ratio` として追加し，`df.head()` を表示しなさい。
34. 問33で追加した `sepal_ratio` のヒストグラムを描画し，ラベルとタイトルを英語でつけなさい。
35. `df` を `"iris_dataset.csv"` という名前で保存し（`index=False`）、  
    そのファイルを `pd.read_csv` で読み込んで `head()` を表示しなさい。
