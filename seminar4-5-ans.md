#### 5回目 解答例

##### 問題1
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

month = [1, 2, 3, 4, 5]
sales = [120, 150, 140, 180, 210]

plt.plot(month, sales, marker="o")

plt.title("月別売上")
plt.xlabel("月")
plt.ylabel("売上")

plt.show()
```

##### 問題2
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

city = ["札幌", "函館", "旭川", "小樽"]
population = [197, 24, 32, 11]

plt.bar(city, population)

plt.title("都市別人口")
plt.xlabel("都市")
plt.ylabel("人口（万人）")

plt.show()
```

##### 問題3
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

product = ["商品A", "商品B", "商品C", "商品D"]
sales = [80, 120, 60, 150]

plt.barh(product, sales)

plt.title("商品別売上")
plt.xlabel("売上")
plt.ylabel("商品")

plt.show()
```

##### 問題4
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

year = [2021, 2022, 2023, 2024, 2025]

sapporo = [120, 150, 180, 220, 250]
hakodate = [90, 110, 130, 150, 170]

plt.plot(year, sapporo, marker="o", label="札幌")
plt.plot(year, hakodate, marker="o", label="函館")

plt.title("観光客数の推移")
plt.xlabel("年")
plt.ylabel("観光客数")

plt.legend()

plt.show()
```

##### 問題5
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

transport = ["自動車", "電車", "バス", "徒歩"]
students = [40, 30, 20, 10]

plt.pie(
    students,
    labels=transport,
    autopct="%1.1f%%"
)

plt.title("通学手段")

plt.show()
```

##### 問題6
```python
transport = ["自動車", "電車", "バス", "徒歩"]
students = [40, 30, 20, 10]

for i in range(len(transport)):
    print(f"{transport[i]}: {students[i]}人")
```

##### 問題7
```python
age = ["10代", "20代", "30代", "40代"]

car = [10, 20, 40, 60]
train = [60, 50, 40, 30]
bus = [30, 30, 20, 10]

bottom_bus = []

for i in range(len(age)):
    bottom_bus.append(car[i] + train[i])

print(bottom_bus)
```

##### 問題8
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

age = ["10代", "20代", "30代", "40代"]

car = [10, 20, 40, 60]
train = [60, 50, 40, 30]
bus = [30, 30, 20, 10]

bottom_train = car

bottom_bus = []

for i in range(len(age)):
    bottom_bus.append(car[i] + train[i])

plt.bar(
    age,
    car,
    label="自動車"
)

plt.bar(
    age,
    train,
    bottom=bottom_train,
    label="電車"
)

plt.bar(
    age,
    bus,
    bottom=bottom_bus,
    label="バス"
)

plt.title("年代別交通手段")
plt.xlabel("年代")
plt.ylabel("割合（%）")

plt.legend()

plt.show()
```

##### 問題9
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

scores = [
    45, 52, 55, 58, 60,
    62, 64, 65, 68, 70,
    72, 73, 75, 78, 80,
    82, 85, 88, 90, 95
]

plt.hist(scores, bins=5)

plt.title("テスト点数の分布")
plt.xlabel("点数")
plt.ylabel("人数")

plt.show()
```

##### 問題10
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

temperature = [15, 18, 20, 23, 25, 28, 30]
sales = [50, 60, 75, 100, 130, 170, 210]

plt.scatter(temperature, sales)

plt.title("気温とアイスクリーム売上")
plt.xlabel("気温（℃）")
plt.ylabel("売上")

plt.show()
```

##### 問題11
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

class_a = [55, 60, 62, 65, 68, 70, 72, 75, 80, 90]
class_b = [40, 50, 55, 60, 65, 70, 80, 85, 90, 98]

plt.boxplot(
    [class_a, class_b],
    tick_labels=["A組", "B組"]
)

plt.title("テスト点数の比較")
plt.ylabel("点数")

plt.show()
```

##### 問題12
```python
import matplotlib.pyplot as plt
import japanize_matplotlib

sales = [120, 160, 140, 210, 230, 190]

months = []

for i in range(len(sales)):
    months.append(i + 1)

print(months)

plt.plot(months, sales, marker="o")

plt.title("月別売上")
plt.xlabel("月")
plt.ylabel("売上")

plt.show()
```

##### 問題13
```python
sales = [120, 160, 140, 210, 230, 190]

