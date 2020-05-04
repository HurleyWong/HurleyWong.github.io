---
title: Numpy官方快速热门教程（译）
tags:
  - Numpy
categories: 
  - Python
date: 2019-11-02
---

### Numpy

Numpy是一个开源的Python科学计算库，它是Python科学计算库的基础库。

### Numpy常用统计函数

**函数在使用时需要指定axis轴的方向**，若不指定，则默认是整个数组

* `np.num()`：返回求和
* `np.mean()`：返回均值
* `np.max()`：返回最大值
* `np.min()`：返回最小值
* `np.ptp()`：数组沿指定轴返回最大值减去最小值，即（max-min）
* `np.std()`：返回标准偏差（standard deviation）
* `np.var()`：返回方差
* `np.cumsum()`：返回累加值
* `np.cunprod()`：返回累乘积值

<!-- more -->

### 数组对象

Numpy的主要操作对象是同类型的多维数组。它是一个由正整数元组索引，元素类型相同的表（通常元素为数字）。在Numpy维度被成为`axes`，`axes`的数量称为`rank`。

例如，在3D空间的一个点[1,2,1]是一个`rank=1`的数组，因为它只有一个`axes`。而这个`axes`的长度为3。同样的，下面这个例子则是，数组`rank=2`（2维，2层嵌套的中括号），第一维的长度为2，第二维长度为3。（第1维即中括号最外面的部分，内部又包含2个中括号（相当于2个元素），所以长度为2；第2维即内部的中括号内含有3个元素）

```python
[[1, 0, 0],
[0, 1, 2]]
```

Numpy的数组类是`ndarray`，也可称作`array`。值得注意的是，`numpy.array`和标准Python库中的`array.array`是不一样的，它只能处理一维数组，提供更少的功能。

#### `ndarray`对象的一些重要属性

* `ndarray.ndim`

  > 数组的`axes`（维数）数值的大小，即`rank`，几维

* `ndarray.shape`

  > 数组的维数，这是由每个维度的大小组成的一个元组。对于一个**n行m列**的矩阵，`shape`是`(n,m)`。由`shape`元组的长度得出`rank`或者维数`ndim`。

* `ndarray.size`

  > 数组元素的个数总和，这等于`shape`元组数字的乘积。

* `ndarray.dtype`

  > 在数组中描述元素类型的一个对象。

* `ndarray.itemsize`

  > 数组中每个元素所占字节数。

* `ndarray.data`

  > 数据实际元素的缓存区。

### 创建数组

首先导入Numpy库，以`np`为缩写

```python
import numpy as np
```

#### 基于list或者tuple

```python
# 一维数组 # 基于list
arr1 = np.array([1, 2, 3, 4])
print(arr1)

# 二维数组
arr2 = np.array([[1, 2, 4], [3, 4 ,5]])
arr2

# 基于tuple
arr_tuple = np.array((1, 2, 3, 4))
print(arr_tuple)
```

输出结果：

```python
[1 2 3 4]
array([[1, 2, 4],
       [3, 4, 5]])
[1 2 3 4]
```

#### 基于np.arange

```python
# 一维数组
arr1 = np.arange(5)
print(arr1)

# 二维数组
arr2 = np.array([np.arange(3), np.arange(3)])
arr2
```

输出结果：

```python
[0 1 2 3 4]
array([[0, 1, 2],
       [0, 1, 2]])
```

#### 基于arange以及reshape创建多维数组

```python
# 创建三维数组
arr = np.arange(24).reshape(2, 3, 4)
arr
```

输出结果：

```python
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23]]])
```

注意，arange的长度必须与ndarray的维度的乘积要相当，即24 = 2x3x4

### ndarray数组的切片和索引

一维数组的切片和索引与python的list索引类似。

二维数组的切片和索引如下图所示

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-31_20-54-44.png)

### 处理数组形状

#### 堆叠数组

```python
b
array([[ 0,  1, 20,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11]])
c = b*2
c
array([[ 0,  2, 40,  6,  8, 10],
       [12, 14, 16, 18, 20, 22]])
```

