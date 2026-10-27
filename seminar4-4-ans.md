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

##### 問題14
```python
from janome.tokenizer import Tokenizer
from collections import Counter

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

# 表層形を保存するリスト
verb_surface = []

# 基本形を保存するリスト
verb_base = []

for token in tokens:
    if token.part_of_speech.startswith("動詞"):
        verb_surface.append(token.surface)
        verb_base.append(token.base_form)

# 出現回数を数える
surface_counter = Counter(verb_surface)
base_counter = Counter(verb_base)

# 表層形の上位20語を表示
print("表層形 top 20")

for word, count in surface_counter.most_common(20):
    print(f"{word}: {count}回")

print()

# 基本形の上位20語を表示
print("基本形 top 20")

for word, count in base_counter.most_common(20):
    print(f"{word}: {count}回")
```

##### 問題15
```python
from janome.tokenizer import Tokenizer

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

nouns = []
verbs = []
adjectives = []

for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)
    elif token.part_of_speech.startswith("動詞"):
        verbs.append(token.surface)
    elif token.part_of_speech.startswith("形容詞"):
        adjectives.append(token.surface)

print(f"名詞 : {len(nouns)}語")
print(f"動詞 : {len(verbs)}語")
print(f"形容詞 : {len(adjectives)}語")
```

##### 問題16
```python
from janome.tokenizer import Tokenizer
from collections import Counter

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

stop_words = {
    "こと",
    "もの",
    "よう",
    "これ",
    "それ",
    "ため",
    "ところ"
}

nouns = []

for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

# ストップワード除去前
noun_counter = Counter(nouns)

print("ストップワード除去前 top 20")

for word, count in noun_counter.most_common(20):
    print(f"{word}: {count}回")

print()

# ストップワードを除去
filtered_nouns = []

for word in nouns:
    if word not in stop_words:
        filtered_nouns.append(word)

# ストップワード除去後
filtered_counter = Counter(filtered_nouns)

print("ストップワード除去後 top 20")

for word, count in filtered_counter.most_common(20):
    print(f"{word}: {count}回")
```

##### 問題17
```python
from collections import Counter

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

characters = ["先生", "私", "奥さん", "Ｋ"]

sentences = text.split("。")

character_counter = Counter()

for sentence in sentences:
    for character in characters:
        if character in sentence:
            character_counter[character] += 1

for character, count in character_counter.most_common():
    print(f"{character} : {count}文")
```

##### 問題18
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

sentences = text.split("。")

teacher_sentences = []

for sentence in sentences:
    if "先生" in sentence:
        teacher_sentences.append(sentence)

for sentence in teacher_sentences[:10]:
    print(sentence)
    print()
```

##### 問題19
```python
from janome.tokenizer import Tokenizer
from collections import Counter
import matplotlib.pyplot as plt
import japanize_matplotlib

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

nouns = []

for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

noun_counter = Counter(nouns)

top10 = noun_counter.most_common(10)

words = []
counts = []

for word, count in top10:
    words.append(word)
    counts.append(count)

plt.bar(words, counts)

plt.xlabel("単語")
plt.ylabel("出現回数")
plt.title("『こころ』における名詞の出現頻度")

plt.show()

```

##### 問題19
```python
from janome.tokenizer import Tokenizer
from collections import Counter
import matplotlib.pyplot as plt
import japanize_matplotlib

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

nouns = []

for token in tokens:
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

noun_counter = Counter(nouns)

top10 = noun_counter.most_common(10)

words = []
counts = []

for word, count in top10:
    words.append(word)
    counts.append(count)

plt.bar(words, counts)

plt.xlabel("単語")
plt.ylabel("出現回数")
plt.title("『こころ』における名詞の出現頻度")

plt.show()
```

##### 問題20
```python
from janome.tokenizer import Tokenizer
from wordcloud import WordCloud
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm
import japanize_matplotlib

with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

tokenizer = Tokenizer()
tokens = list(tokenizer.tokenize(text))

stop_words = {
    "こと",
    "もの",
    "よう",
    "これ",
    "それ",
    "ため",
    "ところ"
}

words = []

for token in tokens:

    if token.part_of_speech.startswith("名詞") or token.surface == "Ｋ":
        word = token.surface

    elif token.part_of_speech.startswith("動詞"):
        word = token.base_form

    elif token.part_of_speech.startswith("形容詞"):
        word = token.base_form

    else:
        continue

    if word not in stop_words:
        words.append(word)

word_text = " ".join(words)

font_path = fm.findfont("IPAexGothic")

wordcloud = WordCloud(
    font_path=font_path,
    width=1000,
    height=600,
    background_color="white"
).generate(word_text)

plt.figure(figsize=(12, 7))
plt.imshow(wordcloud, interpolation="bilinear")
plt.axis("off")
plt.show()

```
