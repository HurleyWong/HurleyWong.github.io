---
title: keras搭建图像分类的CNN
tags:
  - keras
categories: 
  - 深度学习
date: 2019-12-05 
top_img: https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/United%20States%2C%20North%20America%2C.jpg                                             
---

### Conv2D

构建一个**卷积层**，用于从输入的高维数组中提取特征。卷积层的每个过滤器都是一个特征映射，用于提取某一个特征。过滤器的数量决定了卷积层输出特征个数，或者输出深度。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/2nf4ym949o.gif)

<!-- more -->

### MaxPooling2D

构建最大池化层。最大池化层的作用就是降低输出维度（宽高）。在CNN架构中，最大池化层通常出现在卷积层后，后面接着下一个卷积层，**交替出现**。结果就是，输入的高维数组，深度逐次增加，而维度逐次降低。最终，高维的空间信息，逐渐转化为1维的特征向量，然后连接全连接层或者其它分类算法，得到模型输出。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/z2rf1scjhh.png)



示例：在卷积层后面添加最大池化层，降低卷积层的维度。假设卷积层的大小是(100, 100, 15)，希望最大池化层的大小为(50, 50, 15)，那么可以在最大池化层中使用2x2的窗口，步长stride设为2

```python
MaxPooling2D(pool_size=2, strides=2)
```

### 构建CNN

#### 创建序列化模型

```python
model = Sequential()
```

#### 添加卷积层和最大池化层

* 模型的第一层卷积层**接收输入**，因此需要设置一个`input_shape`参数指定输入维度。这里设置为(32, 32, 3)，表示图片需要宽高为32像素的**RGB彩色**图片。在第一层之后的层都不需要设置`input_shape`，因为模型会自动将前一层的输出shape作为后一层的输入shape。
* 由于习惯使得卷积层不改变维度，而让最大池化层每次将维度缩小一半，即宽高都除以2，为了一直能整除，所以最好将shape设置为2的整数幂，如32、64等。

```python
model.add(Conv2D(filters=16, kernel_size=2, padding='same', activation='relu', input_shape=(28, 28, 1)))
model.add(MaxPooling2D(pool_size=2))

model.add(Conv2D(filters=32, kernel_size=2, padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=2))

model.add(Conv2D(filters=64, kernel_size=2, padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=2))
```

### 扁平层

模型第一层输入是(32, 32, 3)，经过卷积层和最大池化层，可以得到的现在输出宽高为32\2\2\2=4。再加上最后一层的过滤器的数量是64，所以输出shape为(4, 4, 64)。

扁平层的作用是把这个多维数组（**张量**）转换为相同数量的**一维向量**。因此，向量的长度为4x4x64=1024。

```python
model.add(Flatten())
```

#### 全连接层

通过卷积层和最大池化层组合使用，从二维的图片中提取特征，将空间信息解构为特征向量后，就可以连接分类器，进而得到模型预测输出。分类器可以采用一个全连接层，也可以采用多个连接层，最后一个全连接层同时也是**输出层**。

```python
model.add(Dense(512, activation='relu'))
model.add(Dense(10, activation='softmax'))
```

这里输出长度为10的向量，对应10个分类的预测概率值。

#### 查看完整模型

可以通过`summary()`方法一览整个模型。`summary()`方法会将模型每一层的参数个数，以及整个模型参数总数和可以训练的个数显示出来。

```python
model.summary()

_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_4 (Conv2D)            (None, 32, 32, 16)        208       
_________________________________________________________________
max_pooling2d_2 (MaxPooling2 (None, 16, 16, 16)        0         
_________________________________________________________________
conv2d_5 (Conv2D)            (None, 16, 16, 32)        2080      
_________________________________________________________________
max_pooling2d_3 (MaxPooling2 (None, 8, 8, 32)          0         
_________________________________________________________________
conv2d_6 (Conv2D)            (None, 8, 8, 64)          8256      
_________________________________________________________________
max_pooling2d_4 (MaxPooling2 (None, 4, 4, 64)          0         
_________________________________________________________________
flatten_1 (Flatten)          (None, 1024)              0         
_________________________________________________________________
dense_1 (Dense)              (None, 500)               512500    
_________________________________________________________________
dense_2 (Dense)              (None, 10)                5010      
=================================================================
Total params: 528,054
Trainable params: 528,054
Non-trainable params: 0
_________________________________________________________________
```











