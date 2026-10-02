### ゼミナールⅣ 3回目
#### 形態素解析続き

#### Janomeで文章の特徴を調べてみよう

ここまで，Janomeを使って文章を形態素解析し，
- 単語を取り出す
- 品詞を調べる
- 名詞や動詞だけを選ぶ
- 基本形を確認する

といった処理を学んできました．

ここからは，形態素解析の結果を使って，

**文章の中にどのような言葉が使われているのか**

を少し詳しく調べていきます．

最初は短い文章を使って練習してみましょう．

---

##### 1. 文章を形態素解析してみよう

まずは，次の文章を使います．

```python
text = "私は札幌の大学でPythonを勉強しています．"
```

Janomeを使って形態素解析してみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

for token in tokenizer.tokenize(text):
    print(token)
```

実行すると，それぞれの単語について詳しい情報が表示されます．

例えば，

```text
札幌    名詞,固有名詞,地域,一般,*,*,札幌,サッポロ,サッポロ
```

のような結果が得られます．

---

##### 2. 必要な情報だけを取り出そう

Janomeの解析結果には，たくさんの情報が含まれています．

最初は，次の3つを使えれば十分です．

| 書き方 | 意味 |
|---|---|
| `token.surface` | 文章中に実際に現れた形 |
| `token.base_form` | 単語の基本形 |
| `token.part_of_speech` | 品詞の情報 |

例えば，

```python
for token in tokenizer.tokenize(text):
    print(f"単語：{token.surface}")
    print(f"基本形：{token.base_form}")
    print(f"品詞：{token.part_of_speech}")
    print()
```

のように書くと，必要な情報を分けて表示できます．

---

##### 3. 表層形と基本形の違い

文章の中では，同じ動詞でも形が変わります．

例えば，

```text
食べる
食べた
食べます
食べて
```

は，すべて同じ「食べる」という動詞です．

文章中に実際に現れた形を **表層形** といいます．

一方，その単語のもとの形を **基本形** といいます．

Janomeでは，

```python
token.surface
```

で表層形，

```python
token.base_form
```

で基本形を取得できます．

例えば，

```python
text = "昨日はラーメンを食べました．"

for token in tokenizer.tokenize(text):
    print(f"{token.surface} → {token.base_form}")
```

とすると，

```text
食べ → 食べる
```

のように確認できます．

---

##### 4. 動詞だけを取り出そう

文章の中から動詞だけを取り出してみます．

```python
text = "朝起きて，ご飯を食べて，大学へ行きます．"
```

次のように書きます．

```python
for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.surface)
```

実行結果の例：

```text
起き
食べ
行き
```

---

##### なぜ startswith() を使うのか

Janomeの品詞情報は，

```text
動詞,自立,*,*
```

のように，詳しい情報を含んだ文字列になっています．

そのため，

```python
token.part_of_speech == "動詞"
```

では一致しません．

そこで，

```python
token.part_of_speech.startswith("動詞")
```

を使って，

**「品詞情報が『動詞』から始まっているか」**

を調べています．

---

##### 5. 動詞を基本形で取り出そう

次は，動詞を基本形で表示してみます．

```python
text = "昨日はカレーを食べました．今日はラーメンを食べます．"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.base_form)
```

実行結果の例：

```text
食べる
食べる
```

文章中では，

```text
食べました
食べます
```

と形が違っています．

しかし基本形にすると，

```text
食べる
```

として同じ単語として扱うことができます．

文章を分析するときには，基本形を使うと便利です．

---

##### 6. 名詞だけを取り出そう

今度は，名詞だけを取り出してみましょう．

```python
text = "私は札幌の大学でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        print(token.surface)
```

実行結果の例：

```text
私
札幌
大学
Python
勉強
```

このように，必要な品詞だけを選ぶことができます．

---

##### 7. 名詞をリストに保存しよう

取り出した名詞をあとで使いたい場合は，リストに保存すると便利です．

```python
text = "北海道には札幌，函館，旭川などの都市があります．"

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns)
```

実行結果の例：

```text
['北海道', '札幌', '函館', '旭川', '都市']
```

リストにしておくと，

- 単語の数を数える
- 出現回数を調べる
- WordCloudを作る

といった処理につなげることができます．

---

##### 8. 名詞の数を数えてみよう

名詞をリストに保存したら，

```python
len()
```

を使って数を調べることができます．

```python
text = "私は札幌の大学でPythonと自然言語処理を勉強しています．"

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(f"名詞は{len(nouns)}個あります．")
```

---

##### 9. 少し細かい品詞情報を見てみよう

Janomeでは，「名詞」よりもさらに細かい情報を確認できます．

例えば，

```text
勉強    名詞,サ変接続,*,*
```

のような情報です．

`token.part_of_speech` を表示すると確認できます．

```python
text = "大学で研究や勉強をしています．"

