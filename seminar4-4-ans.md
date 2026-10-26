#### 解答例

##### 問題1
```python
with open("kokoro_clean.txt", "r", encoding="utf-8") as f:
    text = f.read()

print(text[:500])
```
