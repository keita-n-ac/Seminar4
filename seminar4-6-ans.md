### Q1
```python
import matplotlib.pyplot as plt
x = [0, 100, 200]
y = [100, 0, 200]

plt.title('Sample Line Plot')
plt.xlabel('X value')
plt.ylabel('Y value')
plt.plot(x, y)
plt.show()
```

### Q2
```python
import matplotlib.pyplot as plt
import seaborn as sns

x = [0, 100, 200]
y = [100, 0, 200]
sns.set(style="whitegrid")
sns.lineplot(x=x, y=y)
plt.title('Line Plot with Whitegrid')
plt.xlabel('X value')
plt.ylabel('Y value')
plt.show()
```

### Q3
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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

df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

df.hist(bins=[1, 3, 5, 7, 9, 11], figsize=(8, 4))

plt.suptitle("Histogram of All Results")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.tight_layout()
plt.show()
```

### Q4
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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

df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

bins = [1, 3, 5, 7, 9, 11]

# ResultA のヒストグラム
plt.hist(df["ResultA"], bins=bins)
plt.title("Histogram of ResultA")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()

# ResultC のヒストグラム
plt.hist(df["ResultC"], bins=bins)
plt.title("Histogram of ResultC")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()
```

### Q5
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

table_data = [
    ["Sato", 60, 65, 66],
    ["Suzuki", 80, 85, 88],
    ["Takahashi", 100, 100, 100],
]
col = ["Name", "SubjectA", "SubjectB", "SubjectC"]

df = pd.DataFrame(table_data, columns=col)
df = df.set_index("Name")

sns.set(style="whitegrid")

df.plot.bar()

plt.title("Scores of Each Subject")
plt.xlabel("Name")
plt.ylabel("Score")

plt.show()
```

### Q6
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

table_data = [
    ["Sato", 60, 65, 66],
    ["Suzuki", 80, 85, 88],
    ["Takahashi", 100, 100, 100],
]
col = ["Name", "SubjectA", "SubjectB", "SubjectC"]

df = pd.DataFrame(table_data, columns=col)
df = df.set_index("Name")

sns.set(style="whitegrid")
df["SubjectA"].plot.bar()

plt.title("Scores of SubjectA")
plt.xlabel("Student")
plt.ylabel("Score")

plt.show()
```

### Q7
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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

df = pd.DataFrame(table_data, columns=col)
df = df.set_index("Month")

sns.set(style="whitegrid")

df.plot()
plt.title("Temperature Change by Region")
plt.xlabel("Month")
plt.ylabel("Temperature (°C)")

plt.show()
```

### Q8
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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

df = pd.DataFrame(table_data, columns=col)
df = df.set_index("Month")

sns.set(style="whitegrid")

df["RegionA"].plot()

plt.title("Temperature of RegionA")
plt.xlabel("Month")
plt.ylabel("Temperature (°C)")

plt.show()
```

### Q9
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

table_data = [
    [35, 62],
    [47, 26],
    [18, 12],
]
col = ["DishA", "DishB"]
idx = ["Like", "Neutral", "Dislike"]

df = pd.DataFrame(table_data, columns=col, index=idx)
sns.set(style="whitegrid")

df["DishA"].plot.pie()

plt.title("Preference for DishA")
plt.show()
```

### Q10
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

table_data = [
    [35, 62],
    [47, 26],
    [18, 12],
]
col = ["DishA", "DishB"]
idx = ["Like", "Neutral", "Dislike"]

df = pd.DataFrame(table_data, columns=col, index=idx)
sns.set(style="whitegrid")

df["DishB"].plot.pie(
    startangle=90,
    counterclock=False,
    labeldistance=0.5
)

plt.title("Preference for DishB")
plt.show()
```

### Q11
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

sns.boxplot(data=df, width=0.5)
plt.title("Height Data of Each Class")
plt.show()

print(df.median())
```

### Q12
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

df.plot.scatter(x="Height", y="Weight", c="b")
plt.title("Relationship between Height and Weight")
plt.xlabel("Height (cm)")
plt.ylabel("Weight (kg)")
plt.show()
```

### Q13
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

df.plot.scatter(x="Height", y="Weight", c="b")