for token in tokenizer.tokenize(text):
    print(token.surface, token.part_of_speech)
```

このように，同じ名詞でもさらに細かい種類に分かれています．

最初はすべて覚える必要はありません．

まずは，

```text
名詞
動詞
形容詞
助詞
```

といった大きな分類が分かれば十分です．

---

##### 10. 「名詞 + の + 名詞」を探してみよう

日本語では，

```text
大学の授業
北海道の観光
Pythonの勉強
```

のような表現がよく使われます．

このような，

```text
名詞 + の + 名詞
```

という並びを探してみましょう．

例えば，

```python
text = "私は札幌の大学でPythonの授業を受けています．"
```

を使います．

まず，解析結果をリストにします．

```python
tokens = list(tokenizer.tokenize(text))
```

そのあと，3つずつ順番に確認します．

```python
for i in range(len(tokens) - 2):

    word1 = tokens[i]
    word2 = tokens[i + 1]
    word3 = tokens[i + 2]

    if (word1.part_of_speech.startswith("名詞")
        and word2.surface == "の"
        and word3.part_of_speech.startswith("名詞")):

        print(word1.surface + "の" + word3.surface)
```

実行結果の例：

```text
札幌の大学
Pythonの授業
```

このプログラムでは，

```text
1つ目が名詞
2つ目が「の」
3つ目が名詞
```

という並びを探しています．

---

##### 11. 連続している名詞をまとめてみよう

形態素解析では，

```text
自然言語処理
```

という言葉が，

```text
自然
言語
処理
```

のように分かれることがあります．

このような場合，連続している名詞をまとめることで，

```text
自然言語処理
```

として扱うことができます．

例えば，

```python
text = "私は自然言語処理を勉強しています．"
```

を使います．

```python
nouns = []

for token in tokenizer.tokenize(text):

    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

    else:
        if len(nouns) >= 2:
            print("".join(nouns))

        nouns = []
```

ここで，

```python
"".join(nouns)
```

を使うと，

```text
自然
言語
処理
```

のように分かれている文字列を，

```text
自然言語処理
```

としてつなげることができます．

---

##### 12. ここまでのまとめ

ここまでの処理を整理すると，

```text
文章
 ↓
Janomeで形態素解析
 ↓
単語を取り出す
 ↓
品詞を確認する
 ↓
必要な単語だけを選ぶ
 ↓
リストに保存する
```

という流れになります．

よく使う書き方は次のとおりです．

| 書き方 | 意味 |
|---|---|
| `token.surface` | 文章中の単語 |
| `token.base_form` | 単語の基本形 |
| `token.part_of_speech` | 品詞情報 |
| `startswith("名詞")` | 名詞かどうか調べる |
| `startswith("動詞")` | 動詞かどうか調べる |
| `append()` | リストに追加する |
| `len()` | 要素の数を数える |
| `"".join()` | 文字列をつなぐ |

この次は，取り出した単語について，

**「どの単語が何回登場するのか」**

を調べていきます．

#### Janomeで文章の特徴を見える化しよう

ここまで，Janomeを使って文章から名詞や動詞を取り出し，
必要な単語をリストに保存する方法を学びました．

ここからは，その単語を使って，

- どの単語がよく登場するのか
- よく登場する単語をグラフで見る
- 単語の出現回数のばらつきを見る
- 単語のランキングと出現回数の関係を見る
- WordCloudで文章の特徴を見える化する

といった処理を行います．

---

##### 13. 単語の出現回数を数えよう

まずは，文章の中でそれぞれの単語が何回登場したかを調べてみます．

次の文章を使います．

```python
text = """
Pythonを勉強しています．
Pythonはデータ分析にも使えます．
Pythonを使って自然言語処理を勉強します．
大学ではPythonの授業もあります．
"""
```

Janomeで名詞だけを取り出します．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns)
```

