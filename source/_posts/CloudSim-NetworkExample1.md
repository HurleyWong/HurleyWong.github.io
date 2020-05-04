---
title: CloudSim NetworkExample1
tags:
  - CloudSim
categories: 
  - 云计算
date: 2020-02-02
---

CloudSim中的Network包同样含有很多个Example。在NetworkExample1.java文件中，与Example1.java的不同，主要在于模拟之前，需要初始化网络拓扑。即有以下代码：

```java
// load the network topology file
// 直接运行有可能会运行失败，报错找不到toplogy.brite文件
// 方法一：buildNetworkTopology()中的参数改为topology.brite的绝对路径
// 方法二：把topology.brite拷贝到项目的根目录下
NetworkTopology.buildNetworkTopology("topology.brite");

// maps CloudSim entities to BRITE entities
// PowerDatacenter will correspond to BRITE node 0
int briteNode=0;
NetworkTopology.mapNode(datacenter0.getId(),briteNode);

// Broker will correspond to BRITE node 3
briteNode=3;
NetworkTopology.mapNode(broker.getId(),briteNode);
```

<!-- more -->

那么，NetworkTopology这个类的作用是什么呢？

它的实现主要是根据一个brite文件建立一个网络拓扑模型，topology.brite文件如下：

```
Topology: ( 5 Nodes, 8 Edges ) 
Model (1 - RTWaxman): 5 5 5 1 2 0.15000000596046448 0.20000000298023224 1 1 
10.0 1024.0 

Nodes: ( 5 ) 
0 1 3 3 3 -1 RT_NODE 
1 0 3 3 3 -1 RT_NODE 
2 4 3 3 3 -1 RT_NODE 
3 3 1 3 3 -1 RT_NODE 
4 3 3 4 4 -1 RT_NODE 

Edges: ( 8 ) 
0 2 0 3.0 1.1 10.0 -1 -1 E_RT U 
1 2 1 4.0 2.1 10.0 -1 -1 E_RT U 
2 3 0 2.8284271247461903 3.9 10.0 -1 -1 E_RT U 
3 3 1 3.605551275463989 4.1 10.0 -1 -1 E_RT U 
4 4 3 2.0 5.0 10.0 -1 -1 E_RT U 
5 4 2 1.0 4.0 10.0 -1 -1 E_RT U 
6 0 4 2.0 3.0 10.0 -1 -1 E_RT U 
7 1 4 3.0 4.1 10.0 -1 -1 E_RT U 
```

程序运行后会寻找标记`Nodes`和`Edges`，`Nodes`是节点信息，其中第一列是节点序号，第二列是节点的横坐标，第三列是节点的纵坐标；`Edges`是边信息，第一列是边序号，第二列是始节点序号，第三列是终节点序号，第四列是边长度，第五列是边时延，第六列是边带宽。

这里有一个关键类`ToplogicalGraph`，描绘了图的拓扑的数据结构。这里面包含两个链表，分别用来存储节点`ToplogicalNode`和边`ToplogicalLink`。

在`ToplogicalGraph`中通过`readGraphFile`方法，将文件中的描述，转化为网络拓扑模型。接着用得到的网络拓扑，通过`generateMatrices()`和`createBwMatrix()`生成一个是实体间的时延矩阵和带宽矩阵。





