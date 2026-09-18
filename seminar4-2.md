### ゼミナールⅣ 2回目
#### 形態素解析準備
これまで，Pythonで文字列やファイルを扱う方法を学びました．
次は，文章の中にどのような単語が含まれているのかを調べてみます．
そのために使うのが **形態素解析** です．

---

#### 形態素解析とは

人間は文章を見ると，自然に単語の区切りを理解できます．

例えば，

```text
私は札幌でPythonを勉強しています．
```

という文章を見ると，

```text
私
は
札幌
で
Python
を
勉強
し
て
い
ます
．
```

のように，いくつかの単位に分けて考えることができます．
しかし，コンピュータにとって日本語の文章は，最初は単なる文字の並びです．
日本語には英語のように単語と単語の間に空白がないため，

```text
私は札幌でPythonを勉強しています．
```

だけを見ても，

**どこからどこまでが1つの単語なのか**

を判断する必要があります．
このように，文章を意味のある小さな単位に分け，それぞれの品詞などを調べる処理を **形態素解析** といいます．

---

#### 形態素とは

形態素とは，文章を構成する小さな単位のことです．

例えば，

```text
私は大学で勉強しています．
```

という文章を形態素に分けると，おおよそ次のようになります．

```text
私
は
大学
で
勉強
し
て
い
ます
．
```

それぞれについて，

- 名詞
- 動詞
- 助詞
- 助動詞
- 記号

などの情報も調べることができます．

---

#### Janomeとは

Pythonで日本語の形態素解析を行う方法はいくつかあります．

今回は **Janome（ジャノメ）** というライブラリを使います．

Janomeは，Pythonだけで動作する日本語形態素解析ライブラリです．

比較的簡単にインストールできるため，初めて形態素解析を学ぶ場合にも使いやすいライブラリです．

今回はGoogle Colab上でJanomeを使います．

---

# Janomeをインストールする

Google Colabでは，最初にJanomeをインストールします．

次のコードを実行してください．

```python
!pip install janome
```

`pip` は，Pythonのライブラリをインストールするための仕組みです．

今回は，

```text
janome
```

というライブラリをインストールしています．

Google Colabでは，先頭に `!` を付けることで，Pythonのプログラムではなく，システム上のコマンドを実行できます．

---

#### Janomeを読み込む

インストールが終わったら，JanomeをPythonから使えるようにします．

```python
from janome.tokenizer import Tokenizer
```

これは，

**Janomeの中にあるTokenizerという機能を使います**

という意味です．

---

#### Tokenizerを準備する

次に，形態素解析を行うための準備をします．

```python
tokenizer = Tokenizer()
```

これで，

```python
tokenizer
```

という変数を使って形態素解析を行えるようになります．

最初は，

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
```

をセットで覚えておけば大丈夫です．

---

#### 実際に形態素解析してみよう

次の文章を解析してみます．

```python
text = "私は札幌でPythonを勉強しています．"
```

形態素解析を行うには，`tokenize()` を使います．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(token)
```

実行すると，それぞれの単語について詳しい情報が表示されます．

例えば，

```text
私      名詞,...
は      助詞,...
札幌    名詞,...
で      助詞,...
Python  名詞,...
を      助詞,...
勉強    名詞,...
し      動詞,...
て      助詞,...
い      動詞,...
ます    助動詞,...
．      記号,...
```

のような結果が得られます．

---

#### tokenとは

次の部分を見てみましょう．

```python
for token in tokenizer.tokenize(text):
    print(token)
```

`tokenizer.tokenize(text)` によって，文章がいくつかの単位に分けられます．

その1つ1つを，

```python
token
```

という変数に順番に入れています．

つまり，

```python
for token in tokenizer.tokenize(text):
```

は，

**「解析した結果を1つずつ取り出す」**

という意味です．

---

#### 単語だけを表示する

詳しい情報ではなく，単語だけを表示したい場合は，

```python
token.surface
```

を使います．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(token.surface)
```

実行結果の例：

```text
私
は
札幌
で
Python
を
勉強
し
て
い
ます
．
```

`surface` は，文章中に実際に現れた単語を表します．

---

#### 品詞を調べる

それぞれの単語が，

- 名詞
- 動詞
- 助詞
- 形容詞

などのどの種類なのかを調べることもできます．

Janomeでは，

```python
token.part_of_speech
```

を使います．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(token.surface, token.part_of_speech)
```

