

```python
import numpy as np
# 创建三维数组
arr = np.zeros((3,3,3))
# 将数组转换为矩阵
mat = np.matrix(arr)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-3-0fa2d8bccefa> in <module>()
          3 arr = np.zeros((3,3,3))
          4 # 将数组转换为矩阵
    ----> 5 mat = np.matrix(arr)
    

    d:\program files\python\python36\lib\site-packages\numpy\matrixlib\defmatrix.py in __new__(subtype, data, dtype, copy)
        224             else:
        225                 intype = N.dtype(dtype)
    --> 226             new = data.view(subtype)
        227             if intype != data.dtype:
        228                 return new.astype(intype)
    

    d:\program files\python\python36\lib\site-packages\numpy\matrixlib\defmatrix.py in __array_finalize__(self, obj)
        269                 return
        270             elif (ndim > 2):
    --> 271                 raise ValueError("shape too large to be a matrix.")
        272         else:
        273             newshape = self.shape
    

    ValueError: shape too large to be a matrix.


# 所以需要注意的是：矩阵只能是二维的，而数组可以是多维的。


```python
# 创建数组的方法
alist = [1,2,3,4]
arr = np.array(alist)

arr2 = np.zeros(5)

arr3 = np.arange(12)

arr4 = np.arange(4,12)

# 100 steps from 0 to 1
arr5 = np.linspace(0, 1, 100)
```


```python
img = np.zeros((5,5))
print(img)
```

    [[ 0.  0.  0.  0.  0.]
     [ 0.  0.  0.  0.  0.]
     [ 0.  0.  0.  0.  0.]
     [ 0.  0.  0.  0.  0.]
     [ 0.  0.  0.  0.  0.]]
    


```python
cube = np.zeros((4,4,4))
print(cube)
```

    [[[ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]]
    
     [[ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]]
    
     [[ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]]
    
     [[ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]
      [ 0.  0.  0.  0.]]]
    

### 数组进行转换：
#### reshape 函数和 shape函数
    



```python
arr1d = np.arange(12)
print(arr1d)
```

    [ 0  1  2  3  4  5  6  7  8  9 10 11]
    


```python
# 将arr1d转换为3X4的数组
arr2d = arr1d.reshape(3, 4)
print(arr2d)
```

    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]]
```python
# 将arr1d转换为3维的
arr3d = arr1d.reshape(2, 2, 3)
print(arr3d)
```

    [[[ 0  1  2]
      [ 3  4  5]]
    
     [[ 6  7  8]
      [ 9 10 11]]]
    

### 索引与切片

