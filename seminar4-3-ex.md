#### Matplotlib基礎

1. import matplotlib.pyplot as plt を実行し、plt.plot([1,2,3,4]) を表示せよ。

2. x = np.linspace(0, 2, 11)、y = x**2 を折れ線グラフで表示せよ。

3. 軸ラベル x, y とタイトル「二次関数」を追加せよ。

4. グリッドを表示する plt.grid() を使え。

5. 凡例を plt.legend() で表示せよ。

6. ルート関数 y=np.sqrt(x) と二次関数 y=x**2 を同じグラフに重ねて描け。

7. 問題6のグラフを2列表示にし、左にルート関数、右に二次関数を出力せよ。

8. plt.figure(figsize=(10,4)) を試してサイズを変更せよ。

9. サブプロット (2,2) 配置にして異なる関数を4つ描け。

10. plt.scatter() を用いて x と x**2 の散布図を描け。

#### scikit-learn基礎

1. from sklearn.datasets import load_iris を用いて Iris データを読み込め。

2. iris.data の shape と最初の5行を表示せよ。

3. iris.target の shape と最初の10行を表示せよ。

4. iris.feature_names を出力せよ。

5. x = iris.data, y = iris.target として型を確認せよ。

6. plt.scatter(x[:,0], x[:,2]) を表示せよ。

7. plt.scatter(x[:,0], x[:,2], c=y, cmap='rainbow') として色分けせよ。

8. 軸ラベルに feature_names を使用してタイトルを付けよ。

9. サブプロット3枚（1行3列）で (0,1),(0,2),(0,3) の散布図を並べよ。

10. 4×4 の全組み合わせ散布図を自動生成する for ループを書け。
サブプロット3枚（1行3列）で (0,1),(0,2),(0,3) の散布図を並べよ。

4×4 の全組み合わせ散布図を自動生成する for ループを書け。