実行結果の例：

```text
私 名詞,代名詞,一般,*
は 助詞,係助詞,*,*
札幌 名詞,固有名詞,地域,一般
で 助詞,格助詞,一般,*
Python 名詞,一般,*,*
を 助詞,格助詞,一般,*
勉強 名詞,サ変接続,*,*
し 動詞,自立,*,*
て 助詞,接続助詞,*,*
い 動詞,非自立,*,*
ます 助動詞,*,*,*
． 記号,句点,*,*
```

---

#### 表形式で見てみよう

少し見やすくするために，f-stringを使って表示することもできます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(f"{token.surface}: {token.part_of_speech}")
```

このように，これまで学んだf-stringも形態素解析で使うことができます．

---

#### 基本形を覚えよう

Janomeを使った形態素解析の基本は次の形です．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "解析したい文章"

for token in tokenizer.tokenize(text):
    print(token.surface)
```

まずは，

1. `Tokenizer` を読み込む
2. `Tokenizer()` を準備する
3. `tokenize()` で文章を解析する
4. `token.surface` で単語を取り出す

という流れを覚えておきましょう．

---

#### ファイルから文章を読み込んで解析する

これまで学んだファイル入出力と組み合わせることもできます．

例えば，`sample.txt` に文章が保存されている場合，

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    print(token.surface)
```

と書くことができます．

このプログラムでは，

1. ファイルを読み込む
2. 文章を変数 `text` に入れる
3. Janomeで形態素解析する
4. 単語を1つずつ表示する

という処理を行っています．

---

#### 形態素解析で何ができる？

形態素解析を使うと，文章の中に含まれる単語を調べることができます．

例えば，

- どの単語が多く使われているか
- 名詞だけを取り出す
- 動詞だけを取り出す
- 文章の特徴を調べる
- WordCloudを作る

といったことができるようになります．

このあと，形態素解析した結果から，

**名詞だけを取り出す**

といった処理を行っていきます．

---

#### 形態素解析まとめ

形態素解析とは，

**文章を単語などの小さな単位に分け，それぞれの情報を調べる処理**

です．

今回はJanomeを使います．

Google Colabでは，最初に，

```python
!pip install janome
```

でインストールします．

そして，

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
```

で形態素解析の準備をします．

基本的な解析方法は，

```python
for token in tokenizer.tokenize(text):
    print(token.surface)
```

です．

ここまでできれば，

**ファイルを読み込む → 文章を形態素解析する → 必要な単語を取り出す**

という自然言語処理の基本的な流れができるようになります．

#### 応用例: 名詞だけを取り出す方法
Janomeでは，それぞれの単語について品詞の情報を調べることができます．
例えば，次のプログラムを実行してみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌の大学でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(token.surface, token.part_of_speech)
```

実行すると，次のような結果が表示されます．

```text
私 名詞,代名詞,一般,*
は 助詞,係助詞,*,*
札幌 名詞,固有名詞,地域,一般
の 助詞,連体化,*,*
大学 名詞,一般,*,*
で 助詞,格助詞,一般,*
Python 名詞,一般,*,*
を 助詞,格助詞,一般,*
勉強 名詞,サ変接続,*,*
し 動詞,自立,*,*
て 助詞,接続助詞,*,*
い 動詞,非自立,*,*
ます 助動詞,*,*,*
． 記号,句点,*,*
```

`token.part_of_speech` には，

```text
名詞,一般,*,*
```

や，

```text
名詞,固有名詞,地域,一般
```

のように，品詞に関する詳しい情報が文字列として入っています．

---

##### 最初の部分が大きな品詞を表す

例えば，

```text
名詞,一般,*,*
```

では，最初の

```text
名詞
```

が大きな品詞を表しています．

同じように，

```text
動詞,自立,*,*
```

であれば，

```text
動詞
```

が大きな品詞です．

そのため，名詞だけを取り出したい場合には，

**「品詞の情報が `名詞` から始まっているか」**

を調べればよいことになります．

---

# startswith()とは

`startswith()` は，

**文字列が指定した文字から始まっているかを調べる**

ための機能です．

例えば，

```python
text = "Pythonを勉強しています"

