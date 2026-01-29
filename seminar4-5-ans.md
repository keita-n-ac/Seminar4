### 1
```python
import matplotlib.pyplot as plt
x = [1, 2, 3, 4]
y = [1, 4, 9, 16]
plt.plot(x, y)
plt.show()
```

### 2
```python
import matplotlib.pyplot as plt
x = [1, 2, 3, 4]
y = [1, 4, 9, 16]
plt.plot(y, x)
plt.show()
```

### 3
```python
import matplotlib.pyplot as plt
x = [1, 2, 3, 4]
y = [1, 4, 9, 16]
plt.xlabel('Data ID')
plt.ylabel('Value')
plt.plot(x, y)
plt.show()
```

### 4
```python
import pandas as pd
table_data = [
    [307, 'Sota', 'Aichi', '九段'],
    [308, 'Takahiro', 'Wakayama', '七段'],
    [309, 'Takuya', 'Kyoto', '五段'],
    [310, 'Kazuo', 'Tokyo', '五段'],
]
df = pd.DataFrame(table_data)
print(df)
```

### 5
```python
import pandas as pd
table_data = [
    [307, 'Sota', 'Aichi', '九段'],
    [308, 'Takahiro', 'Wakayama', '七段'],
    [309, 'Takuya', 'Kyoto', '五段'],
    [310, 'Kazuo', 'Tokyo', '五段'],
]
df = pd.DataFrame(table_data, columns=['ID', '名前', '出身', '段位'], index=[0, 1, 2, 3])
print(df)
```

### 6
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data.csv'
df = pd.read_csv(csv_url) # CSVを読み込む
print(df)
```

### 7
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
print(df.head())
```

### 8
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
print(df)
```

### 9
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID','名前','出身','段位']
print(df.columns)
print(df.index)
print(df.dtypes)
print(len(df))
```

### 10
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df1 = df[['名前', 'ID']]
print(df1)
```

### 11
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID','名前','出身','段位']
df1 = df.loc[[1, 3]]
print(df1)
```

### 12
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID','名前','出身','段位']
df1 = df.loc[1, '名前']
print(df1)
```

### 13
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df2 = pd.DataFrame()
df2['名前'] = df['名前']
print(df2)
```

### 14
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID','名前','出身','段位']
df3 = df.drop(columns='段位')
print(df3)
```

### 15
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID','名前','出身','段位']
df3 = df.drop(index=0)
print(df3)
```

### 16
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df = pd.concat([df, pd.DataFrame([[315, 'Kei', 'Kanagawa', '六段']], columns=df.columns)], ignore_index=True)
print(df)
```

### 17
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df4 = df[df['ID'] <= 310]
print(df4)
```

### 18
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df4 = df[(df['ID'] <= 310) & (df['段位'] == '五段')]
print(df4)
```

### 19
```python
import pandas as pd
csv_url = 'https://raw.githubusercontent.com/keita-n-ac/Seminar3/main/kishi_data_no_header.csv'
df = pd.read_csv(csv_url, header=None) # CSVを読み込む
df.columns = ['ID', '名前', '出身', '段位']
df4 = df[(df['ID'] <= 310) | (df['段位'] == '五段')]
print(df4)
```

### 20
```python
import pandas as pd

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
col = ['結果A', '結果B', '結果C']

df = pd.DataFrame(table_data, columns=col)
print(df)

# (1) 各列の平均値・中央値・最頻値
print("平均値")
print(df.mean())
print("中央値")
print(df.median())
print("最頻値")
print(df.mode())

# (2) 結果Aの度数分布表
freq_A = pd.cut(
    df['結果A'],
    bins=[1, 3, 5, 7, 9, 11],
    right=False
).value_counts().sort_index()

print("結果A の度数分布表")
print(freq_A)
```