x = df.loc[3, "Height"]
y = df.loc[3, "Weight"]

plt.plot(x, y, c="r", marker="^", markersize=10)

plt.title("Relationship between Height and Weight")
plt.xlabel("Height (cm)")
plt.ylabel("Weight (kg)")
plt.show()
```

### Q14
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

df.plot.scatter(x="Height", y="Weight", c="b")

x = df.loc[3, "Height"]
y = df.loc[3, "Weight"]

plt.plot(x, y, c="r", marker="^", markersize=10)

plt.axvline(x, c="r", linestyle=":")
plt.axhline(y, c="r", linestyle=":")

plt.title("Relationship between Height and Weight (with guides)")
plt.xlabel("Height (cm)")
plt.ylabel("Weight (kg)")

plt.show()
```

### Q15
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

# SubA vs SubB の散布図
df.plot.scatter(x="SubA", y="SubB")
plt.title("SubA vs SubB")
plt.xlabel("SubA")
plt.ylabel("SubB")
plt.show()

# SubA vs SubC の散布図
df.plot.scatter(x="SubA", y="SubC")
plt.title("SubA vs SubC")
plt.xlabel("SubA")
plt.ylabel("SubC")
plt.show()

print("Correlation (SubA vs SubB):", df.corr()["SubA"]["SubB"])
print("Correlation (SubA vs SubC):", df.corr()["SubA"]["SubC"])
```

### Q16
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

# SubA vs SubB（回帰直線付き）
sns.regplot(data=df, x="SubA", y="SubB", line_kws={"color": "g"})
plt.title("SubA vs SubB (Regression)")
plt.xlabel("SubA")
plt.ylabel("SubB")
plt.show()

# SubA vs SubC（回帰直線付き）
sns.regplot(data=df, x="SubA", y="SubC", line_kws={"color": "r"})
plt.title("SubA vs SubC (Regression)")
plt.xlabel("SubA")
plt.ylabel("SubC")
plt.show()
```

### Q17
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

# SubA vs SubB（散布図＋回帰直線＋ヒストグラム）
sns.jointplot(
    data=df,
    x="SubA",
    y="SubB",
    kind="reg",
    line_kws={"color": "g"}
)
plt.show()

# SubA vs SubC（散布図＋回帰直線＋ヒストグラム）
sns.jointplot(
    data=df,
    x="SubA",
    y="SubC",
    kind="reg",
    line_kws={"color": "r"}
)
plt.show()
```

### Q18
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

# 1: 基本的な相関行列ヒートマップ
sns.heatmap(df.corr())
plt.title("Correlation Heatmap (Basic)")
plt.show()

# 2: 相関係数を表示し，色範囲を -1〜1 に固定したヒートマップ
sns.heatmap(
    df.corr(),
    annot=True,
    vmax=1,
    vmin=-1,
    center=0
)
plt.title("Correlation Heatmap (Annotated)")
plt.show()
```

### Q19
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

# 1: 基本的な散布図行列
sns.pairplot(data=df)
plt.show()

# 2: 回帰直線付きの散布図行列
sns.pairplot(data=df, kind="reg")
plt.show()
```

### Q20
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

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
df = pd.DataFrame(table_data, columns=col)

sns.set(style="whitegrid")

print("Basic Statistics (describe)")
print(df.describe())

plt.figure()
for subject in df.columns:
    plt.hist(df[subject], bins=10, alpha=0.5, label=subject)

plt.title("Histogram of Scores (All Subjects)")
plt.xlabel("Score")
plt.ylabel("Frequency")
plt.legend()
plt.show()

df.plot.scatter(x="SubA", y="SubB")
plt.title("SubA vs SubB")
plt.xlabel("SubA")
plt.ylabel("SubB")
plt.show()

df.plot.scatter(x="SubA", y="SubC")
plt.title("SubA vs SubC")
plt.xlabel("SubA")
plt.ylabel("SubC")
plt.show()

plt.figure()
sns.heatmap(df.corr(), annot=True, vmax=1, vmin=-1, center=0)
plt.title("Correlation Matrix Heatmap")
plt.xlabel("Subject")
plt.ylabel("Subject")
plt.show()
```