print(text.startswith("Python"))
```

とすると，

```text
True
```

と表示されます．

これは，

```text
Pythonを勉強しています
```

という文字列が，

```text
Python
```

から始まっているためです．

一方，

```python
print(text.startswith("Java"))
```

とすると，

```text
False
```

となります．

---

##### Janomeで名詞かどうかを調べる

Janomeでは，

```python
token.part_of_speech
```

に，

```text
名詞,一般,*,*
```

のような文字列が入っています．

そこで，

```python
token.part_of_speech.startswith("名詞")
```

と書くことで，

**品詞情報が「名詞」から始まっているか**

を調べることができます．

名詞であれば，

```text
True
```

名詞でなければ，

```text
False
```

になります．

---

##### if文と組み合わせる

名詞だけを表示したい場合には，if文と組み合わせます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

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

このプログラムでは，

```python
if token.part_of_speech.startswith("名詞"):
```

によって，

**「もし，この単語の品詞が名詞から始まっていたら」**

という条件を指定しています．

そして，

```python
print(token.surface)
```

によって，その単語を表示しています．

---

##### なぜ == "名詞" ではないの？

例えば，次のように書きたくなるかもしれません．

```python
if token.part_of_speech == "名詞":
```

しかし，`token.part_of_speech` に入っているのは，

```text
名詞
```

だけではありません．

実際には，

```text
名詞,一般,*,*
```

や，

```text
名詞,固有名詞,地域,一般
```

のような詳しい情報が入っています．

そのため，

```python
token.part_of_speech == "名詞"
```

では一致しません．

そこで，

```python
token.part_of_speech.startswith("名詞")
```

を使って，

**「最初が名詞ならOK」**

と判断しています．

---

##### 動詞を取り出す場合

同じ方法で，動詞だけを取り出すこともできます．

```python
for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.surface)
```

形容詞なら，

```python
for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("形容詞"):
        print(token.surface)
```

と書けます．

---

##### まとめ

```python
token.part_of_speech
```

には，

```text
名詞,一般,*,*
```

のような詳しい品詞情報が入っています．

そのため，

```python
token.part_of_speech.startswith("名詞")
```

と書くことで，

**その単語が名詞かどうか**

を調べることができます．

つまり，

```python
if token.part_of_speech.startswith("名詞"):
    print(token.surface)
```

は，

**「もしその単語が名詞なら，その単語を表示する」**

という意味になります．


#### Janomeを使った形態素解析 サンプルプログラム15選

ここでは，Janomeを使った形態素解析を，簡単なものから順番に練習します．

最初に，Google ColabでJanomeをインストールします．

```python
!pip install janome
```

---

##### 1. 文章を形態素解析する

まずは，文章をそのまま形態素解析してみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌でPythonを勉強しています．"

for token in tokenizer.tokenize(text):
    print(token)
```

単語と品詞などの情報が表示されます．

---

##### 2. 単語だけを表示する

`surface` を使うと，文章中に現れた単語だけを取り出すことができます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "今日は大学で勉強します．"

for token in tokenizer.tokenize(text):
    print(token.surface)
```

実行結果の例：

```text
今日
は
大学
で
勉強
し
ます
．
```

---

##### 3. 単語と品詞を表示する

`part_of_speech` を使うと，単語の品詞を確認できます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "今日は天気が良いです．"

for token in tokenizer.tokenize(text):
    print(token.surface, token.part_of_speech)
```

---

##### 4. f-stringを使って見やすく表示する

これまで学んだf-stringと組み合わせることもできます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は映画を見ることが好きです．"

for token in tokenizer.tokenize(text):
    print(f"単語：{token.surface}")
```

---

##### 5. 単語と品詞を見やすく表示する

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "札幌は北海道の都市です．"

for token in tokenizer.tokenize(text):
    print(f"{token.surface} : {token.part_of_speech}")
```

---

##### 6. 単語の数を数える

形態素解析によって，いくつの単語に分けられたか調べてみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "今日はPythonを勉強します．"

count = 0

for token in tokenizer.tokenize(text):
    count = count + 1

print(f"単語の数は{count}個です．")
```

---

##### 7. 単語をリストに入れる

解析した単語をリストに保存することもできます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は札幌で勉強しています．"

words = []

for token in tokenizer.tokenize(text):
    words.append(token.surface)

print(words)
```

実行結果の例：

