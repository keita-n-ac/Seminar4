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
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌の大学でPythonと自然言語処理を勉強しています。"

count = 0

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        count = count + 1

print(f"名詞は{count}個あります。")
```

##### 問題12
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "昨日はラーメンを食べました。今日はカレーを食べます。"

for token in tokenizer.tokenize(text):
    print(f"{token.surface} → {token.base_form}")
```

##### 問題13
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "朝起きて、ご飯を食べて、大学へ行きました。"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.base_form)
```

##### 問題14
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "学生が図書館で本を読んでいます。"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞") or token.part_of_speech.startswith("動詞"):
        print(token.surface)
```

##### 問題15
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "札幌では雪まつりや時計台などの観光地が有名です。"

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

result = " ".join(nouns)

print(result)
```

##### 問題16
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
Pythonを勉強します。
Pythonは便利です。
今日はPythonの授業です。
"""

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

print(counts)
```

##### 問題17
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
私は映画が好きです。
休日には映画を見ます。
特に日本の映画が好きです。
音楽も好きです。
"""

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

result = counts.most_common(1)

print(result)
```

##### 問題18
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
大学ではPythonを勉強しています。
Pythonを使ってデータ分析をします。
Pythonを使った自然言語処理にも興味があります。
大学の授業でもデータを扱います。
"""

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

result = counts.most_common(3)

print(result)
```

##### 問題19
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = """私は札幌の大学で勉強しています。
Pythonを使って自然言語処理を学んでいます。
"""

with open("sample.txt", "w", encoding="utf-8") as file:
    file.write(text)

with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    print(token.surface)
```

##### 問題20
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

for word, count in counts.most_common(5):
    print(f"{word} : {count}回")
```

##### チャレンジ問題
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
私は大学でPythonを勉強しています。
Pythonを使うと文章を分析できます。
自然言語処理では文章から単語を取り出します。
大学の授業ではPythonを使って自然言語処理を学びます。
"""

# 名詞を保存するリストを作成
nouns = []

# 形態素解析して名詞だけを取り出す
for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

# 名詞のリストを表示
print("名詞のリスト")
print(nouns)

# 名詞の数を表示
print(f"名詞の数は{len(nouns)}個です。")

# 名詞の出現回数を数える
counts = Counter(nouns)

# 出現回数が多い上位5語を表示
print("出現回数の上位5語")

for word, count in counts.most_common(5):
    print(f"{word} : {count}回")

# 名詞を空白でつないで文字列にする
result = " ".join(nouns)

# 作成した文字列を表示
print("名詞をつないだ文字列")
print(result)
```
