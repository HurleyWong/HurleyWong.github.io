---
title: IrisFlowers训练集
tags:
  - keras
categories: 
  - 深度学习
date: 2019-11-01
---

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/0.jpg)

> “现今程序员的情况好多了，只要有一台便宜的二手电脑，一张Linux光盘和一个互联网帐户，你就已经拥有了把自己提升到任何级别的编程水平所需的全部工具。”
> “在信息时代，进入编程领域的壁垒完全不存在了。即使有也是自我强加的。如果你想着手去开发一些全新的东西，你不需要数百万美元的资本。你只需要足够的比萨和健怡可乐存在你的冰箱里，有一台便宜的PC用于工作，以及让你坚持下来的奉献精神。**我们睡在地板上。我们跋山涉水**。”
> －约翰·卡马克 

约翰·卡马克的最后一句话，通俗易懂。又不禁让我想起了那段台词：

> 这是最好的时代，这是最坏的时代。我们一无所有，我们巍然矗立。

We will build and use a neural network for the Iris classification task. We will use "keras" as a high-level library for managing neural networks.  

<!-- more -->

## Analysis Code

```python
import numpy as np

import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.datasets import load_iris  # import load_iris function from datasets module

from keras.models import Sequential, Input, Model
from keras.utils import to_categorical
from keras.layers import Dense, Dropout, Flatten
from keras import optimizers

# -- Load Iris dataset using sklearn (save "bunch" object containing iris dataset and its attributes) -- ##
# 导入Iris数据集
# Iris数据集是sklearn中自带的
# Iris数据集有3个种类，4个属性，每个属性有50个样例
iris = load_iris()
# x代表iris数据集的数据
X = iris.data
# y代表着着iris的目标属性，即花的类型
y = iris.target

# -- Change the labels from categorical to one-hot encoding -- ##
# The output neurons of the NN will be trained to match the one_hot encoded array
# Example: category label 0 out of 3 labels becomes [1 0 0];
# Example: category label 1 out of 3 labels becomes [0 1 0];
# HINT: use: "to_categorical" to redifine the one hot encoded target y_one_hot using the original y.
# for i in range(len(y)):
#     if y[i] == 0:
#         y[i] = 1
#     else:
#         y[i] = 0  
y_one_hot = to_categorical(y)
print(X.shape)
print(y_one_hot.shape)
# y_one_hot = np.reshape(y, (-1, 1))

# -- Split the dataset for training, validation, and test -- ##

# x是被划分的样本特征集 
# y_one_hot是被划分的样本标签
# 如果是浮点数，就在0~1之间，表示样本所占比例；如果是整数，就是样本的数量
train_and_valid_X, test_X, train_and_valid_y, test_y = train_test_split(X, y_one_hot, test_size=0.1)
train_X, valid_X, train_y, valid_y = train_test_split(train_and_valid_X, train_and_valid_y, test_size=0.2)


# define the neural network
def baseline_model():
    nb_nurons = 8
    # nb_Classes = 1  # HINT:  <---- look here
    nb_Classes = 3
    input_dimensions = 4
    learning_rate = 0.002
    # create model
    # keras.models.Sequential是神经网络模型的封装容器。它会提供常见的函数
    model = Sequential()
    # 第一层级 - 添加有 input_dimensions = 4个节点的输入层
    # 激活函数使用ReLU运算
    model.add(Dense(nb_nurons, input_dim=input_dimensions, activation='relu'))
    # HINT: a 'softmax' activation will output a probability distribution over the output dimensions
    # 激活函数使用softmax函数
    model.add(Dense(nb_Classes,
                    activation='softmax'))
    # Compile model
    # 实例化一个优化器对象，这里采用RMSprop优化器
    opt = optimizers.RMSprop(lr=learning_rate)
    # HINT: a 'binary_crossentropy' is only useful for at most 2 labels, look for another suitable loss function in Keras
    # compile用于配置训练模型，loss是字符串或目标函数名，optimizer是优化器名或优化器实例，metrics是在训练和测试期间的模型评估标准
    # binary_crossentropy是交叉熵损失函数，一般用于二分类
    # 因为这里要实现3中分类即多分类，所以使用categorical_crossentropy
    model.compile(loss='categorical_crossentropy', optimizer=opt, metrics=[
        'accuracy'])
    return model


def find_correct_and_incorrect_labels(model, test_X, test_y):
    # Computes for every input in the test dataset a probability distribution over the categories
    # predict是为输入样本生成输出预测，计算是分批进行的
    predicted_classes = model.predict(test_X)
    # argmax是找到样本以最大概率所属的类别作为样本的预测标签
    # HINT: choose the prediction with the highest probability, np.argmax( ..... , axis=1 )
    # np.round是取返回四舍五入后的值，可指定精度，与np.around等效
    predicted_classes = np.argmax(predicted_classes, axis=1)
    # np.where(conditions)满足conditions的条件即输出数组的下标
    correctIndex = np.where(predicted_classes == np.argmax(test_y))[0]  # HINT: replace test_y by np.argmax(test_y,axis=1)
    incorrectIndex = np.where(predicted_classes != np.argmax(test_y))[0]  # HINT: replace test_y by np.argmax(test_y,axis=1)
    print("Found %d correct labels using the model" % len(correctIndex))
    print("Found %d incorrect labels using the model" % len(incorrectIndex))


def plot_train_performance(trained_model):  
  	# history函数会每轮训练收集损失和准确率，如果有测试集也会收集测试集的数据
    print(trained_model.history.keys())
    accuracy = trained_model.history['accuracy']
    val_accuracy = trained_model.history['val_accuracy']
    loss = trained_model.history['loss']
    val_loss = trained_model.history['val_loss']
    # epoch表示完成了1遍训练集中的所有样本
    epochs = range(len(accuracy))
    # 创建一个画板，1为画板的编号，可以不填
    f1 = plt.figure(1)
    # 一个figure对象包含了多个子图，可以使用subplot()函数来绘制子图
    plt.subplot(1, 2, 1)
    # axis设置坐标轴
    plt.axis((0, len(epochs), 0, 1.2))
    plt.plot(epochs, accuracy, 'bo', label='Training accuracy')
    plt.plot(epochs, val_accuracy, 'b', label='valid accuracy')
    plt.title('Training and valid accuracy')
    plt.legend()
    plt.subplot(1, 2, 2)
    plt.axis((0, len(epochs), 0, 1.2))
    plt.plot(epochs, loss, 'bo', label='Training loss')
    plt.plot(epochs, val_loss, 'b', label='valid loss')
    plt.title('Training and valid loss')
    # 展示出每个数据对应的图像名称，更好辨认
    plt.legend()
    plt.show()
    plt.pause(0.001)


# -- Initialize model -- ##
model = baseline_model()

# -- Test the performmance of the untrained model over the test dataset -- ##
find_correct_and_incorrect_labels(model, test_X, test_y)

# -- Train the model -- ##
print('\nTraining started ...')
trained_model = model.fit(train_X, train_y, batch_size=10, epochs=150, verbose=0, validation_data=(valid_X, valid_y))
print('Training finished. \n')

# -- Test the performmance of the trained model over the test dataset -- ##
find_correct_and_incorrect_labels(model, test_X, test_y)

# -- Plot performance over training episodes -- ##
plot_train_performance(trained_model)
```

