### 1
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)

data1 = [
    ['田中優花', '女', 140, 40.5],
    ['佐藤和也', '男', 175, 70.2],
    ['鈴木一郎', '男', 170, 65.0],
    ['高橋美香', '女', 158, 55.6],
]
cols = ['氏名', '性別', '身長', '体重']

df1 = pd.DataFrame(data1, columns=['氏名', '性別', '身長', '体重'])

print(type(df1))
display(df1)
```

### 2
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)

data1 = [
    ['田中優花', '女', 140, 40.5],
    ['佐藤和也', '男', 175, 70.2],
    ['鈴木一郎', '男', 170, 65.0],
    ['高橋美香', '女', 158, 55.6],
]
cols = ['氏名', '性別', '身長', '体重']

df1 = pd.DataFrame(data1, columns=['氏名', '性別', '身長', '体重'])
cols_1 = df1.columns
index_1 = df1.index
values_1 = df1.values
print('列インデックス', cols_1)
print('行インデックス', index_1)
print('データの中身\n', values_1)
```

### 3
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.csv'
df_csv_url = pd.read_csv(csv_url)
display(df_csv_url)
```

### 4
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url)
display(df_excel_url)
```

### 5
```python
s_height = pd.Series(
    [140, 175, 170, 158],
    name='身長')
print(type(s_height))
print(s_height)
```

### 6
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
s_from_df = df_excel_url['身長']
print(type(s_from_df))
print(s_from_df)
```

### 7
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
row_loc1 = df_excel_url.loc[1]
print(type(row_loc1))
print(row_loc1)
```

### 8
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
dtypes_excel = df_excel_url.dtypes
print(dtypes_excel)
```

### 9
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
cols = ['氏名', '性別']
df_cols2 = df_excel_url[cols]
print(type(df_cols2))
dtypes_excel = df_excel_url.dtypes
print(df_cols2)
```

### 10
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
df_head3 = df_excel_url.head(3)
print(df_head3)
```

### 11
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
index = (df_excel_url['性別'] == '男')
df_male = df_excel_url[index]
display(df_male)
```

### 12
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
index = ((df_excel_url['性別'] == '男') & (df_excel_url['身長'] >= 170))
df_male_tall = df_excel_url[index]
display(df_male_tall)
```

### 13
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
df_copy = df_excel_url.copy()
df_drop_name = df_copy.drop('氏名', axis=1)
display(df_drop_name)
```

### 14
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
bmi = df_excel_url['体重'] / (df_excel_url['身長'] / 100) ** 2 # BMIを計算
df_with_bmi = df_excel_url.copy()
df_with_bmi['BMI'] = bmi # カラムBMIでbmiを追加する
display(df_with_bmi)
```

### 15
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
bmi = df_excel_url['体重'] / (df_excel_url['身長'] / 100) ** 2 # BMIを計算
df_insert_bmi = df_excel_url.copy()
df_insert_bmi.insert(2, 'BMI', bmi)  # 2列目をカラムBMIでbmiを追加する
display(df_insert_bmi)
```

### 16
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
bmi = df_excel_url['体重'] / (df_excel_url['身長'] / 100) ** 2 # BMIを計算
df_insert_bmi = df_excel_url.copy()
df_insert_bmi.insert(2, 'BMI', bmi)  # 2列目をカラムBMIでbmiを追加する
s_age = pd.Series([10, 25, 45, 34], name='年齢')
df_with_age = pd.concat([df_insert_bmi, s_age], axis=1)
display(df_with_age)
```

### 17
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
new_dict = {'氏名': '山田太郎', '性別': '男', '身長': 165, '体重': 64.2}
new_data = pd.DataFrame([new_dict])
df_added_row = pd.concat([df_excel_url, new_data], ignore_index=True)
display(df_added_row)
```

### 18
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
bmi = df_excel_url['体重'] / (df_excel_url['身長'] / 100) ** 2 # BMIを計算
df_with_bmi = df_excel_url.copy()
df_with_bmi['BMI'] = bmi # カラムBMIでbmiを追加する
df_female_subset = df_with_bmi.loc[df_with_bmi['性別'] == '女', ['氏名', '身長', 'BMI']]
display(df_female_subset)
```

### 19
```python
import pandas as pd
from IPython.display import display
pd.options.display.float_format = '{:.4f}'.format
pd.set_option('display.max_columns', None)
excel_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/df-sample.xlsx'
df_excel_url = pd.read_excel(excel_url) # excelファイルを読み込む
bmi = df_excel_url['体重'] / (df_excel_url['身長'] / 100) ** 2 # BMIを計算
df_with_bmi = df_excel_url.copy()
df_with_bmi['BMI'] = bmi # カラムBMIでbmiを追加する
df_sorted_bmi_desc = df_with_bmi.sort_values('BMI', ascending=False)
display(df_sorted_bmi_desc)
```