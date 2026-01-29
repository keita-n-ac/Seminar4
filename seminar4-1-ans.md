### 1)
```python
print(1 + 2)
print(type(1 + 2))
```

### 2)
```python
print(100 / 2)
print(type(100 / 2))
```

### 3)
```python
print(10 // 7, 10 % 7, 10 / 7)
```

### 4)
```python
print(3 + 4 * 2 - 5) # 4 * 2 → 3 + 8 → 11 - 5
```

### 5)
```python
print(type(4))
print(type(4.0))
print(type(4/2))
print(type(4//2))
```

### 6)
```python
print("a" * 3 + "b" * 2 + "!")
```

### 7)
```python
"123" + 456 # 文字列と整数の足し算なのでエラー
```

### 8)
```python
x = int(input())
print(x + 100)
```

### 9)
```python
print(int(3.99))
print(float(10))
print(str(12.5))
```

### 10)
```python
x = int(input())
print(x ** 3)
```

### 11)
```python
w = 10
w = w + 1 
print(w)
w = 10
w +=  1 
print(w)
```

### 12)
```python
a = 2
a = a * 3 # a = 6
a += 4    # a = 10
a //= 3
print(a)
```

### 13)
```python
x = 10
print((x >= 10) and (x % 2 == 1))
```

### 14)
```python
x = 1
print(x < 10)
print(x > 10)
```

### 15)
```python
x = 9
if x % 2 == 1:
    print('xは奇数です')
```

### 16)
```python
x = 10
if x % 2 == 1:
    print('xは奇数です')
else:
    print('xは偶数です')
```

### 17)
```python
x = 5
if x % 3 == 0:
    print('xは3の倍数')
elif x % 3 == 1:
    print('x+2は3の倍数')
else:
    print('x+1は3の倍数')
```

### 18)
```python
x = 12
y = 3.4
print(x, y, sep='\n')
```

### 19)
```python
s = '文字列のサンプル'
print('文字列の長さ:', len(s))
```

### 20)
```python
i2 = int(10.01)
i3 = int('123')
f2 = float(12)
f3 = float('123')
print(i2)
print(i3)
print(f2)
print(f3)
```

### 21)
```python
s1 = 'I like an apple'
s2 = s1.upper() # s1の文字列をすべて大文字にする
print(s2)
```

### 22)
```python
s1 = 'I like an apple'
s2 = 'apple'
s3 = 'pen'
p1 = s1.find(s2) # s1の何文字目にappleがあるかを調べる
p2 = s1.find(s3) # s1の何文字目にorangeがあるかを調べる
print(p1)
print(p2)
```

### 23)
```python
l1 = [1, 3, 5, 7, 9]
print(l1[0])
print(l1[len(l1)//2])
print(l1[-1])
```

### 24)
```python
l1 = [1, 3, 5, 7, 9]
print(l1[1:4])
print(l1[:2])
print(l1[2:])
print(l1[:4])
```

### 25)
```python
data = ['First', 'Second', 'Third']
print('要素数:', len(data))
```

### 26)
```python
data1 = [1, 3, 5, 7, 9]
data2 = ['First', 'Second', 'Third']
print(data1 + data2)
```

### 27)
```python
s1 = 'I like an apple'
print(s1[0])
print(s1[7])
print(s1[-1])
print(s1[10:15])
```

### 28)
```python
data = []
data.append('First')
data.append('Second')
data.append('Third')
print(data)
```

### 29)
```python
l2 = ['First','Second','Third']
data1 = 'Second'
if data1 in l2:
    print(data1, 'は存在します')
else:
    print(data1, 'は存在しません')
data2 ='Forth'
if data2 in l2:
    print(data2, 'は存在します')
else:
    print(data2, 'は存在しません')
```

### 30)
```python
data = ['First', 'Second', 'Third']
for i in data:
    print(i)
```

