### 1
```python
import numpy as np
print(np.__version__)
```

### 2
```python
import numpy as np
data = np.array([1, 2, 3, 4])
print(data)
```

### 3
```python
import numpy as np
data = np.array([[1, 2, 3], [4, 5, 6]])
print(data.shape)
print(len(data))
```

### 4
```python
import numpy as np
data = np.linspace(0, 1, 6) 
print(data)
```

### 5
```python
import numpy as np
data = np.arange(0, 10, 2)
print(data)
```

### 6
```python
import numpy as np
data = np.array([1, 2, 3, 4])
print(np.square(data))
```

### 7
```python
import numpy as np
data = np.array([1, 2, 3, 4])
print(data ** 2)
```

### 8
```python
import numpy as np
data1 = np.array([1, 7, 5, 2])
data2 = np.array([-3, 3, 1, -2])
print(data1 - data2)
```

### 9
```python
import numpy as np
n2 = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
print(n2[0])
```

### 10
```python
import numpy as np
n2 = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
print(n2[:, 1])
```

### 11
```python
import numpy as np
n2 = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
print(n2[:1, 2:])
```

### 12
```python
import numpy as np
n2 = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
n2_index = np.array([True, False])
data = n2[n2_index]
print(data)
```

### 13
```python
import numpy as np
data = np.array([1, 7, 5, 2])
print(np.max(data))
print(np.min(data))
```

### 14
```python
import numpy as np
data = np.array([1, 7, 5, 2])
data_max = data.max()
data_min = data.min()
data_normal = (data - data_min) / (data_max - data_min)
print(data_normal)
```

### 15
```python
import numpy as np
data1 = np.array([1, 2, 3, 4])
data2 = np.array([10, 20, 30, 40])
data3 = data1 + data2
print(data3)
```

### 16
```python
import numpy as np
data = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
ans = data.sum(axis=1)
print(ans)
```

### 17
```python
import numpy as np
data = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
ans = data.sum(axis=0)
print(ans)
```

### 18
```python
import numpy as np
data = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
ans = data.sum() / data.shape[0] / data.shape[1]
print(ans)
```

### 19
```python
import numpy as np
print(np.zeros((2, 3)))
print(np.ones((2, 3)))
```

### 20
```python
import numpy as np
print(np.random.rand(3, 3))
```

### 21
```python
import numpy as np
print(np.random.randint(0, 10, (2, 5)))
```

### 22
```python
import numpy as np
data = np.random.randint(0, 10, (5, 5))
ans = data.max(axis=0)
print(data)
print(ans)
```

### 23
```python
import numpy as np
data = np.random.rand(3, 3)
data *= 10
print(data)
data = data.astype(int)
print(data)
```

### 24
```python
import numpy as np
data = np.array([1, 2, 3, 4, 5, 6])
print(np.mean(data))
print(np.std(data))
```

### 25
```python
import numpy as np
data1 = np.array([1, 0, 1, 1, 0])
data2 = np.array([1, 1, 1, 0, 0])
matched = (data1 == data2)
count = sum(matched)
total = len(matched)
accuracy = count / total
print('一致数:', count)
print('データ数:', total)
print('一致率:', accuracy)
```