* 水平叠加

  ```python
  hstack()
  np.hstack((b,c))
  array([[ 0,  1, 20,  3,  4,  5,  0,  2, 40,  6,  8, 10],
         [ 6,  7,  8,  9, 10, 11, 12, 14, 16, 18, 20, 22]])
  ```

  column_stack()函数以列的方式对数组进行叠加，功能类似hstack()

  ```python
  column_stack()
  np.column_stack((b,c))
  array([[ 0,  1, 20,  3,  4,  5,  0,  2, 40,  6,  8, 10],
         [ 6,  7,  8,  9, 10, 11, 12, 14, 16, 18, 20, 22]])
  ```

* 垂直叠加

  ```python
  vstack()
  np.vstack((b,c))
  array([[ 0,  1, 20,  3,  4,  5],
         [ 6,  7,  8,  9, 10, 11],
         [ 0,  2, 40,  6,  8, 10],
         [12, 14, 16, 18, 20, 22]])
  ```

  row_stack()函数以行的方式对数组进行叠加，功能类似vstack()

  ```python
  row_stack()
  np.row_stack((b,c))
  array([[ 0,  1, 20,  3,  4,  5],
         [ 6,  7,  8,  9, 10, 11],
         [ 0,  2, 40,  6,  8, 10],
         [12, 14, 16, 18, 20, 22]])
  ```

* concatenate()方法，通过设置axis的值来设置叠加方向

  axis=1时，沿水平方向叠加

  axis=0时，沿垂直方向叠加

  ```python
  np.concatenate((b,c),axis=1)
  array([[ 0,  1, 20,  3,  4,  5,  0,  2, 40,  6,  8, 10],
         [ 6,  7,  8,  9, 10, 11, 12, 14, 16, 18, 20, 22]])
  np.concatenate((b,c),axis=0)
  array([[ 0,  1, 20,  3,  4,  5],
         [ 6,  7,  8,  9, 10, 11],
         [ 0,  2, 40,  6,  8, 10],
         [12, 14, 16, 18, 20, 22]])
  ```

用示意图来表示如下：

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/v2-8e62ce376316c13dd7d5be9f9b66bafa_hd.jpg)

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/v2-0da226f02c3a7600abfb285868ebd98b_hd.jpg)

* 深度叠加

  ```python
  arr_dstack = np.dstack((b,c))
  print(arr_dstack.shape)
  arr_dstack
  (2, 6, 2)
  
  array([[[ 0,  0],
          [ 1,  2],
          [20, 40],
          [ 3,  6],
          [ 4,  8],
          [ 5, 10]],
  
         [[ 6, 12],
          [ 7, 14],
          [ 8, 16],
          [ 9, 18],
          [10, 20],
          [11, 22]]])
  ```

  叠加前，b和c均是shape为(2,6)的二维数组，叠加后，arr_dstack是shape为(2,6,2)的三维数组。

#### 数组拆分

数组的拆分可以分为横向拆分、纵向拆分和深度拆分。

```python
b
array([[ 0,  1, 20,  3,  4,  5], [ 6,  7,  8,  9, 10, 11]])
```

* 横向拆分（axis=1）

  ```python
  np.hsplit(b, 2)
  [array([[ 0,  1, 20], [ 6,  7,  8]]), array([[ 3,  4,  5], [ 9, 10, 11]])]
  np.split(b,2, axis=1)
  [array([[ 0,  1, 20], [ 6,  7,  8]]), array([[ 3,  4,  5], [ 9, 10, 11]])]
  ```

* 纵向拆分（axis=0）

  ```python
  np.vsplit(b, 2)
  [array([[ 0,  1, 20,  3,  4,  5]]), array([[ 6,  7,  8,  9, 10, 11]])]
  np.split(b,2,axis=0)
  [array([[ 0,  1, 20,  3,  4,  5]]), array([[ 6,  7,  8,  9, 10, 11]])]
  ```

