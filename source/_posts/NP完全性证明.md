---
title: NP完全性证明
tags:
  - NP问题
categories: 
  - 图论
date: 2019-12-24
top_img: https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Awaiting.jpg
---

## NP完全性的证明

**引理**：如果语言L是一种满足对任意$L'\in NPC$都有$L'\le_{p}L$的语言，则L是NP-hardness。此外，如果$L\in NP$，则$L\in NPC$。

**证明**：

$\because L'\in NPC\\
\therefore 对于所有L''\in NP，都有L''\le _{p}L'\\
根据假设，L'\le _{p}L\\
\therefore 根据传递性，L''\in _{p}L\\
\therefore L是NP-hardness\\
那么，如果L\in NP，且L是NP-hardness\\
\therefore L\in NPC$

<!-- more -->

### 证明某种语言L是NP完全问题的方法

1. 证明$L\in NP$
2. 选取一种已知的NP完全语言L'
3. 描述一种可计算函数f(x)的算法，其中f可将L'中每一个实例$x\in \left\{0,1\right\}^*$映射为L中的实例$f(x)$
4. 证明函数f满足$x\in L'$当前仅当对于所有的$x\in \left\{0,1\right\}^*$都有$f(x)\in L$
5. 证明计算函数$f(x)$的算法具有多项式运行时间

第2步~第5步是为了证明L是NP-hardness，然后结合第一步的L是NP问题，就可以得出$L\in NPC$。

## 典型NPC问题

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/%E6%89%AB%E6%8F%8F%202019%E5%B9%B412%E6%9C%8824%E6%97%A5%2023.33.JPG)

* **SAT**：布尔公式的可满足性问题
* **3-CNF-SAT**：3合取范式的布尔公式的可满足性问题
* **团问题CLIQUE**：寻找无向图中的最大团
* **顶点覆盖问题VERTEX COVER**：在无向图中找出最小规模的顶点覆盖
* **哈密顿回路问题HAM-CYCLE**：无向图中是否存在哈密顿回路，即通过每个顶点的简单回路
* **旅行商问题TSP**：寻找通过无向图每个顶点一次的最小回路
* **子集和问题SUBSET-SUM**：给定正整数集合和正整数t，判断是否存在一个子集的元素和为t

## 布尔组合电路

布尔组合电路由一个或多个布尔组合元素通过线路连接而成，布尔组合电路是不包括回路的。

一个布尔组合电路的**真值赋值**是指一组布尔输入值。如果一个单输出布尔组合电路具有可满足性赋值，则称该布尔组合电路是可满足的。

布尔值取自集合$\left\{0,1\right\}$，0代表false，1代表true。

布尔组合元素称为逻辑门：$\begin{cases}与门\quad AND\\或门\quad OR\\非门\quad NOT\end{cases}$

For example：

1. 对此电路的输入赋值$<x_1=1, x_2=1, x_3=0>$，使得电路的输出为1，那么电路是可满足的。
2. 如果对此电路输入的任何一种赋值都不能使得输出为1，则电路不满足。

### NP完全性证明

给定一个电路C，通过检查输入的所有可能赋值来确定它是否来自可满足性电路。

那么，如果有k个输入，就有检查$2^k$种可能，因为$\begin{cases}1\\0\end{cases}$

所以当电路C的规模为k的多项式时，对每个电路的检查要花费$\Omega(2^k)$的时间，呈多项式关系。

$\therefore$ 该问题是NP完全的

## 布尔可满足性问题SAT

**定理**：布尔公式的可满足性问题是NP完全的。

**证明**：

1. 证明$SAT\in NP$，即证明对于输入公式$\phi$，由它的一个可满足性赋值所组成的证书可以在多项式时间内得到验证
2. 证明$CIRCUIT-SAT\le _{p}SAT$从而得出SAT是NP-hard
3. 根据语言$L\in NP$且$L\in NP-hard$能推出$L\in NPC$，得证

## 3-CNF可满足性

即布尔公式中的一个文字（literal）是指一个变量或非“$\neg$”。

### 合取范式

