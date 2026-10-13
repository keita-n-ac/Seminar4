#### 解答例
##### 問題1
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = '私は札幌で勉強しています。'
for token in tokenizer.tokenize(text):
    print(token)
```

##### 問題2
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "今日は大学でPythonを勉強します。"
for token in tokenizer.tokenize(text):
    print(token.surface)
```

##### 問題3
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "札幌は北海道の都市です。"
for token in tokenizer.tokenize(text):
    print(token.surface, ":", token.part_of_speech)
```

##### 問題4
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "私は映画を見ることが好きです。"
for token in tokenizer.tokenize(text):
    print(f"単語：{token.surface}")
```

##### 問題5
```python
from janome.tokenizer import Tokenizer
tokenizer = Tokenizer()
text = "今日はPythonを勉強します。"
count = 0

for token in tokenizer.tokenize(text):
    count += 1

print(f"形態素の数は{count}個です。")
```

##### 問題6
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "私は札幌の大学でPythonを勉強しています。"
for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        print(token.surface)

```

##### 問題7
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "私は学校へ行って、本を読みます。"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.surface)
```

##### 問題8
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "今日は天気が良く、とても暖かいです。"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("形容詞"):
        print(token.surface)
```

##### 問題9
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = "北海道には美しい自然があります。"

for token in tokenizer.tokenize(text):
    result = token.part_of_speech.startswith("名詞")
    print(f"{token.surface} : {result}")
```

##### 問題10
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "北海道には札幌、函館、旭川などの都市があります。"
nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns)
```

##### 問題11
```python

```

##### 問題12
```python

```

##### 問題13
```python

```

##### 問題14
```python

```

##### 問題15
```python

```

##### 問題10
```python

```