実行すると，名詞だけがリストに保存されます．

例えば，

```text
['Python', '勉強', 'Python', 'データ', '分析', ...]
```

のような形になります．

---

##### 14. Counterを使って回数を数える

単語の出現回数を数えるには，`Counter` が便利です．

最初に読み込みます．

```python
from collections import Counter
```

そして，先ほど作った `nouns` を使います．

```python
counts = Counter(nouns)

print(counts)
```

実行結果の例：

```text
Counter({'Python': 4, '勉強': 2, 'データ': 1, '分析': 1})
```

これは，

```text
Python → 4回
勉強 → 2回
データ → 1回
分析 → 1回
```

登場したことを表しています．

---

##### 15. 出現回数の多い順に並べよう

`Counter` には，出現回数の多い順に並べるための `most_common()` という機能があります．

```python
print(counts.most_common())
```

例えば，

```text
[('Python', 4), ('勉強', 2), ('データ', 1), ('分析', 1)]
```

のように表示されます．

上位10語だけを取り出したい場合は，

```python
print(counts.most_common(10))
```

と書きます．

---

##### 16. 上位10語を見やすく表示しよう

そのまま表示すると，

```text
[('Python', 4), ('勉強', 2), ...]
```

のようになります．

f-stringを使うと，もっと見やすくできます．

```python
top10 = counts.most_common(10)

for word, count in top10:
    print(f"{word} : {count}回")
```

実行結果の例：

```text
Python : 4回
勉強 : 2回
データ : 1回
分析 : 1回
```

ここでは，

```python
for word, count in top10:
```

によって，

```text
単語
出現回数
```

を1つずつ取り出しています．

---

##### 17. 上位10語を棒グラフにしよう

数字だけでなく，グラフにすると違いが分かりやすくなります．

まず，上位10語を取り出します．

```python
top10 = counts.most_common(10)
```

次に，単語と出現回数を別々のリストにします．

```python
words = []
frequencies = []

for word, count in top10:
    words.append(word)
    frequencies.append(count)
```

確認してみましょう．

```python
print(words)
print(frequencies)
```

例えば，

```text
['Python', '勉強', '大学', '授業']
[4, 2, 1, 1]
```

のようになります．

---

##### 棒グラフを表示する

グラフを描くために `matplotlib` を使います．

```python
import matplotlib.pyplot as plt
```

棒グラフは `plt.bar()` を使います．

```python
plt.bar(words, frequencies)

plt.xlabel("単語")
plt.ylabel("出現回数")
plt.title("よく使われている単語")

plt.show()
```

棒が高いほど，その単語が文章中に多く登場していることを表します．

---

##### 18. なぜグラフにするのか

例えば，

```text
Python : 20回
大学 : 12回
授業 : 8回
学生 : 5回
```

という数字だけを見ても違いは分かります．

しかし，棒グラフにすると，

- どの単語が特に多いのか
- 1位と2位にどのくらい差があるのか
- 上位の単語にどの程度偏りがあるのか

が直感的に分かります．

文章分析では，

**数字を出すだけでなく，グラフで見える形にする**

ことも重要です．

---

##### 19. 単語の出現回数のばらつきを見てみよう

文章中の単語には，

- 何度も登場する単語
- 数回だけ登場する単語
- 1回しか登場しない単語

があります．

例えば，

```text
Python : 10回
大学 : 5回
授業 : 3回
自然 : 1回
言語 : 1回
処理 : 1回
```

のような場合です．

ここでは，

**「何回登場する単語が，どのくらい存在するのか」**

を調べてみます．

---

##### 20. 出現回数だけを取り出そう

`Counter` に保存されている出現回数だけを取り出してみます．

```python
frequency_values = list(counts.values())

print(frequency_values)
```

例えば，

```text
[10, 5, 3, 1, 1, 1]
```

のようなリストになります．

これは，

```text
ある単語は10回
ある単語は5回
ある単語は3回
3種類の単語は1回ずつ
```

登場していることを表しています．

---

##### 21. ヒストグラムを作ろう

出現回数の分布を見るには，ヒストグラムを使います．

```python
import matplotlib.pyplot as plt

plt.hist(frequency_values)

plt.xlabel("単語の出現回数")
plt.ylabel("単語の種類数")
plt.title("単語の出現回数の分布")

plt.show()
```

このグラフでは，