如果一个布尔公式可以表示为所有子句的“与”，并且每个字句都是一个或多个文字的“或”，则称该布尔公式为合取范式。

如果每个字句恰好有三个不同的**“文字”**，则该布尔公式为3合取范式，即3-CNF。

For example：

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/%E5%90%88%E5%8F%96.png)

**定理**：3合取范式形式的布尔公式的可满足性是NP完全的。

**证明**：要证明$3-CNF-SAT\le NP$，仅需证明$SAT\le _{p}3-CNF-SAT$。

## 团问题CLIQUE

无向图G=(V,E)的团(clique)是一个顶点子集$V'\subseteq V$，其中每一对顶点之间都由E中的一条边来连接。

一个团是G中的一个完全子图，**图的规模是指它所包含的顶点数**。

团问题就是关于寻找图中规模最大的团的优化问题。

事实上，团问题的有效算法是不大可能存在的。因为要确定一个具有$|V|$个顶点的无向图G=(V,E)是否包含一个规模为k的团，有一种朴素算法：

列出V的所有规模为k的子集，对其中的每一个进行检查，看它是否是一个团。这个算法的运行时间是与k有关。如果k是常数，那么该算法的运行时间是多项式时间的。然而，在一般情况下，k可能接近于$|V|/2$。这样的话，运行时间就是超多项式时间。所以，团问题的有效算法是不大可能存在的。

### 形式语言定义

$CLIQUE=\left\{<G,k>:G是一个包含规模为k的团的图\right\}$

**定理**：$CLIQUE\subseteq NP-Complete$

**证明**：首先，证明$CLIQUE\in NP$。然后，证明$CLIQUE\in NP-hard$

1. 对于一个给定的图G=(V,E)，用图中顶点集$V'\subseteq V$作为G的一个证书。对于任意一对顶点$\mu,\nu\in V'$，通过检查边$(\mu,\nu)$是否属于E，就可以在多项式时间内确定V'是否是团。
2. 通过证明$3-CNF-SAT\le _{p}CLIQUE$来说明$CLIQUE\in NP-hard$。

## 顶点覆盖问题Vertex Cover

无向图G=(V,E)的顶点覆盖是一个子集$V'\subseteq V$，满足如果有$(\mu,\nu)\in E$，则$\mu\in V'$或$\nu\in V'$（或两者同时成立）。

顶点覆盖的规模是指它所包含的顶点数。顶点覆盖问题就是在一个给定的图中，找出具有最小规模的顶点覆盖。

### 形式语言定义

$VERTEX-COVER=\left\{<G,k>:图G有一个规模为k的顶点覆盖\right\}$

**定理**：$VC\subseteq NP-Complete$

**证明**：首先，证明$VC\in NP$。然后证明$CLIQUE\le _{p}VC$从而得到$VC\in NP-hard$

## 哈密顿回路问题HAM-CYCLE

**定理**：哈密顿回路问题是NP-Complete

**证明**：首先，证明$HAM-CYCLE\in NP$。然后通过证明$VC\le _{p}HAM-CYCLE$从而得到$HAM-CYCLE\in NP-hard$

## 旅行商问题TSP

### 形式语言定义

$TSP=\left\{<G,c,k>:G=(V,E)是一个完全图，c是V*V\rightarrow Z上的一个函数，k\in Z，G中包含一个最大花费为k的旅行回路。\right\}$

**定理**：旅行商问题是NP-Complete

**证明**：首先，证明$TSP\in NP$。然后通过证明$HAM-CYCLE\le _{p}TSP$从而得到$TSP\in NP-hard$

## 子集和问题SUBSET-SUM problem

给定一个正整数有限集S和一个整数目标t>0，问是否存在一个子集$S'\subseteq S$，其元素和为t。

### 形式语言定义

$SUBSET-SUM=\left\{<S,t>:存在一个子集S'\subseteq S，使得t= \sum\limits_{S\in S'}S\right\}$

**定理**：子集和问题是NP-Complete

**证明**：首先，证明$SUBSET-SUM\in NP$。然后，通过证明$3-CNF-SAT\le _{p}SUBSET-SUM$从而得到$SUBSET-SUM\in NP-hard$





















