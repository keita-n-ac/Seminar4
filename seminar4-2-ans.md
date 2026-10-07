#### 解答例
##### 問題1
```python
from janome.tokenizer import Tokenizer

tokenizer = Tokenizer()
text = '私は札幌で勉強しています。'
for token in tokenizer.tokenize(text):
    print(token)
```

