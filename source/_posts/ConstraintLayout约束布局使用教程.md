---
title: ConstraintLayout约束布局使用教程
tags:
  - UI界面
categories: 
  - Android
date: 2018-10-13
---

目前最新版的AndroidStudio默认的布局方式就是使用ConstraintLayout布局，因为一些复杂的布局可以使用ConstraintLayout实现而不再需要像以前一样嵌套很多层布局，从而能够提升性能。

### 一、相关资源

[ConstraintLayout官方文档（英文）](https://developer.android.google.cn/reference/android/support/constraint/ConstraintLayout)

[郭霖-ConstraintLayout完全解析](https://blog.csdn.net/guolin_blog/article/details/53122387)

<!-- more -->

### 二、相对定位

#### 属性列表

* layout_constraintLeft_toLeftOf
* layout_constraintLeft_toRightOf
* layout_constraintRight_toLeftOf
* layout_constraintRight_toRightOf
* layout_constraintStart_toEndOf
* layout_constraintStart_toStartOf
* layout_constraintEnd_toStartOf
* layout_constraintEnd_toEndOf
* layout_constraintTop_toTopOf
* layout_constraintTop_toBottomOf
* layout_constraintBottom_toTopOf
* layout_constraintBottom_toBottomOf
* layout_constraintBaseline_toBaselineOf

![](https://github.com/HurleyJames/ImageHosting/blob/master/ConstraintLayout相对定位说明.png?raw=true)

### 三、边距（Margins）

### 四、偏向（Bias）

* layout_constraintHorizontal_bias
* layout_constraintVertical_bias

![](https://github.com/HurleyJames/ImageHosting/blob/master/ConstraintLayout偏向.png?raw=true)

Bias当控件两边（上下或者左右）都有约束的时候，默认为bias约束，可以使用bias的两个属性来控制偏向哪边。

### 五、尺寸限制（Dimensions Constraints)

ConstraintLayout自身有以下最大最小尺寸限制：

* android:minWidth
* android:minHeight
* android:maxWidth
* android:maxHeight

0dp，等于match_constraint，官方建议使用match_constraint而不是使用match_parent

注意，控件会和约束控件一样宽高，并不是和ConstraintLayout一样宽高

### 六、比例（Ratio）

可以用比例去定义View的宽高，需要以下条件：

* 至少一个约束尺寸设置为0dp（即match_constraint）
* 为属性layout_constraintDimentionRatio设置比例

### 七、链条（chain）

### 八、辅助线（Guideline）

Guideline只用于ConstraintLayout中，是一个工具类，不会被显示，仅仅用于辅助布局。

它可以是horizontal或vertical的。

* vertical的Guideline宽度为零，高度为ConstraintLayout的高度
* horizontal的Guideline高度为零，宽度为ConstraintLayout的宽度

定位Guideline有三种方式：

* 指定距离左侧或顶部的固定距离 layout_constraintGuide_begin
* 指定距离右侧或底部的固定距离 layout_constraintGuide_end
* 指定在父控件中的宽度或高度的百分比 layout_constraintGuide_percent