### 31)
```python
data = ['1st', '2nd', '3rd', '4th', '5th', '6th', '7th', '8th', '9th', '10th', '11th', '12th']
for i in range(12):
    print(i, data[i])
```

### 32)
```python
t1 = (1, 3, 5, 7, 9)
print(type(t1), t1)
print(type((1,)), (1,))
print(type((1)), (1))
```

### 33)
```python
t1 = (1, 3, 5, 7, 9)
print(t1[1])
print(t1[1:3])
```

### 34)
```
TypeError: 'tuple' object does not support item assignment
```

### 35)
```python
t1 = (1, 3, 5, 7, 9)
l1 = list(t1)
l1[1] = 0
print(l1)
```

### 36)
```python
x, y = 2, 4
print('x =', x)
print('y =', y)
```

### 37)
```python
data = [('T254',12),('A727',6),('T256',4),('T254',10),('A726',7),('A727',4)]

for key, value in data:
    print('key =', key, ', value =', value)
```

### 38)
```python
s1 = {5, 2, 1, 2, 3, 9, 3, 4}
print(s1)
```

### 39)
```python
l5 = [5, 2, 1, 2, 3, 9, 3, 4]
s5 = set(l5)
l5 = list(s5)
print(l5)
```

### 40)
```python
d1 = {'T254':'男の子用食器セット','T256':'女の子用食器セット','A726':'目覚まし時計（緑）','A727':'目覚まし時計（赤）','A728':'目覚まし時計（ピンク）'}
print(d1['A726'])
```

### 41)
```python
d1 = {'T254':'男の子用食器セット','T256':'女の子用食器セット','A726':'目覚まし時計（緑）','A727':'目覚まし時計（赤）','A728':'目覚まし時計（ピンク）'}

d1['T257'] = '大人用食器セット'
d1['A726'] = '目覚まし時計（青）'
del d1['A728']

print(d1)
```

### 42)
```python
d1 = {'T254':'男の子用食器セット','T256':'女の子用食器セット','A726':'目覚まし時計（緑）','A727':'目覚まし時計（赤）','A728':'目覚まし時計（ピンク）'}

d1['T257'] = '大人用食器セット'
d1['A726'] = '目覚まし時計（青）'
del d1['A728']

print(d1.keys())
k1 = 'T256'
c1 = k1 in d1.keys()
print(c1)
k2 = 'T257'
c2 = k2 in d1.keys()
print(c2)
```

### 43)
```python
def printHello(name):
    print('Hello, ' + name)

n = input()
printHello(n)
```

### 44)
```python
def getAdd2(num1, num2):
    return num1 + num2

a = int(input())
b = int(input())
print(getAdd2(a, b))
```

### 45)
```python
def f(x):
    y = x ** 2 - 2 * x
    return y

print(f(1))
print(f(2))
print(f(3))
```

### 46)
```python
def head(s, n):
    r = s[0:n]
    return r

s1 = 'ABCDEFG'
n1 = 4

h1 = head(s1, n1)
print(h1)
```

### 47)
```python
def div(s):
    p = s.find('@')  # @の場所を求める
    pre = s[:p]      # @の前を求める
    post = s[p+1:]   # @の後を求める
    return pre, post # コンマ区切りで複数を戻り値にする

s1 = 'abc@xyz.co.jp'
p1, p2 = div(s1) # 複数を受け取るようにする

print('@の前:', p1)
print('@の後:', p2)
```

### 48)
```python
def print_type_value(x):
    print('変数名:', x)
    print('型名:', type(x))

data = 'ABC123'
print_type_value(data)
```

### 49)
```python
s1 = 'サンプル文字列'
for i, s in enumerate(s1):
    print(i+1, '番目の文字は', s, 'です')
```

### 50)
```python
cabins = ['B5', 'C22', 'G6']
data1 = [x[0] for x in cabins]
data2 = [len(x) for x in cabins]
print(data1)
print(data2)
data3 = [9] * 100
print(data3)
```