## Result

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-11-01_21-10-25.png)

## Error

在按照提示修改代码后，会一直提示以下这个错误，即实际输出的数组形状为与预期数据的形状不同。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-11-01_21-20-09.png)

最终通过Stack Overflow上的[一篇帖子](https://stackoverflow.com/questions/51456613/valueerror-error-when-checking-target-expected-dense-3-to-have-shape-1-but)找到了问题所在。

the following line is wrong

```python
nb_Classes = 1
```

change it to 

```python
nb_Classes = 3
```

Because final layer is of 3 dimension. Beacuse I used `categorical_crossentropy` and also the terminal shows that actually there are three layers.

## 知识点

### categorical_crossentropy()函数

即**分类交叉熵**函数。它用于衡量两个概率分布之间的举例。

### train_test_split

`train_test_split`是交叉验证中常用的函数，功能是从样本中随机的按比例选取train_data和test_data，形式为：

`X_train, X_test, y_train, y_test = cross_validation.train_test_split(train_data, train_target, test_size=0.4, randow_state=0)`

`cross_validation`为交叉验证

**参数解释：**

* train_data：所划分的样本特征集
* train_target：所要划分的样本结果
* test_size：样本占比，如果是整数的话就是样本的数量
* random_size：随机数的种子

**随机数种子：**

该组随机数的编号，可以在需要重复试验的时候，保证得到一组同样的随机数。比如，如果每次都设置随机数为1，那么得到的随机数组是一样的。如果设置为0或者不填，每次都会不一样。

随机数的产生取决于种子，随机数和种子之间关系：种子不同，产生不同的随机数；种子相同，即使实例不同也产生相同的随机数。

### ReLU激活函数

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/20161113161105403.png)

