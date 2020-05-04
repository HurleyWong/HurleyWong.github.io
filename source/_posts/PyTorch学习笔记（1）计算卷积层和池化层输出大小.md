---
title: PyTorch学习笔记（1）计算卷积层和池化层输出大小
tags:
  - PyTorch
categories: 
  - 深度学习
date: 2020-02-29
---

### 卷积操作输出的计算公式

首先，定义一下参数的概念。

`width`、`height`、`depth`、`filter`、`stride`、`padding`

W：图像的宽；H：图像的高；D：图像的深度（通道数）

F：卷积核的宽和高；N：卷积核（过滤器）的个数

S：步长；P：用零填充的个数

因此，卷积输出的公式为：

<!-- more -->

`output_shape = (input_shape - filter_size + 2 * padding) / stride + 1`

即`卷积输出大小=(输入大小 - 卷积核大小 + 2 * padding) / 步长 + 1`

### 池化操作输出的计算公式

同样，W：图像宽；H：图像高；D：图像深度（通道数）

F：`MaxPooling`中的卷积核的宽高；S：步长

因此，池化后输出大小为：

`(input_shape - filter_size) / stride + 1`

值得注意的是，这里的filter_size不是`Conv2d`中的卷积核大小，而是池化层中的卷积核大小。例如`MaxPool2d(2, 2)`这里的卷积核大小就是`2x2`。

### nn.Conv2d简单说明

#### 参数

* `in_channels(int)`
* `out_channels(int)`
* `kernel_size(int or tuple)`
* `stride(int or tuple, optional)`
* `padding(int or tuple, optional)`
* `groups(int, optional)`
* `bias(bool, optional)`











