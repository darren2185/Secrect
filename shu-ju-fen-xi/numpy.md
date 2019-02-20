# Numpy

### Numpy Use Guide

numpy是科学计算的基本包，其最大对象为ndarray，必须熟悉其所有方法及属性，注意区别python中array对象（仅用于一维数组及少数功能性），ndarray最主要属性如下：

> * ndarray.ndim  数组维度
> * ndarray.shape 数维度数，返回tuple对象，其列表里的每个数相乘则为数组的元素个数，另其返回对象内部长度则为数组维度ndim
> * ndarray.size    数组元素个数
> * ndarray.dtype  数组元素的数据类型，即可参考python数据类型，也可以使用其内部数据类型numpy.int32, numpy.int16, numpy.float64等
> * ndarray.itemsize     数组内数据元素字节长度
> * ndarray.data   缓冲区里的数据真实元素位置，实际基本不用

#### 创建数组

有如下几种方法创建

1. 通过array方法，我们可以创建存储在python list和tuple中的数组对象，注意经常出错的问题在传参数时，非iterate对象（list, tuple等）

   ```py
   import numpy as np  
   a = np.array([2,3,4])   
   a  
   # array([2,3,4])  
   a.dtype      # dtype('int64')  
   b = np.array([1.2, 3.5, 5.1])  
   b.dtype      # dtype('float64')  
   b = np.array([(1.5,2,3),(4,5,6)])  
   b
   # array([[1.5, 2., 3.],  
            [4., 5., 6.]])
   c = np.array([[2,3],[3,4]]， dtype=complex)
   c  
   # array([1 + 0.j, 2. + 0.j],  
   #       [3.+ 0.j, 4. + 0.j]])
   ```

2. 通常具体数据元素数值是不知晓的，但是其数据类型大小是知道的，故Numpy提供了几个方法创建数组， zeros创建所有元素为0的数组， ones则其所有元素都为1，还有empty函数其元素值为随机，其dtype通常为float64:\(ones_like\(\), empty\\_like\(\), _\)

   ```py
    np.zeros((3,4))
   # array([[0.,0.,0.,0.],   
           [0.,0.,0.,0.],
           [0.,0.,0.,0.]])

    np.ones((2,3,4),dtype=int16)
    array([[[1,1,1,1],
            [1,1,1,1],
            [1,1,1,1]],
           [[1,1,1,1],
            [1,1,1,1],
            [1,1,1,1]]], dtype=int16)
    np.empty( (2,3) )  # uninitialized, output may vary

   # array([[3.73603959e-262,6.02658058e-154,6.55490914e-260], 
            [5.30498948e-313,3.14673309e-307,1.00000000e+000]])
   ```

3. 创建连续性的序列，可以参照python的range方法，返回array对象

   ```py
   np.arange(10,30,5)
   # array([10,15,20,25])

   np.arange(0,2,0.3)
   # array([0., 0.3, 0.6, 0.9, 1.2, 1.5, 1.8])
   ```

4. linspace方法，可以确定元素个数，而非步长

   ```py
   from numpy import pi
   np.linspace(0,2,9)
   # array([0., 0.25, 0.5, 0.75, 1.0, 1.25, 1.5, 1.75,2.])
   x = np.lispace(0, 2 * pi 100)
   f = np.sin(x)
   ```

#### 数组显示

当你需要显示numpy数组时，Numpy非常轻松将以嵌套列表的方式呈现，当然以如下布局方式：

* The last axis is printed from left to right
* The second-to-last is printed from top to bottom
* The rest are also printed from top to bottom, with each slice separated from the next by an empty line.

一维将呈现一行，二维呈现矩阵，三维则呈现为列表矩阵

```py
a = np.arange(6)
print(a)   # [0,1,2,3,4,5]

b = np.arange(12).reshape(4,3)
print(b)

# [[0,1,2],
   [3,4,5],
   [6,7,8],
   [9,10,11]])
c = np.arange(24).reshape(2,3,4)
print(c)

# [[[ 0  1  2  3]
   [ 4  5  6  7]
   [ 8  9 10 11]]
  [[12 13 14 15]
   [16 17 18 19]
   [20 21 22 23]]]
```

如果需要显示特别大量数据的数组时，Numpy将会跳过中间部分，取而代之以省略号显示。 我们可以同np.set\_printoptoins\(threshold=np.nan\)函数来迫使打印全部数据信息。

#### 基本操作

算术操作可以如平常一样使用

```py
a = np.array([20,30,40,50])
b = np.arange(4)  # array([0,1,2,3])

c = a - b   # array([20,29,38,47])
b**2   # array([0,1,4,9])

10 * np.sin(a)  # array([ 9.12945251, -9.88031624,  7.4511316 , -2.62374854])

a < 35   # array([True, True, False, False])
```

Numpy中使用乘法，与其他矩阵语言不太相同，\* 表示矩阵表中每个对应坐标元素相乘，而矩阵相乘则使用“@”或者dot函数

```py
a = np.array([[1,1],
              [0,1]]) 

b = np.array([[2,0],
              [3,4]])
a * b
# array([[2, 0],
#       [0, 4]])

a @ b
# array([[5, 4],
#        [3, 4]])

a.dot(b)
# array([[5, 4],
#        [3, 4]])
```

其他二元操作，如+=, \*=等，考虑ndarray对象的特性，其相当于运算完后，重新创建新的矩阵

```py
a = np.ones((2,3), dtype=int)
b = np.random.random((2,3))

a *= 3
# array([[3,3,3],
#        [3,3,3]])

b += a

a += b  # 出错，float64赋值给int64
```

如果将上述两个矩阵的运算赋值给新的变量时，则可以。

```py
a = np.ones(3,dtype=np.int32)
b = np.linspace(0, np.pi, 3)
b.dtype.name # 'float64'
c = a + b
c # array([1.        , 2.57079633, 4.14159265])

d = np.exp(c * 1j)
# array([ 0.54030231+0.84147098j, -0.84147098+0.54030231j, -0.54030231-0.84147098j])
```

许多一元操作，如计算所有元的和，都在ndarray对象中实现

```py
a = np.random.random((2,3))
# array([[0.63900631, 0.22746009, 0.81599543],
#        [0.36092778, 0.14295098, 0.69072727]])

a.sum() # 2.8770678643182928
a.min() # 0.14295097938903178
a.max() # 0.8159954326659985
```

还可以通过其不同轴向axis进行一元操作

```py
b = np.arange(12).reshape(3,4)
# array([[ 0,  1,  2,  3],
#        [ 4,  5,  6,  7],
#        [ 8,  9, 10, 11]])

b.sum(axis=0) # column
# array([12, 15, 18, 21])
b.sum(axis=1) # row
# array([ 6, 22, 38])

b.min(axis=1) # row  array([0,4,8])
b.cumsum(axis=1)  # row向元素累加
```

#### 一般函数

Numpy提供了些熟悉的数学函数，例如sin, cos和exp等，在Numpy中被称为一般函数“ufunc", 及计算后结果将返回一个新的array

```py
b = np.arange(3)
np.exp(b)
# array([1.        , 2.71828183, 7.3890561 ])
np.sqrt(b)
# array([0.        , 1.        , 1.41421356])
np.add(b, np.array([2., -1., 4.]))
# array([2., 0., 6.])
```

其他相关函数，待下一步完成

##### 索引、切片和迭代

一维数组能索引，切片和迭代，类似lists及其他python序列对象