ReLU函数是分段线性函数，可以简单表示为`ReLU(x) = max(x, 0)`，在神经元中输出为：$\max(0, w^Tx+b)$

> **线性整流函数**（Rectified Linear Unit, **ReLU**），又称修正线性单元，是一种[人工神经网络](https://baike.baidu.com/item/人工神经网络)中常用的激活函数（activation function），通常指代以[斜坡函数](https://baike.baidu.com/item/斜坡函数)及其变种为代表的非线性函数。

**优点：**

* 梯度不饱和。因为梯度计算公式为：1{x>0}，所以在反向传播的过程中，减轻了梯度弥散的问题，神经网络前几层的参数也可以很快更新。
* 计算速度快。ReLU函数仅仅需要设置阈值，加快了正向传播的速度。

### RMSprop优化器

For example:

```python
keras.optimizers.RMSprop(lr=0.001, rho=0.9, epsilon=None, decay=0.0)
```

建议使用优化器的默认参数（除了学习率lr，它可以被自由调节）。

RMSprop优化器通常是训练循环神经网络RNN的不错选择。

**参数：**

* **lr**: float >= 0，学习率
* **rho**: float >= 0，RMSProp梯度平方的移动均值的衰减率
* **epsilon**: float >= 0，模糊因子。若为None，默认为`K.epsilon()`
* **decay**: float >= 0，每次参数更新后学习率衰减值

### Model类类型方法

#### compile

```python
compile(optimizer, loss=None,  metrics=None, loss_weights=None, sample_weight_mode=None, weighted_metrics=None, target_tensors=None)
```

**参数：**

* **optimizer**：字符串（优化器名）或者优化器实例
* **loss**：字符串（目标函数名）或目标函数。如果模型具有多个输出，则可以通过传递损失函数的字典或列表，在每个输出上使用不同的损失。 模型将最小化的损失值将是所有单个损失的总和。
* **metrics**：在训练和测试期间的模型评估标准。
* **loss_weights**：可选的指定标量系数（Python 浮点数）的列表或字典， 用以衡量损失函数对不同的模型输出的贡献。 模型将最小化的误差值是由 `loss_weights` 系数加权的*加权总和*误差。 如果是列表，那么它应该是与模型输出相对应的 1:1 映射。 如果是张量，那么应该把输出的名称（字符串）映到标量系数。
* **sample_weight_mode**：如果你需要执行按时间步采样权重（2D 权重），请将其设置为 `temporal`。 默认为 `None`，为采样权重（1D）。 如果模型有多个输出，则可以通过传递 mode 的字典或列表，以在每个输出上使用不同的 `sample_weight_mode`。
* **weighted_metrics**：在训练和测试期间，由`sample_weight`或`class_weight`评估和加权的度量标准列表。
* **target_tensors**：默认情况下，Keras 将为模型的目标创建一个占位符，在训练过程中将使用目标数据。 相反，如果你想使用自己的目标张量（反过来说，Keras 在训练期间不会载入这些目标张量的外部 Numpy 数据）， 您可以通过 `target_tensors` 参数指定它们。 它可以是单个张量（单输出模型），张量列表，或一个映射输出名称到目标张量的字典。
* **kwargs**： 当使用 Theano/CNTK 后端时，这些参数被传入 `K.function`。 当使用 TensorFlow 后端时，这些参数被传递到 `tf.Session.run`。

#### fit

```python
fit(x=None, y=None, batch_size=None, epochs=1, verbose=1, callbacks=None, validation_split=0.0, validation_data=None, shuffle=True, class_weight=None, sample_weight=None, initial_epoch=0, steps_per_epoch=None, validation_steps=None)
```

编译（compile）后的模型就可以开始训练（fit）了，fit的过程可以简单的理解为通过测试数据来确定神经元间连接权重（weight）的过程。

**参数：**

* **x**：训练数据的Numpy数组（一个输入）或者Numpy数组的列表（如果模型有多个输入）。None是默认。
* **y**：目标（标签）数据的Numpy数组（一个输出）或者Numpy数组的列表（如果模型有多个输出）。None是默认。
* **batch_size**：整数或者None。每次梯度更新的样本数。如果未指定，则默认为32。
* **epochs**：整数。训练模型迭代的最终轮次。
* **verbose**：0，1或2。是日志显示模式。0是安静模式，1是进度条，2是每轮一行。
* **callbacks**：一系列的`keras.callbacks.Callback`实例。一系列可以在训练时使用的回调函数。
* **validation_split**：0和1之间的浮点数，用于验证集的训练数据的比例。模型将分出一部分不会被训练的验证数据，并将在每一轮结束时评估这些验证数据的误差和任何其他模型指标。
* **validatoin_data**：元组 `(x_val，y_val)` 或元组 `(x_val，y_val，val_sample_weights)`， 用来评估损失，以及在每轮结束时的任何模型度量指标。 
* **shuffle**：布尔值在每轮迭代之前混洗数据）或者字符串（batch）。
* **class_weight**：可选的字典，用来映射类索引（整数）到权重（浮点）值，用于加权损失函数（仅在训练期间）。
* **sample_weight**：训练样本的可选Numpy权重数组，用于对损失函数进行加权。
* **initial_epoch**：整数。开始训练的轮次。
* **steps_per_epoch**：整数或None。在声明一个轮次完成并开始下一个轮次之前的总步数。
* **validation_steps**：只有在指定了`steps_per_epoch`时才有用。停止前要验证的总步数。

### np.where()方法

1. `np.where(condition, x, y)`

   当满足条件condition时，输出x，否则输出y。

2. `np.where(condition)`

   只有条件condition，没有x和y，则输出满足条件元素的坐标（以tuple的形式给出）。

3. 给`np.where()`函数传递一个条件数组和两个值或者数组，对于条件数组中等价于True的位置，从第一个值或数组中取值进行替换，否则从第二个值或数组中取值进行替换。

   ```python
   x = np.array([1, 2, 3, 4, 5, 6])
   y = np.array([[1, 0, 3], [4, 5, 0]])
   print(np.where(x%2 == 1, x, -x))
   print(np.where(y%2 == 1, 1, -1))
   print(np.where(y, [30, 40, 50], [60, 70, 80]))
   ```

   输出结果：

   ```python
   # 最后一组是当等于0时为false,不为0时为true
   # 所以y取1时为true，最后一个取第一组的30；y取0时为false，最后一个取第二组的70
   [ 1 -2  3 -4  5 -6]
   [[ 1 -1  1]
    [-1  1 -1]]
   [[30 70 50]
    [30 40 80]]
   ```

np.where()[0]表示行的索引，np.where()[1]表示列的索引

### Epoch、Batchsize、Iteration

####  Epoch

训练时，所有训练数据集都被训练过一次。

#### Batchsize

在训练集中选择一组样本（训练集中的部分样本）用来更新权值。1个batch包含的样本的数目，通常是2的n次幂。常用的包括64，128，256。网络较小时选择256，较大时选择64。

#### Iteration

训练时，1个batch训练图像通过网络训练一次（一次前向传播 + 一次后向传播），每迭代一次权重更新一次；测试时，1个batch测试图像通过网络一次（一次前向传播）。iteration即完成一个epoch所需要的batch个数。

### subplot()

`subplot()`是用来绘制子图的。

```python
# 生成两行两列，编号为1
# plt.subplot('行', '列', '编号')
plt.subplot(2, 2, 1)
```

**Tips:**

行号优先，行优先开始数。







