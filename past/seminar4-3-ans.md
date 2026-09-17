## Matplotlib
### 1
```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.show()
```

### 2
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y = x ** 2 
plt.plot(x, y)
plt.show()
```

### 3
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y = x ** 2
plt.title('quadratic function')
plt.xlabel('x')
plt.ylabel('y')
plt.plot(x, y)
plt.show()
```

### 4
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y = x ** 2
plt.title('quadratic function')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y)
plt.show()
```

### 5
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y = x ** 2
plt.title('quadratic function')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y, label='y = x^2')
plt.legend()
plt.show()
```

### 6
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y1 = np.sqrt(x)
y2 = x ** 2
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y1, label='y = sqrt(x)')
plt.plot(x, y2, label='y = x^2')
plt.legend()
plt.show()
```

### 7
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y1 = np.sqrt(x)
y2 = x ** 2

plt.subplot(1, 2, 1)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y1, label='y = sqrt(x)')
plt.legend()

plt.subplot(1, 2, 2)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y2, label='y = x^2')
plt.legend()
plt.show()
```

### 8
```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 11)
y1 = np.sqrt(x)
y2 = x ** 2

plt.figure(figsize=(10, 4)) 

plt.subplot(1, 2, 1)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y1, label='y = sqrt(x)')
plt.legend()

plt.subplot(1, 2, 2)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y2, label='y = x^2')
plt.legend()
plt.show()
```

### 9
```python
import matplotlib.pyplot as plt
x = np.linspace(-10, 10, 101)
y1 = x
y2 = x ** 2
y3 = x ** 3
y4 = x ** 4

plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y1, label='y = x')
plt.legend()

plt.subplot(2, 2, 2)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y2, label='y = x^2')
plt.legend()

plt.subplot(2, 2, 3)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y3, label='y = x^3')
plt.legend()

plt.subplot(2, 2, 4)
plt.title('Graph plot')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.plot(x, y4, label='y = x^4')
plt.legend()

plt.show()
```

### 10
```python
import matplotlib.pyplot as plt
x = np.linspace(-10, 10, 101)
y1 = x
y2 = x ** 2
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.scatter(x, y1, label='y = x')
plt.scatter(x, y2, label='y = x^2')
plt.legend()
plt.show()
```

## scikit-learn
### 1
```python
from sklearn.datasets import load_iris
iris = load_iris()
print(iris)
```

### 2
```python
from sklearn.datasets import load_iris
iris = load_iris()
print(iris.data.shape)
print(iris.data[:5])
```

### 3
```python
from sklearn.datasets import load_iris
iris = load_iris()
print(iris.data.shape)
print(iris.target[:10])
```

### 4
```python
from sklearn.datasets import load_iris
iris = load_iris()
print(iris.feature_names)
```

### 5
```python
from sklearn.datasets import load_iris
iris = load_iris()
x = iris.data
y = iris.target
print(type(x))
print(type(y))
```

### 6
```python
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
iris = load_iris()
x = iris.data
plt.scatter(x[:, 0], x[:, 2])
plt.show()
```

### 7
```python
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
iris = load_iris()
x = iris.data
plt.scatter(x[:,0], x[:,2], c=y, cmap='rainbow')
plt.show()
```

### 8
```python
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
iris = load_iris()
x = iris.data
plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[2])
plt.scatter(x[:,0], x[:,2], c=y, cmap='rainbow')
plt.show()
```

### 9
```python
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
iris = load_iris()
x = iris.data

plt.figure(figsize=(16, 5))

plt.subplot(1, 3, 1)
plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[1])
plt.scatter(x[:,0], x[:,1], c=y, cmap='rainbow')

plt.subplot(1, 3, 2)
plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[2])
plt.scatter(x[:,0], x[:,2], c=y, cmap='rainbow')

plt.subplot(1, 3, 3)
plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[3])
plt.scatter(x[:,0], x[:,3], c=y, cmap='rainbow')

plt.show()
```

### 10
```python
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
iris = load_iris()
x = iris.data

plt.figure(figsize=(20, 20))

for i in range(4):
    for j in range(4):
        k = i * 4 + j + 1
        plt.subplot(4, 4, k)
        plt.xlabel(iris.feature_names[i])
        plt.ylabel(iris.feature_names[j])
        plt.scatter(x[:,i], x[:,j], c=y, cmap='rainbow')
plt.tight_layout()
plt.show()
```