- 横軸：単語が何回登場したか
- 縦軸：その回数登場した単語が何種類あるか

を表しています．

---

##### 22. ヒストグラムから何が分かる？

長い文章では，

**1回しか登場しない単語が非常に多い**

ということがあります．

一方で，

**何度も繰り返し登場する単語は少数**

であることも多いです．

ヒストグラムを使うと，このような，

**単語の出現回数のばらつき**

を見ることができます．

---

##### 23. 単語をランキングにしてみよう

次は，単語を出現回数の多い順に並べます．

```python
ranking = counts.most_common()
```

例えば，

```text
1位 Python 20回
2位 大学 15回
3位 学生 10回
4位 授業 8回
```

のようなイメージです．

順位を作ります．

```python
ranks = range(1, len(ranking) + 1)
```

出現回数も取り出します．

```python
frequencies = []

for word, count in ranking:
    frequencies.append(count)
```

---

##### 24. 順位と出現回数をグラフにしよう

順位と出現回数の関係をグラフにしてみます．

```python
import matplotlib.pyplot as plt

plt.plot(ranks, frequencies)

plt.xlabel("順位")
plt.ylabel("出現回数")
plt.title("単語の順位と出現回数")

plt.show()
```

このグラフを見ると，

**順位が下がるほど，出現回数も少なくなっていく**

ことが分かります．

---

##### 25. 両対数グラフにしてみよう

文章中の単語の順位と出現回数には，特徴的な関係が現れることがあります．

その関係を見やすくするために，グラフの両方の軸を対数表示にしてみます．

```python
plt.plot(ranks, frequencies)

plt.xscale("log")
plt.yscale("log")

plt.xlabel("順位")
plt.ylabel("出現回数")
plt.title("単語順位と出現回数")

plt.show()
```

ここでは，対数の詳しい数学的な意味を覚える必要はありません．

まずは，

**よく使われる少数の単語は何度も登場し，多くの単語は少ししか登場しない**

という特徴をグラフで確認してみましょう．

---

##### 26. WordCloudを作ってみよう

最後に，単語の出現回数を見た目で分かりやすくする方法として，WordCloudを作ります．

WordCloudでは，

**たくさん登場する単語ほど大きく表示されます．**

例えば，

```text
Python
大学
授業
学生
分析
```

といった単語が，出現回数に応じて異なる大きさで表示されます．

---

##### 27. WordCloudのライブラリを準備する

WordCloudを使うためには，最初に `wordcloud` というライブラリをインストールします．

Google Colabでは，次のコードを実行します．

```python
!pip install wordcloud
```

`pip` は，Pythonで使うライブラリをインストールするための仕組みです．

今回は，

```text
wordcloud
```

というライブラリを追加しています．

---

##### WordCloudを読み込む

インストールが終わったら，Pythonから使えるようにします．

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt
```

ここでは，

- `WordCloud` → WordCloudを作るために使う
- `matplotlib.pyplot` → 作成したWordCloudを画面に表示する

という役割があります．


WordCloudを使うために，ライブラリを読み込みます．

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt
```

Google Colabでは，日本語を表示するために日本語フォントも準備します．

```python
!apt-get -y install fonts-noto-cjk
```

インストールした日本語フォントの場所を指定します．

```python
font_path = "/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc"
```

---

##### 28. 名詞をWordCloud用の文章にしよう

これまで作った名詞のリスト，

```python
nouns
```

を使います．

例えば，

```python
print(nouns)
```

の結果が，

```text
['Python', '大学', '授業', 'Python', '分析']
```

だったとします．

WordCloudで使いやすいように，単語を空白でつないだ1つの文字列にします．

```python
wordcloud_text = " ".join(nouns)

print(wordcloud_text)
```

実行結果：

```text
Python 大学 授業 Python 分析
```

`join()` は，リストの中にある文字列をつなぐために使います．

---

##### 29. WordCloudを表示しよう

WordCloudを作成します．

```python
wc = WordCloud(
    font_path=font_path,
    width=800,
    height=400,
    background_color="white"
).generate(wordcloud_text)
```

作成したWordCloudを表示します．

```python
plt.figure(figsize=(10, 5))

plt.imshow(wc)
plt.axis("off")

plt.show()
```

大きく表示されている単語ほど，文章中に多く登場していることを表します．

---

##### 30. WordCloudの見方