for i in range(len(sales)):
    if sales[i] >= 200:
        print(f"{i + 1}月: {sales[i]}")
```

##### 問題14
```python
sales = [120, 160, 140, 210, 230, 190]

high_months = []
high_sales = []

for i in range(len(sales)):
    if sales[i] >= 200:
        high_months.append(i + 1)
        high_sales.append(sales[i])

print(high_months)
print(high_sales)
```


##### 問題15
```python
sales = [120, 160, 140, 210, 230, 190]

high_months = []
high_sales = []

for i in range(len(sales)):
    if sales[i] >= 200:
        high_months.append(i + 1)
        high_sales.append(sales[i])


plt.bar(high_months, high_sales)

plt.title("売上200以上の月")
plt.xlabel("月")
plt.ylabel("売上")

plt.show()
```

##### 問題16
```python
import csv

cities = []
visitors = []
satisfaction = []

with open(
    "tourism.csv",
    "r",
    encoding="utf-8"
) as f:

    reader = csv.reader(f)

    next(reader)

    for row in reader:
        cities.append(row[0])
        visitors.append(int(row[1]))
        satisfaction.append(float(row[2]))

print(cities)
print(visitors)
print(satisfaction)
```

##### 問題17
```python
import csv

cities = []
visitors = []
satisfaction = []

with open(
    "tourism.csv",
    "r",
    encoding="utf-8"
) as f:

    reader = csv.reader(f)

    next(reader)

    for row in reader:
        cities.append(row[0])
        visitors.append(int(row[1]))
        satisfaction.append(float(row[2]))


plt.bar(cities, visitors)

plt.title("都市別観光客数")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

##### 問題18
```python
import csv

cities = []
visitors = []
satisfaction = []

with open(
    "tourism.csv",
    "r",
    encoding="utf-8"
) as f:

    reader = csv.reader(f)

    next(reader)

    for row in reader:
        cities.append(row[0])
        visitors.append(int(row[1]))
        satisfaction.append(float(row[2]))

plt.scatter(visitors, satisfaction)

plt.title("観光客数と満足度")
plt.xlabel("観光客数")
plt.ylabel("満足度")

plt.show()
```

##### 問題19
```python
import csv

cities = []
visitors = []
satisfaction = []

with open(
    "tourism.csv",
    "r",
    encoding="utf-8"
) as f:

    reader = csv.reader(f)

    next(reader)

    for row in reader:
        cities.append(row[0])
        visitors.append(int(row[1]))
        satisfaction.append(float(row[2]))


selected_cities = []
selected_visitors = []

for i in range(len(cities)):
    if visitors[i] >= 200:
        selected_cities.append(cities[i])
        selected_visitors.append(visitors[i])

for i in range(len(selected_cities)):
    print(
        f"{selected_cities[i]}: "
        f"{selected_visitors[i]}人"
    )

plt.bar(
    selected_cities,
    selected_visitors
)

plt.title("観光客数200人以上の都市")
plt.xlabel("都市")
plt.ylabel("観光客数")

plt.show()
```

##### 問題20
```python
import csv
import matplotlib.pyplot as plt
import japanize_matplotlib

months = []
sales = []
customers = []

with open(
    "shop.csv",
    "r",
    encoding="utf-8"
) as f:

    reader = csv.reader(f)

    next(reader)

    for row in reader:
        months.append(int(row[0]))
        sales.append(int(row[1]))
        customers.append(int(row[2]))

# 月別売上
plt.plot(
    months,
    sales,
    marker="o"
)

plt.title("月別売上")
plt.xlabel("月")
plt.ylabel("売上")

plt.show()


# 売上と来店客数
plt.scatter(
    sales,
    customers
)

plt.title("売上と来店客数の関係")
plt.xlabel("売上")
plt.ylabel("来店客数")

plt.show()


# 売上200以上の月
high_months = []
high_sales = []

for i in range(len(months)):

    if sales[i] >= 200:
        high_months.append(months[i])
        high_sales.append(sales[i])


# 結果を表示
for i in range(len(high_months)):
    print(
        f"{high_months[i]}月: "
        f"売上{high_sales[i]}"
    )


# 棒グラフ
plt.bar(
    high_months,
    high_sales
)

plt.title("売上200以上の月")
plt.xlabel("月")
plt.ylabel("売上")

plt.show()
```
