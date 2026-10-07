#### 解答例
##### 問題1
```python
name = '田中'
print(f'こんにちは，{name}さん．')
```

##### 問題2
```python
name = '佐藤'
age = 20
print(f'{name}さんは{age}歳です．')
```

##### 問題3
```python
name = '鈴木'
city = '札幌'
print(f'{name}さんの出身地は{city}です．')
```

##### 問題4
```python
item = 'りんご'
price = 150
print(f'{item}の値段は{price}円です．')
```

##### 問題5
```python
x = 10
y = 5
print(f'xは{x}，yは{y}です．')
```

##### 問題6
```python
price = 120
count = 4
print(f'合計金額は{price * count}円です．')
```

##### 問題7
```python
a = 12
b = 8
print(f'{a} + {b} = {a + b}')
```

##### 問題8
```python
score1 = 80
score2 = 90
score3 = 75
average = (score1 + score2 + score3) / 3
print(f'平均点は{average}点です．')
```

##### 問題9
```python
score = 83.4567
print(f'平均点は{score:.2f}点です．')
```

##### 問題10
```python
score1 = 72
score2 = 85
score3 = 91
average = (score1 + score2 + score3) / 3
print(f'3人の平均点は{average:.1f}点です．')
```

##### 問題11
```python
with open('sample.txt', 'r', encoding='utf-8') as file:
    text = file.read()
print(text)
```

##### 問題12
```python
with open('profile.txt', 'r', encoding='utf-8') as file:
    text = file.read()
print(text)
```

##### 問題13
```python
count = 0

with open('sample.txt', 'r', encoding='utf-8') as file:
    for line in file:
        line = line.strip()
        count += len(line)

print(f'文字数は{count}文字です．')
```

##### 問題14
```python
with open('python.txt', 'r', encoding='utf-8') as file:
    text = file.read()

count = text.count('Python')

print(f'Pythonは{count}回登場します．')
```

##### 問題15
```python
with open('sample.txt', 'r', encoding='utf-8') as file:
    for line in file:
        print(line, end='')
```

##### 問題16
```python
with open('sample.txt', 'r', encoding='utf-8') as file:
    for line in file:
        line = line.strip()
        print(line)
```

##### 問題17
```python
with open('result.txt', 'w', encoding='utf-8') as file:
    file.write('Pythonを勉強しています．')
```

##### 問題18
```python
with open('profile.txt', 'w', encoding='utf-8') as file:
    file.write('名前：田中\n')
    file.write('年齢：20\n')
    file.write('出身：札幌\n')
```

##### 問題19
```python
with open('diary.txt', 'a', encoding='utf-8') as file:
    file.write('\nファイル入出力について学びました．')
```

##### 問題20
```python
count = 0

with open('message.txt', 'r', encoding='utf-8') as file:
    for line in file:
        line = line.strip()
        count += len(line)

print(f'このファイルには{count}文字あります．')
```

##### チャレンジ問題
```python
text = ''
length = 0
count = 0

with open('input.txt', 'r', encoding='utf-8') as file:
    for line in file:
        line = line.strip()
        text += line + '\n'
        length += len(line)
        count += line.count('Python')

print('文章：')
print(text)

print(f'文字数：{length}文字')
print(f'Pythonの登場回数：{count}回')
```
