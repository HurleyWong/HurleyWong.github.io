---
title: Introduction to PyTorch
tags:
  - PyTorch
categories: 
  - 深度学习
date: 2020-02-20
---

This notebook covers:

* Tensors
* Gradients
* Datasets
* Neural networks
* Training(+ training on a GPU)

### Code

代码见[Intro_to_Pytorch](https://github.com/HurleyJames/GoogleColabExercise/blob/master/Intro_to_PyTorch.ipynb)。

<!-- more -->

### Tensors

Tensor is a basic building block.

它和Numpy的`ndarrays`相似，但是相比后者，它可以在GPU上使用。

`torch.Tensor`是一种包含单一数据类型元素的多维矩阵。

### Gradients

相比Numpy，PyTorch在传播梯度方面更加强大。它可以前向传播也可以反向传播。

Both the gradient, and forward and backward pass functions are attached to PyTorch's Tensor object.

```python
x = torch.tensor([4.0, 5.0, 6.0], requires_grad=True)
```

如果设置`requires_grad=True`，那么将会追踪对于该张量的操作。当完成计算后，通过调用`.backward()`，自动计算所有梯度，而这个张量的所有梯度将会自动积累到`.grad`属性。

```python
x.grad_fn
```

`Tensor`和`Function`是互联的并且构成了一个无环计算图，以此来实现对完整计算历程的编码。每个Tensor都有一个`.grad_fn`属性指向一个`Function`，正是这个`Function`创建了那个Tensor。

------

然后通过Numpy和Tensor分别创建了两个相同的数组，Numpy通过`grad_w = v * w`得到的结果与Tensor通过

```python
y = w * x
y.backward(v)
w.grad
```

得到的结果是相同的。

可以看到，PyTorch中的`backward`函数是一个反向求导的函数，通过反向传播的方式，使用链式法则求导。

### Datasets

**Transforms** are common image transformations which can be chained together using Compose().

`torchvision.transforms`是PyTorch中的图像预处理包，包含了很多种对图像数据进行变换的函数。而`Compose`方法则是把多种变换组合在一起。

```python
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])
```

`.ToTensor()`的变换操作是将PILImage转变为`torch.FloatTensor`的数据形式。然后的`.Normalize`方法是用给定的均值和标准差分别对每个通道的数据进行正则化，即使用如下公式进行归一化：

`channel = (channel - mean) / std`

`DataLoader`是PyTorch中的一种数据类型，主要包含以下几个参数：

1. `dataset`：数据类型`dataset`

    输入数据类型。例如**数据集**。

2. `batch_size`：数据类型`int`

    每次输入数据的行数，默认为1。即定义每次喂给神经网络多少行数据，如果是1，那么就是一行一行的进行（效率太低）。

3. `shuffle`：数据类型`bool`

    洗牌。默认设置为`False`。如果设置为`True`，那么系统在返回之前会将张量数据Tensors复制到CUDA内存中。

4. `batch_sampler`：数据类型`Sampler`

    批量采样，默认设置为`None`。每次返回的是一批数据的索引。**和`batch_size`和`sampler`和`drop_last`不兼容**。

5. `sampler`：数据类型`Sampler`

    采样，默认设置为`None`。根据定义的策略从数据集中采样输入。如果定义了采样规则，则洗牌设置必须为`False`。

6. `num_workers`：数据类型`int`

    工作者数量，默认为0。即**使用多少个子进程来导入数据**。如果设置为0，就是使用主进程来导入数据（这个数字必须大于0）。

例如，如果想

* 打乱数据的顺序，可以设置**shuffle**为`True`
* 改变数据输入的数量，可以设置**batch_size**的数目
* 想多线程输入，可以设置**num_workers**的数目
* 想随机抽取的模式输入，可以设置**sampler**或者**batch_sampler**。

然后`classes = np.arange(0, 10)`的方法就是创建一个数组，默认步长为1，所以这个数组就是`array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])`。这个的作用主要是后面的绘制混淆矩阵要用到。

### Neural networks

这里主要有两个步骤：

* 构建网络
* 构建损失函数和优化器

所有的网络都继承至`nn.Module`，然后总是需要用到以下两个函数：

* **init**, which will be called the moment you instantiate the class.
* **forward()** function which will be called during training.

#### 网络部分

```python
class LinearClassifier(nn.Module):
    
    def __init__(self, num_classes=10):
        # Calls __init__() on the parent class, which is nn.Module
        super(LinearClassifier, self).__init__()
        
        # Define each layer of the network as a class variable
        # fc1 stands for first fully-connected layer
        self.fc1 = nn.Linear(28 * 28, num_classes)
        
    def forward(self, x):
        out = x.reshape(x.size(0), -1) # TODO what does this do? Why do we need it?
        out = self.fc1(out)
        return out
```

这部分代码没有加上卷积层、池化层等操作，而是只有一个简单的全连接层。

而后面又问了一个问题：`out = x.reshape(x.size(0), -1)`这句代码的作用是什么？为什么要这样写？

如果数据集最后一个batch样本数量小于定义的batch_batch大小，会出现mismatch问题。可以自己修改下，如只传入后面的shape，然后通过x.szie(0)，来输入。

```python
torch.manual_seed(0)
```

这行的代码是因为在神经网络中，参数默认是进行随机初始化的。而不同的初始化参数往往会导致不同的结果，而在得到好的结果时我们都希望这个结果是能够**复现**的。因为通过设置**随机数种子**可以达到这个目的。

#### 损失函数和优化器部分

```python
criterion = nn.CrossEntropyLoss()

# Stochastic gradient descent
optimizer = optim.SGD(model.parameters(), lr=0.001, momentum=0.9)
```

这里用到的损失函数是`CrossEntropyLoss()`，然后优化器是用`SGD`，学习率为0,001，动量为0.9。

### Training

`optimizer.zero_grad`是将梯度重置为0，其余部分主要就是设置epoch次数，然后打印出每轮的损失率。最后通过计算`accuracy = correct / total`来得到准确率。

然后可以通过`matplotlib.pyplot`来生出具体的特征图，例如混淆矩阵。















