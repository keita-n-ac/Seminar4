## 前準備（最初に1度だけ実行）
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
```

---

## 1. 二重リストからの DataFrame 作成
二重リスト `data1` と列名 `cols` から DataFrame を作成し、型と中身を表示せよ。  
- 変数名：`df1`
```python
data1 = [
    ['田中優花', '女', 140, 40.5],
    ['佐藤和也', '男', 175, 70.2],
    ['鈴木一郎', '男', 170, 65.0],
    ['高橋美香', '女', 158, 55.6],
]
cols = ['氏名', '性別', '身長', '体重']
```

---

## 2. 列・行インデックスと値の確認
`df1` の「列インデックス・行インデックス・値（numpy配列）」をそれぞれ表示せよ。  
- 変数名：`cols_1`, `index_1`, `values_1`

---

## 3. CSV（URL）読み込み
次の URL から CSV を読み込み、DataFrame を表示せよ。  
- 変数名：`df_csv_url`  
```python
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.csv'
```

---

## 4. Excel（URL）読み込み
次の URL から Excel を読み込み、DataFrame を表示せよ。  
- 変数名：`df_excel_url`  
```python
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
```

---

## 5. Series の作成（名前つき）
身長のリスト `[140, 175, 170, 158]` から **名前が「身長」** の Series を作り、型と中身を表示せよ。  
- 変数名：`s_height`

---

## 6. DataFrame 列から Series を取り出す
`df_excel_url` から列「身長」を Series として取り出し、型と中身を表示せよ。  
- 変数名：`s_from_df`

---

## 7. 行を Series として取り出す（loc）
`df_excel_url` の **インデックス1** の行を `loc` で取り出し、型と中身を表示せよ。  
- 変数名：`row_loc1`

---

## 8. データ型（dtypes）の確認
`df_excel_url` の各列のデータ型を表示し、`object`/`int64`/`float64` のどれかを確認せよ。  
- 変数名：`dtypes_excel`

---

## 9. 列の絞り込み
`df_excel_url` から列「氏名」「性別」だけを取り出して表示せよ。  
- 変数名：`df_cols2`

---

## 10. 行の絞り込み（head）
`df_excel_url` の先頭 3 行だけを表示せよ（`head` 使用）。  
- 変数名：`df_head3`

---

## 11. ブールインデックス（単一条件）
`df_excel_url` から「性別」が「男」の行のみを抽出して表示せよ。  
- 変数名：`df_male`

---

## 12. ブールインデックス（複合条件）
`df_excel_url` から「性別=男 **かつ** 身長>=170」の行のみを抽出して表示せよ。  
- 変数名：`df_male_tall`

---

## 13. コピーと列削除（drop）
`df_excel_url` を `copy()` して `df_copy` を作成し、`df_copy` から列「氏名」を `drop(..., axis=1)` で削除して表示せよ。  
- 変数名：`df_copy`, `df_drop_name`

---

## 14. 計算列の追加（BMI）
`df_excel_url` に対して BMI＝**体重 / (身長/100)^2** を計算し、列名「BMI」で追加して表示せよ。  
- 変数名：`df_with_bmi`

---

## 15. insert で列を指定位置に追加
上問の BMI 列を **2番目の列位置（インデックス2）** に `insert` で追加した DataFrame を作り、表示せよ。  
- 変数名：`df_insert_bmi`

---

## 16. Series を concat で結合
次の年齢 Series を作成し、`df_insert_bmi` に `concat(..., axis=1)` で結合して表示せよ。  
- 変数名：`s_age`, `df_with_age`
```python
ages = [10, 25, 45, 34]  # ヒント: name を「年齢」にする
```

---

## 17. 行の追加（辞書＋concat）
辞書 `{'氏名':'山田太郎','性別':'男','身長':165,'体重':64.2}` を1行の DataFrame にして、`df_excel_url` に `concat` で追加（`ignore_index=True`）し、表示せよ。  
- 変数名：`df_added_row`

---

## 18. 行/列の同時絞り込み（loc/条件）
`df_with_bmi` から「性別=女」の **氏名・身長・BMI** だけを表示せよ（列と行の同時指定）。  
- 変数名：`df_female_subset`

---

## 19. 並べ替え（sort_values）
`df_with_bmi` を **BMI の降順** に並べ替えて表示せよ。  
- 変数名：`df_sorted_bmi_desc`

---

### 参考メモ（使ってほしい主なメソッド）
- 作成：`pd.DataFrame`, `pd.Series`  
- 入出力：`pd.read_csv`, `pd.read_excel`  
- 参照：`df[...]`, `.loc[...]`, `.head(n)`, `.dtypes`, `.values`, `.columns`, `.index`  
- 抽出：ブールインデックス（`df[col] == 値`、複合条件は `&`）  
- 変更：`copy()`, `drop()`, `insert()`, 列の計算代入  
- 結合：`pd.concat([...], axis=1 or 0)`  
- 並べ替え：`sort_values(by=..., ascending=...)`

---