WordCloudは，

**文章の中でよく登場する単語を直感的に確認する**

ために便利です．

例えば，

```text
猫
主人
人間
家
学校
```

などが大きく表示されていれば，

その文章ではこれらの言葉がよく使われていることが分かります．

ただし，

**大きく表示されている単語が，必ずしも文章の中で最も重要な単語とは限りません．**

WordCloudが表しているのは，

**単語の意味の重要度ではなく，主に出現回数**

です．

---

##### 31. 不要な単語を除いてみよう

文章を分析すると，

```text
こと
もの
これ
それ
ため
```

のような，文章の特徴を見る上ではあまり必要ではない単語が多く登場することがあります．

このような単語を除外することもできます．

例えば，

```python
stop_words = ["こと", "もの", "これ", "それ", "ため"]
```

というリストを作ります．

そして，名詞を取り出すときに，

```python
nouns = []

for token in tokenizer.tokenize(text):

    if token.part_of_speech.startswith("名詞"):

        if token.surface not in stop_words:
            nouns.append(token.surface)
```

とします．

ここでは，

```python
token.surface not in stop_words
```

によって，

**その単語が除外する単語のリストに入っていないか**

を確認しています．

このように，分析から除外する単語を **ストップワード** と呼ぶことがあります．

---

##### 32. ファイルの文章からWordCloudを作ろう

最後に，これまで学習した内容を組み合わせてみましょう．

例えば，`sample.txt` に文章が保存されているとします．

まず，ファイルを読み込みます．

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()
```

次に，Janomeで形態素解析し，名詞だけを取り出します．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)
```

名詞を空白でつなぎます．

```python
wordcloud_text = " ".join(nouns)
```

WordCloudを作ります．

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt

font_path = "/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc"

wc = WordCloud(
    font_path=font_path,
    width=800,
    height=400,
    background_color="white"
).generate(wordcloud_text)
```

最後に表示します．

```python
plt.figure(figsize=(10, 5))

plt.imshow(wc)
plt.axis("off")

plt.show()
```

---

## 全体をまとめると

```python
from janome.tokenizer import Tokenizer
from wordcloud import WordCloud
import matplotlib.pyplot as plt

tokenizer = Tokenizer()

with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

wordcloud_text = " ".join(nouns)

font_path = "/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc"

wc = WordCloud(
    font_path=font_path,
    width=800,
    height=400,
    background_color="white"
).generate(wordcloud_text)

plt.figure(figsize=(10, 5))
plt.imshow(wc)
plt.axis("off")
plt.show()
```

このプログラムでは，

```text
ファイルを読み込む
        ↓
Janomeで形態素解析する
        ↓
名詞だけを取り出す
        ↓
単語を空白でつなぐ
        ↓
WordCloudを作る
        ↓
結果を表示する
```

という流れになっています．

---

### まとめ

ここまでの流れをまとめると，

```text
文章
 ↓
Janomeで形態素解析
 ↓
必要な単語を取り出す
 ↓
Counterで出現回数を数える
 ↓
頻出語を確認する
 ↓
グラフで表示する
 ↓
