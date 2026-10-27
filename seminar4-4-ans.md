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

##### 問題5
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
  text = f.read()

ans = 0
words = ["先生", "私", "奥さん", "Ｋ"]
for word in words:
    count = text.count(word)
    if ans < count:
        ans = count
        most_common_word = word
    print(f"{word}: {count}回")

print(f"最も多く出現する言葉: {most_common_word}")
```

##### 問題6
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))
for token in tokens[:50]:
    print(token)
```

##### 問題7
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))
for token in tokens[:100]:
    print(token.surface)
```

##### 問題8
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))
for token in tokens[:50]:
    pos = token.part_of_speech.split(",")[0]
    print(f"{token.surface} : {pos}")
```

##### 問題9
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

nouns = []
for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns[:50])
```

##### 問題10
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

verbs = []
for token in tokens:
    if token.part_of_speech.startswith("動詞"):
        verbs.append(token.surface)

for word in verbs[:50]:
    print(word)
```

##### 問題11
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

verbs_base = []

for token in tokens:
    if token.part_of_speech.startswith("動詞"):
        verbs_base.append(token.base_form)

for word in verbs_base[:50]:
    print(word)
```

##### 問題12
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

adjectives = []

for token in tokens:
    if token.part_of_speech.startswith("形容詞"):
        adjectives.append(token.surface)

for word in adjectives:
    print(word)
```

##### 問題13
```python
from janome.tokenizer import Tokenizer
from collections import Counter

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

nouns = []

for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

noun_counter = Counter(nouns)

for word, count in noun_counter.most_common():
    print(f"{word}: {count}回")

print('top 20')
for word, count in noun_counter.most_common(20):
    print(f"{word}: {count}回")
```