* 深度拆分

  ```python
  arr_dstack
  array([[[ 0,  0],
          [ 1,  2],
          [20, 40],
          [ 3,  6],
          [ 4,  8],
          [ 5, 10]],
  
         [[ 6, 12],
          [ 7, 14],
          [ 8, 16],
          [ 9, 18],
          [10, 20],
          [11, 22]]])
  np.dsplit(arr_dstack,2)
  [array([[[ 0],
           [ 1],
           [20],
           [ 3],
           [ 4],
           [ 5]],
  
          [[ 6],
           [ 7],
           [ 8],
           [ 9],
           [10],
           [11]]]), array([[[ 0],
           [ 2],
           [40],
           [ 6],
           [ 8],
           [10]],
  
          [[12],
           [14],
           [16],
           [18],
           [20],
           [22]]])]
  ```

  拆分的结果就是把原来的三维数组拆分成两个二维数组。

#### 数组类型转换

* 数组转换成list，使用tolist()

  ```python
  b
  array([[ 0,  1, 20,  3,  4,  5],
         [ 6,  7,  8,  9, 10, 11]])
  b.tolist()
  [[0, 1, 20, 3, 4, 5], [6, 7, 8, 9, 10, 11]]
  ```

* 转换成指定类型，使用astype()函数

  ```python
  b.astype(float)
  array([[  0.,   1.,  20.,   3.,   4.,   5.],
         [  6.,   7.,   8.,   9.,  10.,  11.]])
  ```

#### 形状转换

* reshape()和resize()

  ```python
  b.reshape(4,3)
  array([[ 0,  1,  2],
         [ 3,  4,  5],
         [ 6,  7,  8],
         [ 9, 10, 11]])
  b
  array([[ 0,  1,  2,  3],
         [ 4,  5,  6,  7],
         [ 8,  9, 10, 11]])
  b.resize(4,3)
  b
  array([[ 0,  1,  2],
         [ 3,  4,  5],
         [ 6,  7,  8],
         [ 9, 10, 11]])
  ```

  resize()与reshape()的作用相似，但是resize()会改变所作用的数组

* ravel()和flatten()，可以将多维数组转换成一维数组

  ```
  b.ravel()
  array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
  b.flatten()
  array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
  b
  array([[ 0,  1,  2],
         [ 3,  4,  5],
         [ 6,  7,  8],
         [ 9, 10, 11]])
  ```

  两者的区别在于返回拷贝还是返回视图。即flatten()是返回一份拷贝，需要分配新的内存空间，会影原始矩阵；但ravel()返回的是视图，会影响原始矩阵。

* 用tuple指定数组的形状，如下所示：

  ```python
  b.shape=(2,6)
  b
  array([[ 0,  1, 20,  3,  4,  5],
         [ 6,  7,  8,  9, 10, 11]])
  ```

* 转置

  通过transpose()函数来实现

  ```python
  b.transpose()
  array([[ 0,  6],
         [ 1,  7],
         [20,  8],
         [ 3,  9],
         [ 4, 10],
         [ 5, 11]])
  ```


### 零碎知识点

#### np.reshape函数参数-1的意思

-1表示暂时不知道需要什么数字，但可以通过其他推导出来。即其实可以忽略-1。

```python
>>> a = np.array([[1,2,3], [4,5,6]])
>>> np.reshape(a, (3,-1))  # the unspecified value is inferred to be 2
array([[1, 2],
       [3, 4],
       [5, 6]])
```

这里的-1即可以忽略，只通过a和3即可推导出-1的实际应为2。

即把原数组合并在一起成为一个数组，然后分成3行，这样每行就有2列。

```python
# 下面是两张2*3大小的照片(不知道有几张照片用-1代替)，如何把所有二维照片给摊平成一维
>>> image = np.array([[[1,2,3], [4,5,6]], [[1,1,1], [1,1,1]]])
>>> image.shape
(2, 2, 3)
>>> image.reshape((-1, 6))
array([[1, 2, 3, 4, 5, 6],
       [1, 1, 1, 1, 1, 1]])
```

reshape后分成6列，则12/6=2行。





















