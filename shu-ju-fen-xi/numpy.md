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
   a = np.array([2,3,4])   # a  -> array([2,3,4])
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
2. 通常具体数据元素数值是不知晓的，但是其数据类型大小是知道的，故Numpy提供了几个方法创建数组， zeros创建所有元素为0的数组， ones则其所有元素都为1，还有empty函数其元素值为随机，其dtype通常为float64:

   ```py
   np.zeros((3,4))
   #array([[0.,0.,0.,0.],
           [0.,0.,0.,0.],
           [0.,0.,0.,0.]])

   np.ones((2,3,4),dtype=int16)
   #array([[[1,1,1,1],
            [1,1,1,1],
            [1,1,1,1]],
           [[1,1,1,1],
            [1,1,1,1],
            [1,1,1,1]]], dtype=int16)

   np.empty( (2,3) )  # uninitialized, output may vary
   #array([[3.73603959e-262,6.02658058e-154,6.55490914e-260],
          [5.30498948e-313,3.14673309e-307,1.00000000e+000]])
   ```
3. zeros创建所有元素为0的数组， ones则其所有元素都为1，还有empty函数其元素值为随机，其dtype通常为float64