WordCloudで見える化する
```

となります．

文章を分析するときには，

**数値で確認する方法**

と，

**グラフやWordCloudで見える化する方法**

の両方を使うと，文章の特徴を理解しやすくなります．

---

### 今回使った主な機能

| 書き方 | 意味 |
|---|---|
| `Counter()` | 単語の出現回数を数える |
| `most_common()` | 出現回数の多い順に並べる |
| `counts.values()` | 出現回数だけを取り出す |
| `plt.bar()` | 棒グラフを描く |
| `plt.hist()` | ヒストグラムを描く |
| `plt.plot()` | グラフを描く |
| `plt.xscale("log")` | 横軸を対数表示にする |
| `plt.yscale("log")` | 縦軸を対数表示にする |
| `" ".join()` | 単語を空白でつなぐ |
| `WordCloud()` | WordCloudを作る |
| `stop_words` | 分析から除外する単語をまとめる |
| `not in` | リストの中に含まれていないか調べる |

---

##### 次にできること

ここまでできるようになると，長い文章を使った分析にも挑戦できます．

例えば，

- 小説の頻出語を調べる
- 青空文庫の作品をWordCloudにする
- 2つの小説を比較する
- ニュース記事の特徴を比べる
- アンケートの自由記述を分析する

といったことができます．

まずは短い文章で分析の流れを確認し，そのあと実際の長い文章に挑戦してみましょう．

# 練習問題：「問わずがたりの洋酒外史」を分析してみよう
以下の問題では，配布した「問わずがたりの洋酒外史」の文章を `text` に読み込んで使用してください．

---

#### 問1: 文章を形態素解析してみよう

文章全体をJanomeで形態素解析し，それぞれの単語について，

- 表層形
- 基本形
- 品詞

を表示してください．

ヒント：

```python
token.surface
token.base_form
token.part_of_speech
```

を使います．

---

#### 問2: 文章から名詞を取り出そう

文章全体から**名詞だけ**を取り出して表示してください．

例えば，この文章には，

```text
ウイスキー
洋酒
ビール
日本
恵比寿
```

などの名詞が含まれています．

`startswith("名詞")` を使って判定してください．

---

#### 問3: 名詞をリストに保存しよう

問2で取り出した名詞を，

```python
nouns
```

というリストに保存してください．

その後，

```python
print(nouns)
```

で内容を確認してください．

さらに，

```python
len(nouns)
```

を使って，**文章中に名詞が全部で何個登場したか**を調べてください．

---

#### 問4: 動詞を基本形で取り出そう

文章から動詞だけを取り出し，**基本形**で表示してください．

文章中では，同じ動詞でも形が変化している場合があります．

基本形を利用することで，同じ動詞として扱いやすくなります．

ヒント：

```python
token.base_form
```

を使って表示してください．

---

#### 問5: 名詞の出現回数を調べよう

問3で作成した `nouns` を使って，それぞれの名詞が何回登場したか調べてください．

まず，`Counter` を読み込みます．

```python
from collections import Counter
```

次に，

```python
counts = Counter(nouns)
```

として名詞の出現回数を集計してください．

その後，

```python
print(counts)
```

で結果を確認してください．

---

#### 問6: 頻出名詞上位10語を調べよう

`most_common()` を使って，文章中で多く登場する**名詞上位10語**を調べてください．

結果を，

```text
ビール : ○回
ウイスキー : ○回
日本 : ○回
...
```

のような形式で表示してください．

ヒント：

```python
top10 = counts.most_common(10)

for word, count in top10:
    print(f"{word} : {count}回")
```

を参考にしてください．

結果を見て，**どのような単語が上位に入っているか**確認してください．

---

#### 問7: 頻出名詞を棒グラフにしよう

問6で調べた頻出名詞上位10語について，棒グラフを作成してください．

横軸を**単語**，縦軸を**出現回数**とします．

例えば，

```python
plt.xlabel("単語")
plt.ylabel("出現回数")
plt.title("問わずがたりの洋酒外史の頻出語")
```

などを設定してみましょう．

グラフを見て，**特に多く登場している単語**を確認してください．

---

#### 問8: 単語の出現回数の分布を調べよう

次のコードを使って，各名詞の出現回数だけを取り出してください．

```python
frequency_values = list(counts.values())
```

その後，

```python
plt.hist(frequency_values)
```

を使ってヒストグラムを作成してください．

作成したグラフを見て，

**「何度も登場する単語」と「1回や2回しか登場しない単語」のどちらが多いか**

考えてみてください．

---

#### 問9: 不要な単語を除いてみよう

頻出語を確認すると，文章の内容を考えるうえではあまり重要ではない単語が含まれることがあります．

例えば，

```python
stop_words = [
    "こと",
    "もの",
    "これ",
    "それ",
    "よう",
    "ため"
]
```

のようなストップワードを設定してください．

ストップワードを除外して，もう一度頻出名詞上位10語を調べてください．

さらに，

**ストップワードを除く前と後で，結果がどのように変化したか**

確認してください．

---

#### 問10: WordCloudを作って文章の特徴を考えよう

ストップワードを除いた名詞を使ってWordCloudを作成してください．

まず，

```python
wordcloud_text = " ".join(nouns)
```

によって名詞を1つの文字列につなぎます．

その後，`WordCloud` を使って文章を可視化してください．

完成したWordCloudと問6・問7の結果を見ながら，以下のことについて考えると，解析に繋がります．

> この文章では，どのような話題が中心になっているでしょうか．  
> 頻出する単語を具体的に挙げながら，100～150字程度で説明してください．
