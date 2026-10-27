#### 解答例

##### 問題1
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

print(text[:500])
```

##### 問題2
```python
count = 0

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    for line in f:
        count += len(line.strip())

print(f"文字数: {count}")
```

##### 問題3
```python
count = 0
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    for line in f:
        count += 1

print(f"行数: {count}")
```


##### 問題4
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
  text = f.read()

count = text.count("先生")
print(f"先生: {count}回")
```

##### 問題4
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
  text = f.read()

words = ["先生", "私", "奥さん", "Ｋ"]
for word in words:
    count = text.count(word)
    print(f"{word}: {count}回")
```

##### 問題5
```python

```
