---
title: Latex数学公式
tags:
  - Latex
categories: 
  - 效率
date: 2019-10-30
---

## 概念

> [**LaTeX**](**LaTeX**（/ˈlɑːtɛx/，常被读作/ˈlɑːtɛk/或/ˈleɪtɛk/，写作"LaTeX"），是一种基于[TeX](https://zh.wikipedia.org/wiki/TeX)的[排版](https://zh.wikipedia.org/wiki/排版)系统，由[美国](https://zh.wikipedia.org/wiki/美国)[计算机科学](https://zh.wikipedia.org/wiki/计算机科学)家[莱斯利·兰伯特](https://zh.wikipedia.org/wiki/莱斯利·兰伯特)在20世纪80年代初期开发，利用这种格式系统的处理，即使用户没有排版和程序设计的知识也可以充分发挥由TeX所提供的强大功能，不必一一亲自去设计或校对，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和[数学](https://zh.wikipedia.org/wiki/数学)公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的[科技](https://zh.wikipedia.org/wiki/科技)和数学、物理文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。)（/ˈlɑːtɛx/，常被读作/ˈlɑːtɛk/或/ˈleɪtɛk/，写作“LaTeX”），是一种基于[TeX](https://zh.wikipedia.org/wiki/TeX)的[排版](https://zh.wikipedia.org/wiki/排版)系统，由[美国](https://zh.wikipedia.org/wiki/美国)[计算机科学](https://zh.wikipedia.org/wiki/计算机科学)家[莱斯利·兰伯特](https://zh.wikipedia.org/wiki/莱斯利·兰伯特)在20世纪80年代初期开发，利用这种格式系统的处理，即使用户没有排版和程序设计的知识也可以充分发挥由TeX所提供的强大功能，不必一一亲自去设计或校对，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和[数学](https://zh.wikipedia.org/wiki/数学)公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的[科技](https://zh.wikipedia.org/wiki/科技)和数学、物理文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

## 基础

Latex的数学模式有两种：

<!-- more -->

* 行内模式（inline）：前者在正文的行文中，插入数学公式；使用`$...$`插入行内公式。
* 行间模式（display）：独立排列单独成行，并自动居中；使用`$$...$$`插入行间公式

> 行内公式也可以使用 `\(...\)` 或者 `\begin{math} ... \end{math}` 来插入。
>
> 行间公式也可以使用`\[ ... \] ` 或者 `\begin{displaymath} ... \end{displaymath}` 来插入。

Latex中最常用的特殊符号是`{}`和`\`，`{}`会把包含在中间的元素看成一个整体，`\`后面通过连接一些字母来表示符号。

## 基础数学符号

### 重音符

|    符号     |   写法    |    符号     |   写法    |
| :---------: | :-------: | :---------: | :-------: |
|  $\hat{a}$  |  \hat{a}  | $\acute{a}$ | \acute{a} |
|  $\bar{a}$  |  \bar{a}  |  $\dot{a}$  |  \dot{a}  |
| $\breve{a}$ | \breve{a} | $\check{a}$ | \check{a} |
| $\grave{a}$ | \grave{a} |  $\vec{a}$  |  \vec{a}  |
| $\ddot{a}$  | \ddot{a}  | $\tilde{a}$ | \tilde{a} |

#### 向量

|         符号          |        写法         |
| :-------------------: | :-----------------: |
|       $\vec{a}$       |       \vec{a}       |
| $\overrightarrow{AB}$ | \overrightarrow{AB} |
| $\overleftarrow{AB}$  | \overleftarrow{AB}  |

#### 加粗、斜体等

|  描述  |       符号        |      写法       |
| :----: | :---------------: | :-------------: |
|  加粗  |  $\textbf{abc}$   |  \textbf{abc}   |
|  斜体  |  $\textit{abc}$   |  \textit{abc}   |
| 下划线 | $\underline{abc}$ | \underline{abc} |
| 上划线 | $\overline{abc}$  | \overline{abc}  |

### 希腊字母

|    符号     |   写法    |    符号     |   写法    |     符号      |    写法     |
| :---------: | :-------: | :---------: | :-------: | :-----------: | :---------: |
|  $\alpha$   |  \alpha   |   $\beta$   |   \beta   |   $\gamma$    |   \gamma    |
|  $\delta$   |  \delta   | $\epsilon$  | \epsilon  | $\varepsilon$ | \varepsilon |
|   $\zeta$   |   \zeta   |   $\eta$    |   \eta    |   $\theta$    |   \theta    |
| $\vartheta$ | \vartheta |   $\iota$   |   \iota   |   $\kappa$    |   \kappa    |
|  $\lambda$  |  \lambda  |    $\mu$    |    \mu    |     $\nu$     |     \nu     |
|    $\xi$    |    \xi    |     $o$     |     o     |     $\pi$     |     \pi     |
|  $\varpi$   |  \varpi   |   $\rho$    |   \rho    |   $\varrho$   |   \varrho   |
|  $\sigma$   |  \sigma   | $\varsigma$ | \varsigma |    $\tau$     |    \tau     |
|   $\rho$    |   \rho    |   $\phi$    |   \phi    |   $\varphi$   |   \varphi   |
|   $\chi$    |   \chi    |   $\psi$    |   \psi    |   $\omega$    |   \omega    |
|  $\Gamma$   |  \Gamma   |  $\Delta$   |  \Delta   |   $\Theta$    |   \Theta    |
|  $\Lambda$  |  \Lambda  |    $\Xi$    |    \Xi    |     $\Pi$     |     \Pi     |
|  $\Sigma$   |  \Sigma   | $\Upsilon$  | \Upsilon  |    $\Phi$     |    \Phi     |
|   $\Psi$    |   \Psi    |  $\Omega$   |  \Omega   |               |             |

**Tips**：

* $\delta$：德尔塔，数学中两个函数的名称

* $\epsilon$：埃普西隆。与$\varepsilon$似乎表示同一个意思。

  > * 数学： 
  >   * [非常小](https://zh.wikipedia.org/wiki/極限)
  >   * [集合](https://zh.wikipedia.org/wiki/集合)的关系中，表示“属于”的“[∈](https://zh.wikipedia.org/wiki/∈)”符号
  >   * [列维-齐维塔符号](https://zh.wikipedia.org/wiki/列維-齊維塔符號)（符号Levi-Civita）
  >
  > * [计算机科学](https://zh.wikipedia.org/wiki/電腦科學)： 

* $\Gamma$：伽马，大写时在数学中表示$\Gamma$函数，和阶乘有关

* $\Theta$：大写时在数学中表示大$\Theta$函数，是[大O符号](https://zh.wikipedia.org/wiki/大O符号)和[大Ω符号](https://zh.wikipedia.org/wiki/大Ω符号)的结合。即：

  $f(v)=\Theta[g(v)]，若\begin{cases}f(v)=O[g(v)]\\f(v)=\Omega[g(v)]\end{cases}$

### 二元运算

|        符号        |       写法       |   符号    |  写法   |
| :----------------: | :--------------: | :-------: | :-----: |
|       $\pm$        |       \pm        |  $\cap$   |  \cap   |
|     $\diamond$     |     \diamond     | $\oplus$  | \oplus  |
|       $\mp$        |       \mp        |  $\cup$   |  \cup   |
|  $\bigtriangleup$  |  \bigtriangleup  | $\ominus$ | \ominus |
|      $\times$      |      \times      | $\uplus$  | \uplus  |
| $\bigtriangledown$ | \bigtriangledown | $\otimes$ | \otimes |
|       $\div$       |       \div       | $\sqcap$  | \sqcap  |
|  $\triangleleft$   |  \triangleleft   | $\oslash$ | \oslash |
|       $\ast$       |       \ast       | $\sqcup$  | \sqcup  |
|  $\triangleright$  |  \triangleright  |  $\odot$  |  \odot  |
|      $\star$       |      \star       |  $\vee$   |  \vee   |

### 关系运算

|    符号     |   写法    |    符号     |   写法    |   符号    |  写法   |
| :---------: | :-------: | :---------: | :-------: | :-------: | :-----: |
| $\leq,\le$  | \leq,\le  | $\geq, \ge$ | \geq, \ge | $\equiv$  | \equiv  |
|  $\models$  |  \models  |   $\prec$   |   \prec   |  $\succ$  |  \succ  |
|   $\sim$    |   \sim    |  $\preceq$  |  \preceq  | $\succeq$ | \succeq |
|  $\simeq$   |  \simeq   |   $\mid$    |   \mid    |   $\ll$   |   \ll   |
|    $\gg$    |    \gg    | $\parallel$ | \parallel | $\subset$ | \subset |
|  $\supset$  |  \supset  |  $\approx$  |  \approx  | $\bowtie$ | \bowtie |
| $\subseteq$ | \subseteq | $\supseteq$ | \supseteq |  $\cong$  |  \cong  |
| $\sqsubset$ | \sqsubset | $\sqsupset$ | \sqsupset |  $\neq$   |  \neq   |
|    $\in$    |    \in    |    $\ni$    |    \ni    |    $=$    |    =    |
|  $\vdash$   |  \vdash   |  $\dashv$   |  \dashv   |    $<$    |    <    |
|     $>$     |     >     |     $:$     |     :     | $\notin$  | \notin  |

### 大尺寸运算符

|     符号     |    写法    |    符号     |   写法    |    符号     |   写法    |
| :----------: | :--------: | :---------: | :-------: | :---------: | :-------: |
|    $\sum$    |    \sum    |   $\prod$   |   \prod   |  $\coprod$  |  \coprod  |
|    $\int$    |    \int    |   $\oint$   |   \oint   |  $\bigcap$  |  \bigcap  |
| $\bigotimes$ | \bigotimes | $\bigoplus$ | \bigoplus | $\biguplus$ | \biguplus |

### 箭头符号

|         符号         |        写法        |         符号          |        写法         |      符号      |     写法     |
| :------------------: | :----------------: | :-------------------: | :-----------------: | :------------: | :----------: |
|     $\leftarrow$     |     \leftarrow     |   $\longleftarrow$    |   \longleftarrow    |   $\uparrow$   |   \uparrow   |
|     $\Leftarrow$     |     \Leftarrow     |   $\Longleftarrow$    |   \Longleftarrow    |   $\Uparrow$   |   \Uparrow   |
|    $\rightarrow$     |    \rightarrow     |   $\longrightarrow$   |   \longrightarrow   |  $\downarrow$  |  \downarrow  |
|  $\leftrightarrow$   |  \leftrightarrow   | $\longleftrightarrow$ | \longleftrightarrow | $\updownarrow$ | \updownarrow |
|  $\Leftrightarrow$   |  \Leftrightarrow   | $\Longleftrightarrow$ | \Longleftrightarrow | $\Updownarrow$ | \Updownarrow |
|      $\mapsto$       |      \mapsto       |     $\longmapsto$     |     \longmapsto     |   $\nearrow$   |   \nearrow   |
|      $\mapsto$       |   \hookleftarrow   |   $\hookrightarrow$   |   \hookrightarrow   |   $\searrow$   |   \searrow   |
|   $\leftharpoonup$   |   \leftharpoonup   |   $\rightharpoonup$   |   \rightharpoonup   |   $\swarrow$   |   \swarrow   |
|  $\leftharpoondown$  |  \leftharpoondown  |  $\rightharpoondown$  |  \rightharpoondown  |   $\nwarrow$   |   \nwarrow   |
| $\rightleftharpoons$ | \rightleftharpoons |        $\iff$         |        \iff         |   $\leadsto$   |   \leadsto   |

### 分隔符号

|     符号     |    写法    |      符号      |     写法     |      符号      |     写法     |
| :----------: | :--------: | :------------: | :----------: | :------------: | :----------: |
|  $\uparrow$  |  \uparrow  |   $\Uparrow$   |   \Uparrow   |  $\downarrow$  |  \downarrow  |
| $\Downarrow$ | \Downarrow | $\updownarrow$ | \updownarrow | $\Updownarrow$ | \Updownarrow |
|     $/$      |     /      |  $\backslash$  |  \backslash  |    $\vert$     |    \vert     |
|   $\Vert$    |   \Vert    | $\rmoustache$  | \rmoustache  | $\lmoustache$  | \lmoustache  |
|  $\rgroup$   |  \rgroup   |   $\lgroup$    |   \lgroup    |  $\arrowvert$  |  \arrowvert  |
| $\Arrowvert$ | \Arrowvert |  $\bracevert$  |  \bracevert  |     $\mid$     |     \mid     |
|     $($      |     (      |      $)$       |      )       |      $[$       |      [       |
|     $]$      |     ]      |                |              |                |              |

### 杂类符号

|      符号      |     写法     |     符号     |    写法    |     符号     |    写法    |
| :------------: | :----------: | :----------: | :--------: | :----------: | :--------: |
|    $\dots$     |    \dots     |   $\cdots$   |   \cdots   |   $\vdots$   |   \vdots   |
|    $\ddots$    |    \ddots    |   $\aleph$   |   \aleph   |   $\prime$   |   \prime   |
|   $\forall$    |   \forall    |   $\infty$   |   \infty   |   $\hbar$    |   \hbar    |
| $\varnothing$  | \varnothing  |  $\exists$   |  \exists   |   $\nabla$   |   \nabla   |
|    $\surd$     |    \surd     |    $\Box$    |    \Box    | $\triangle$  | \triangle  |
|   $\Diamond$   |   \Diamond   |   $\imath$   |   \imath   |   $\jmath$   |   \jmath   |
|     $\ell$     |     \ell     |    $\neg$    |    \neg    |    $\top$    |    \top    |
|    $\flat$     |    \flat     |  $\natural$  |  \natural  |   $\sharp$   |   \sharp   |
|     $\wp$      |     \wp      |    $\bot$    |    \bot    | $\clubsuit$  | \clubsuit  |
| $\diamondsuit$ | \diamondsuit | $\heartsuit$ | \heartsuit | $\spadesuit$ | \spadesuit |
|     $\mho$     |     \mho     |    $\Re$     |    \Re     |    $\Im$     |    \Im     |
|    $\angle$    |    \angle    |  $\partial$  |  \partial  | $\emptyset$  | \emptyset  |
|  $\ulcorner$   |  \ulcorner   | $\urcorner$  | \urcorner  | $\llcorner$  | \llcorner  |
|  $\lrcorner$   |  \lrcorner   |              |            |              |            |

### 曲线函数符号

|   符号    |  写法   |   符号    |  写法   |  符号   | 写法  |
| :-------: | :-----: | :-------: | :-----: | :-----: | :---: |
| $\arccos$ | \arccos |  $\cos$   |  \cos   | $\exp$  | \exp  |
|  $\ker$   |  \ker   | $\limsup$ | \limsup | $\min$  | \min  |
|  $\sinh$  |  \sinh  | $\arcsin$ | \arcsin | $\cosh$ | \cosh |
|  $\deg$   |  \deg   |  $\gcd$   |  \gcd   |  $\lg$  |  \lg  |
|   $\ln$   |   \ln   |   $\Pr$   |   \Pr   | $\sup$  | \sup  |
| $\arctan$ | \arctan |  $\cot$   |  \cot   | $\det$  | \det  |
|  $\hom$   |  \hom   |  $\lim$   |  \lim   | $\log$  | \log  |
|  $\sec$   |  \sec   |  $\tan$   |  \tan   | $\tan$  | \tan  |
|  $\arg$   |  \arg   |  $\coth$  |  \coth  | $\dim$  | \dim  |
|  $\inf$   |  \inf   | $\liminf$ | \liminf | $\max$  | \max  |
|  $\sin$   |  \sin   |  $\tanh$  |  \tanh  |         |       |

### 数字字母

|        符号         |       写法        |
| :-----------------: | :---------------: |
|  $\mathrm{ABCdef}$  |  \mathrm{ABCdef}  |
|  $\mathit{ABCdef}$  |  \mathit{ABCdef}  |
| $\mathcal{ABCdef}$  | \mathcal{ABCdef}  |
| $\mathscr{ABCdef}$  | \mathscr{ABCdef}  |
| $\mathfrak{ABCdef}$ | \mathfrak{ABCdef} |
|  $\mathbb{ABCdef}$  |  \mathbb{ABCdef}  |

## 数学公式

### 一般数学结构

|        符号        |       写法       |      符号       |     写法      |       符号        |      写法       |
| :----------------: | :--------------: | :-------------: | :-----------: | :---------------: | :-------------: |
| $\widetilde{abc}$  | \widetilde{abc}  | $\widehat{abc}$ | \widehat{abc} | $\overbrace{abc}$ | \overbrace{abc} |
| $\underbrace{abc}$ | \underbrace{abc} |  $\sqrt{abc}$   |  \sqrt{abc}   |  $\sqrt[n]{abc}$  |  \sqrt[n]{abc}  |
| $\frac{abc}{xyz}$  | \frac{abc}{xyz}  | $\dbinom{n}{r}$ | \dbinom{n}{r} |                   |                 |

### 矩阵

```latex
\begin{matrix} x&y\\z&v \end{matrix}
\begin{vmatrix} x&y\\z&v \end{vmatrix}
\begin{bmatrix} x&y\\z&v \end{bmatrix}
\begin{pmatrix} x&y\\z&v \end{pmatrix}
```

$\begin{matrix} x&y\\z&v \end{matrix}
\begin{vmatrix} x&y\\z&v \end{vmatrix}
\begin{bmatrix} x&y\\z&v \end{bmatrix}
\begin{pmatrix} x&y\\z&v \end{pmatrix}$

### 分段函数

分段函数可以用`cases`实现

```latex
y=\begin{cases}
-x,& x\leq 0 \\
x,& x>0
\end{cases}
```

$y=\begin{cases}
-x,& x\leq 0 \\
x,& x>0
\end{cases}$

### 对齐

对齐的公式可以使用`align`实现，对齐则可以使用`$`实现。

```latex
\begin{align}
x = a&+b+c+ \\
d&+e+f+g
\end{align}
```

$\begin{align}x = a&+b+c+ \\d&+e+f+g\end{align}$

### 公式组

无需对齐的公式组可以使用`gather`环境，需要对齐的公式组可以使用`align`环境。

```latex
\begin{gather}
a = b+c+d \\
x = y+z
\end{gather}
```

$\begin{gather}a = b+c+d \\x = y+z\end{gather}$

```latex
\begin{align}
a &= b+c+d \\
x &= y+z
\end{align}
```

$\begin{align}a &= b+c+d \\x &= y+z\end{align}$

## 常见问题

### 插入大括号

```latex
A = \left\{B\right\}
```

$A=\left\{B\right\}$

### 下标正下方

* 如果是数学符号，那么用\limits命名就能放在正下方

  ```latex
  \sum\limits_{i}
  ```

  $\sum\limits_{i}$

* 如果是普通符号，则用\mathop先转换成数学符号后再用\limits

  ```latex
  \mathop{Q}\limits_{^}
  ```

  $\mathop{Q}\limits_{i}$

