#### 解答例

##### 事前準備
- 以下を行うこと．
```
!pip install janome
!pip install matplotlib
!pip install japanize-matplotlib
!pip install wordcloud
!apt-get -y install fonts-noto-cjk
```

##### 問題1
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    print(f"表層形：{token.surface}")
    print(f"基本形：{token.base_form}")
    print(f"品詞：{token.part_of_speech}")
    print()
```

##### 問題2
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        print(token.surface)
```

##### 問題3
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns)

print(f"名詞の数は{len(nouns)}個です。")
```

##### 問題4
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.base_form)
```

##### 問題5
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

print(counts)
```

##### 問題6
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

top10 = counts.most_common(10)

for word, count in top10:
    print(f"{word} : {count}回")
```

##### 問題7
```python
from janome.tokenizer import Tokenizer
from collections import Counter
import matplotlib.pyplot as plt
import japanize_matplotlib

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

top10 = counts.most_common(10)

words = []
frequencies = []

for word, count in top10:
    words.append(word)
    frequencies.append(count)

plt.figure(figsize=(10, 5))

plt.bar(words, frequencies)

plt.xlabel("単語")
plt.ylabel("出現回数")
plt.title("問わずがたりの洋酒外史の頻出語")

plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

##### 問題8
```python
from janome.tokenizer import Tokenizer
from collections import Counter
import matplotlib.pyplot as plt
import japanize_matplotlib

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

frequency_values = list(counts.values())

plt.figure(figsize=(10, 5))

plt.hist(frequency_values)

plt.xlabel("単語の出現回数")
plt.ylabel("単語の種類数")
plt.title("名詞の出現回数の分布")

plt.show()
```

##### 問題9
```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

stop_words = [
    "こと",
    "もの",
    "これ",
    "それ",
    "よう",
    "ため"
]

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

print("ストップワード除外前")

for word, count in counts.most_common(10):
    print(f"{word} : {count}回")

filtered_nouns = []

for word in nouns:
    if word not in stop_words:
        filtered_nouns.append(word)

filtered_counts = Counter(filtered_nouns)

print()
print("ストップワード除外後")

for word, count in filtered_counts.most_common(10):
    print(f"{word} : {count}回")
```

##### 問題10
```python
from janome.tokenizer import Tokenizer
from collections import Counter
from wordcloud import WordCloud
import matplotlib.pyplot as plt

tokenizer = Tokenizer()

with open("whiskey.txt", "r", encoding="utf-8") as file:
    text = file.read()

stop_words = [
    "こと",
    "もの",
    "これ",
    "それ",
    "よう",
    "ため"
]

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        if token.surface not in stop_words:
            nouns.append(token.surface)

counts = Counter(nouns)

print("頻出名詞上位10語")

for word, count in counts.most_common(10):
    print(f"{word} : {count}回")

wordcloud_text = " ".join(nouns)

font_path = "/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc"

wc = WordCloud(
    font_path=font_path,
    width=800,
    height=400,
    background_color="white",
    collocations=False
).generate(wordcloud_text)

plt.figure(figsize=(10, 5))

plt.imshow(wc)
plt.axis("off")

plt.show()
```