```text
['私', 'は', '札幌', 'で', '勉強', 'し', 'て', 'い', 'ます', '．']
```

---

##### 8. 名詞だけを表示する

品詞が「名詞」の単語だけを取り出してみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

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

---

##### 9. 動詞だけを表示する

今度は「動詞」だけを取り出してみます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は学校へ行って，本を読みます．"

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("動詞"):
        print(token.surface)
```

---

##### 10. 名詞をリストに保存する

名詞だけをリストに入れてみましょう．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "北海道には札幌や函館などの都市があります．"

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

print(nouns)
```

---

##### 11. 基本形を表示する

動詞などは，文章の中では形が変化することがあります．

例えば，

```text
食べます
食べた
食べて
```

は，すべて「食べる」という動詞が変化したものです．

Janomeでは `base_form` を使うと基本形を確認できます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "私は昨日ラーメンを食べました．"

for token in tokenizer.tokenize(text):
    print(f"{token.surface} → {token.base_form}")
```

---

##### 12. 名詞の出現回数を数える

`Counter` を使うと，単語が何回登場したか数えることができます．

```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
Pythonを勉強します．
Pythonは便利です．
今日はPythonの授業です．
"""

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

print(counts)
```

---

##### 13. 最も多く登場する単語を調べる

`most_common()` を使うと，よく登場する単語を確認できます．

```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

text = """
私は映画が好きです．
休日には映画を見ます．
特に日本の映画が好きです．
"""

words = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        words.append(token.surface)

counts = Counter(words)

print(counts.most_common())
```

上位3つだけ表示する場合は，

```python
print(counts.most_common(3))
```

と書きます．

---

##### 14. テキストファイルを読み込んで形態素解析する

これまで学習したファイル入出力と組み合わせてみましょう．

例えば，`file2.txt` に次の文章が入っているとします．

```text
私は札幌の大学で勉強しています．
Pythonを使って自然言語処理を学んでいます．
```

Pythonでは次のように読み込みます．

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

with open("file2.txt", "r", encoding="utf-8") as file:
    text = file.read()

for token in tokenizer.tokenize(text):
    print(token.surface)
```

このプログラムでは，

1. ファイルを読み込む
2. 文章を `text` に入れる
3. Janomeで解析する
4. 単語を表示する

という処理を行っています．

---

##### 15. ファイルから名詞を取り出して回数を数える

最後に，これまでの内容を組み合わせてみましょう．

```python
from janome.tokenizer import Tokenizer
from collections import Counter

tokenizer = Tokenizer()

with open("file2.txt", "r", encoding="utf-8") as file:
    text = file.read()

nouns = []

for token in tokenizer.tokenize(text):
    if token.part_of_speech.startswith("名詞"):
        nouns.append(token.surface)

counts = Counter(nouns)

for word, count in counts.most_common():
    print(f"{word} : {count}回")
```

実行結果の例：

```text
Python : 3回
大学 : 2回
札幌 : 1回
授業 : 1回
```

このプログラムでは，

- ファイル入出力
- 形態素解析
- if文
- リスト
- Counter
- f-string

を組み合わせています．

---

# まとめ

今回のサンプルでは，次のことを行いました．

| 番号 | 内容 |
|---|---|
| 1 | 文章を形態素解析する |
| 2 | 単語だけを表示する |
| 3 | 品詞を表示する |
| 4 | f-stringと組み合わせる |
| 5 | 単語と品詞を見やすく表示する |
| 6 | 単語数を数える |
| 7 | 単語をリストに保存する |
| 8 | 名詞だけを取り出す |
| 9 | 動詞だけを取り出す |
| 10 | 名詞をリストに保存する |
| 11 | 基本形を表示する |
| 12 | 単語の出現回数を数える |
| 13 | よく登場する単語を調べる |
| 14 | ファイルを読み込んで解析する |
| 15 | ファイルから名詞を抽出して頻度を調べる |

まずは，

```python
for token in tokenizer.tokenize(text):
    print(token.surface)
```

を基本形として覚えておきましょう．

そのあと，

```python
token.part_of_speech
```

を使って品詞を調べたり，

```python
if token.part_of_speech.startswith("名詞"):
```

のように条件を付けることで，必要な単語だけを取り出せるようになります．

### Janome 形態素解析 練習問題

ここでは、Janomeを使った形態素解析について練習します。

最初にGoogle ColabでJanomeをインストールしておきます。

```python
!pip install janome
```

基本となる準備は次のとおりです。

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
```

---

#### 基礎問題

##### 問題1：文章を形態素解析しよう

次の文章をJanomeで形態素解析し、解析結果をすべて表示してください。

```python
text = "私は札幌で勉強しています。"
```

`tokenizer.tokenize()` を使います。

---

##### 問題2：単語だけを表示しよう

次の文章を形態素解析し、`surface` を使って単語だけを表示してください。

```python
text = "今日は大学でPythonを勉強します。"
```

実行結果の例：

```text
今日
は
大学
で
Python
を
勉強
し
ます
。
```

---

##### 問題3：単語と品詞を表示しよう

次の文章を形態素解析してください。

```python
text = "札幌は北海道の都市です。"
```

それぞれの単語について、

```text
単語 : 品詞情報
```

の形式で表示してください。

`token.surface` と `token.part_of_speech` を使用します。

---

##### 問題4：f-stringを使って表示しよう

次の文章を形態素解析します。

```python
text = "私は映画を見ることが好きです。"
```

f-stringを使って、

```text
単語：私
単語：は
単語：映画
```

のように表示してください。

---

##### 問題5：形態素の数を数えよう

次の文章を形態素解析してください。

```python
text = "今日はPythonを勉強します。"
```

形態素が全部でいくつあるか数えて、

```text
形態素の数は○個です。
```

と表示してください。

---

#### 品詞を使ってみよう

##### 問題6：名詞だけを表示しよう

次の文章を形態素解析してください。

```python
text = "私は札幌の大学でPythonを勉強しています。"
```

名詞だけを表示してください。

次の条件を使用します。

```python
token.part_of_speech.startswith("名詞")
```

---

##### 問題7：動詞だけを表示しよう

次の文章を形態素解析してください。

```python
text = "私は学校へ行って、本を読みます。"
```

動詞だけを表示してください。

ヒント：

```python
token.part_of_speech.startswith("動詞")
```

---

##### 問題8：形容詞だけを表示しよう

次の文章を形態素解析してください。

```python
text = "今日は天気が良く、とても暖かいです。"
```

形容詞だけを表示してください。

---

##### 問題9：名詞かどうかを表示しよう

次の文章を形態素解析します。

```python
text = "北海道には美しい自然があります。"
```

それぞれの単語について、

```text
北海道 : True
に : False
```

のように、

```python
token.part_of_speech.startswith("名詞")
```

の結果を表示してください。

---

##### 問題10：名詞をリストに保存しよう

次の文章を形態素解析してください。

```python
text = "北海道には札幌、函館、旭川などの都市があります。"
```

名詞だけを、

```python
nouns = []
```

というリストに追加してください。

最後にリスト全体を表示してください。

---

#### 少し発展してみよう

##### 問題11：名詞の数を数えよう

次の文章を形態素解析してください。

```python
text = "私は札幌の大学でPythonと自然言語処理を勉強しています。"
```

名詞だけを数えて、

```text
名詞は○個あります。
```

と表示してください。

---

##### 問題12：基本形を表示しよう

次の文章を形態素解析してください。

```python
text = "昨日はラーメンを食べました。今日はカレーを食べます。"
```

それぞれの単語について、

```text
食べ → 食べる
```

のように、

**文章中の形 → 基本形**

を表示してください。

`token.base_form` を使用します。

---

##### 問題13：動詞の基本形だけを表示しよう

次の文章を形態素解析してください。

```python
text = "朝起きて、ご飯を食べて、大学へ行きました。"
```

動詞だけを選び、その基本形を表示してください。

実行結果の例：

```text
起きる
食べる
行く
```

---

##### 問題14：名詞と動詞だけを表示しよう

次の文章を形態素解析してください。

```python
text = "学生が図書館で本を読んでいます。"
```

名詞または動詞の場合だけ表示してください。

ヒント：

```python
if 条件1 or 条件2:
```

を使うことができます。

---

##### 問題15：名詞を1行で表示しよう

次の文章を形態素解析してください。

```python
text = "札幌では雪まつりや時計台などの観光地が有名です。"
```

名詞だけをリストに保存したあと、

```python
" ".join(nouns)
```

を使って、次のように1行で表示してください。

```text
札幌 雪 まつり 時計 台 観光 地
```

※ 実際の分割結果はJanomeの解析結果によって異なる場合があります。

---

#### 単語の出現回数を調べよう

##### 問題16：単語の出現回数を数えよう

次の文章を使用します。

```python
text = """
Pythonを勉強します。
Pythonは便利です。
今日はPythonの授業です。
"""
```

名詞だけをリストに保存してください。

そのあと、

```python
from collections import Counter
```

を使って、名詞の出現回数を数えてください。

最後に結果を表示してください。

---

##### 問題17：最も多い名詞を表示しよう

次の文章を使用します。

```python
text = """
私は映画が好きです。
休日には映画を見ます。
特に日本の映画が好きです。
音楽も好きです。
"""
```

名詞を取り出して `Counter` で数え、

```python
most_common(1)
```

を使って、最も多く登場する名詞を調べてください。

---

##### 問題18：出現回数の上位3語を表示しよう

次の文章を使用します。

```python
text = """
大学ではPythonを勉強しています。
Pythonを使ってデータ分析をします。
Pythonを使った自然言語処理にも興味があります。
大学の授業でもデータを扱います。
"""
```

名詞の出現回数を調べ、上位3語を表示してください。

ヒント：

```python
counts.most_common(3)
```

を使用します。

---

#### ファイル入出力と組み合わせよう

##### 問題19：テキストファイルを形態素解析しよう

次の内容を `sample.txt` に保存してください。

```text
私は札幌の大学で勉強しています。
Pythonを使って自然言語処理を学んでいます。
```

これまで学習した `with open()` を使ってファイルを読み込みます。

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    text = file.read()
```

読み込んだ文章をJanomeで形態素解析し、すべての単語を表示してください。

---

##### 問題20：ファイルの頻出名詞を調べよう

`sample.txt` に複数の文章が保存されているとします。

次の処理を行うプログラムを作成してください。

1. `with open()` でファイルを読み込む
2. Janomeで形態素解析する
3. 名詞だけを取り出す
4. 名詞をリストに保存する
5. `Counter` で出現回数を数える
6. 出現回数の多い順に上位5語を表示する

表示例：

```text
Python : 5回
大学 : 3回
授業 : 3回
学生 : 2回
データ : 2回
```

表示にはf-stringを使ってください。

---

#### チャレンジ問題

余裕がある人は、次の問題にも挑戦してみましょう。

次の文章を分析します。

```python
text = """
私は大学でPythonを勉強しています。
Pythonを使うと文章を分析できます。
自然言語処理では文章から単語を取り出します。
大学の授業ではPythonを使って自然言語処理を学びます。
"""
```

次の処理をすべて行ってください。

1. Janomeで形態素解析する
2. 名詞だけを取り出す
3. 名詞をリストに保存する
4. 名詞の数を表示する
5. `Counter` で出現回数を数える
6. 出現回数の多い上位5語を表示する
7. 名詞を空白でつないで1つの文字列にする

最後の処理には、

```python
" ".join(nouns)
```

を使います。

この処理は、今後 **WordCloud** を作るときにも利用できます。

---

# 今回使った主な機能

| 書き方 | 意味 |
|---|---|
| `Tokenizer()` | 形態素解析の準備 |
| `tokenizer.tokenize(text)` | 文章を形態素解析する |
| `token.surface` | 文章中に現れた単語を取得する |
| `token.part_of_speech` | 品詞情報を取得する |
| `startswith("名詞")` | 品詞情報が「名詞」から始まるか調べる |
| `token.base_form` | 単語の基本形を取得する |
| `append()` | リストに追加する |
| `Counter()` | 単語の出現回数を数える |
| `most_common()` | 出現回数の多い順に取り出す |
| `" ".join()` | 単語を空白でつなぐ |
| `with open()` | ファイルを開いて読み込む |

---

# 学習の流れ

今回の20問は、次の順番で少しずつ難しくなっています。

```text
形態素解析
    ↓
単語の取得
    ↓
品詞の確認
    ↓
名詞・動詞の抽出
    ↓
リストへの保存
    ↓
基本形の取得
    ↓
単語の頻度集計
    ↓
ファイルの文章を解析
```

まずは、次の基本形を自分で書けるようになることを目標にしましょう。

```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()

text = "解析したい文章"

for token in tokenizer.tokenize(text):
    print(token.surface)
```
