---
title: Android属性动画详解（转载）
tags:
  - 动画
categories: 
  - Android
date: 2018-11-05
---

### 一、属性动画出现的原因

属性动画（Property Animation）是Android3.0（API11）之后的版本中才提供的一种全新的动画模式

#### 背景

实现动画效果在Android开发中非常常见，所以Android系统提供了两种实现动画的方式：

* 逐帧动画（Frame Animation）
* 补间动画（Tweened Animation）

<!-- more -->

#### 缺陷

* 补间动画只能够作用在视图View上，即只可以对一个Button、TextView或者LinearLayout或者其它继承自View的组件进行动画操作，但无法对非View的对象进行动画操作
* 没有改变View的属性，只是改变视觉效果。补间动画只是改变了View的视觉效果，但不会真正改变View的属性。比如通过补间动画将屏幕左上角的按钮移动到右上角，但是点击屏幕右上角仍然是没有反应的，因为实际上按钮仍然在左上角，补间动画只是将其绘制到了屏幕右上角，改变了视觉效果而已
* 动画效果单一。补间动画只能实现平移、旋转、缩放和透明度等简单的动画需求，对于复杂的动画效果，补间动画无法实现

### 二、属性动画简介

* 作用对象：任意Java对象，不再局限于视图View对象
* 实现的动画效果：可以自定义各种动画效果，不再局限于4种基本变换

### 三、工作原理

* 在一定时间间隔内，通过不断对值进行改变，并不断将该值赋给对象的属性，从而实现该对象在该属性上的动画效果
* 具体的工作原理逻辑如下：
* 从上述工作原理中可以看出属性动画有两个非常重要的类：ValueAnimator类和ObjectAnimator类

### 四、使用方法

#### ValueAnimator类

* 定义：属性动画机制中，最核心的一个类
* 实现动画的原理：通过不断控制值的变化，再不断手动赋给对象的属性，从而实现动画效果
* ValueAnimator类中有3个主要方法：
  * `ValueAnimator.ofInt(int values)`
  * `ValueAnimator.ofFloat(float values)`
  * `ValueAnimator.ofObject(int values)`

#### 1.valueAnimator.ofInt(int values)

Java代码设置：
在实际开发中，建议使用Java代码实现属性动画，因为大多数情况下，属性的起始值是无法提前确定的（无法使用XML设置）
```Java
//步骤1：设置动画属性的初始值和结束值
ValueAnimator anim = ValueAnimator.ofInt(0, 3);
//ofInt()的作用有两个
//1.创建动画实例
//2.将传入的多个Int参数进行平滑过渡：此处传入0和3，表示将值从0平滑过渡到3
//如果传入了3个参数a、b、c，则是先从a平滑过渡到b，再从b平滑过渡到c，以此类推

//步骤2：设置动画的各种播放属性
//设置动画运行的时长
anim.setDuration(1000);
//设置动画延迟播放时间
anim.setStartDelay(1000);
//设置动画重复播放次数 = 重放次数 + 1
//动画播放次数 = infinite时，动画无限重复
anim.setRepeatCount(0);
//设置重复播放动画模式
//RESTART（默认）：正序播放
anim.setRepeatMode(ValueAnimator.RESTART);
//REVERSE：倒序回放

//步骤3：将改变的值手动赋值给对象的属性值：
//通过动画的更新监听器，设置值的更新监听器
//即值每次改变、变化一次，该方法就会调用一次
anim.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
  @Override
  public void onAnimationUpdate(ValueAnimator animation) {
    //获得改变后的值
    int currentValue = (Integer) animation.getAnimatedValue();

    //步骤4：将改变后的值赋给对象的属性值
    View.setProperty(currentValue);
    //步骤5：刷新视图，即重新绘制，从而实现动画效果
    View.requestLaytout();
  }
});

//启动动画
anim.start();

```

XML布局文件设置：  
步骤1：在路径res/animator文件夹中创建相对应的动画.xml文件
步骤2：设置动画参数
```XML
<animator
  xmlns:android="http://schemas.android.com/apk/res/android"
  android:valueFrom="0"         //初始值
  android:valueTo="100"         //结束值
  android:valueType="intType"   //变化值类型：floatType & intType

  android:duration="3000"       //动画持续时间（ms），必须设置，动画才有效果
  android:startOffset="1000"    //动画延迟开始时间（ms）
  android:fillBefore="true"     //动画播放完后，视图是否会停留在动画开始的状态，默认为true
  android:fillAfter="false"     //动画播放完后，视图是否会停留在动画结束的状态，优先于fillBefore值，默认为false
  android:fillEnabled="true"    //是否使用fillBefore值，对fillAfter值无影响，默认为true
  android:repeatMode="restart"  //选择重复播放动画模式，restart代表正序播放，reverse代表倒序回放，默认为restart
  android:repeatCount="0"       //重复次数（动画的播放次数=重复次数+1），为infinite时无限重复
  //插值器，影响动画的播放速度
  android:interpolator=@[package:]anim/interpolator_resource
/>
```
步骤3：在Java代码中启动动画
```Java
//载入XML动画
Animator animator = AnimatorInflater.loadAnimator(context, R.animator.animation);
//设置动画对象
animator.setTarget(view);
//启动动画
animator.start();
```

#### 2.valueAnimator.ofInt(float values)

在使用上与ValueAnimator.ofInt(int values)完全没有区别

#### 3.valueAnimator.ofObject()

```Java
//创建初始动画时对象 & 结束动画时的对象
Object object1 = new Object();
Object object2 = new Object();

//创建动画对象 & 设置参数
//参数说明
//参数1：自定义的估值器对象（TypeEvaluator类型参数）
//参数2：初始动画的对象
//参数3：结束动画的对象
ValueAnimator anim = ValueAnimator.ofObject(new objectEvaluator(), object1, object2);

//设置动画属性
anim.setDuration(3000);
//启动动画
anim.start();

```

#### ObjectAnimator类

###### 实现动画的原理
直接对对象的属性值进行改变操作，从而实现动画效果
###### ValueAnimator类与ObjectAnimator类的区别
* ValueAnimator类是先改变值，然后手动赋值给对象的属性从而实现动画；是间接对对象属性进行操作
* ObjectAnimator类是先改变值，然后自动赋值给对象的属性从而实现动画；是直接对对象属性进行操作

###### 使用方法
Java设置
```Java
ObjectAnimator anim = ObjectAnimator.ofFloat(Object object, String property, float ...values);
anim.setDuration(500);
anim.setStartDelay(500);
anim.setRepeatCount(0);
anim.setRepeatMode(ValueAnimator.RESTART);
anim.start();
```
XML设置  
与ValueAnimator一样  

a.透明度：
```Java
mButton = findViewById(R.id.button);
//动作作用的对象是mButton
//动画作者的对象的属性是透明度alpha
//动画效果是：常规 - 全透明 - 常规
ObjectAnimator anim = ObjectAnimator.ofFloat(mButton, "alpha", 1f, 0f, 1f);
anim.setDuration(5000);
anim.start();
```
b.旋转：
```Java
mButton = findViewById(R.id.button);
//动作作用的对象是mButton
//动画作者的对象的属性是旋转rotation
//动画效果是：0 - 360
ObjectAnimator anim = ObjectAnimator.ofFloat(mButton, "rotation", 0f, 360f);
anim.setDuration(5000);
anim.start();
```
c.平移：
```Java
mButton = findViewById(R.id.button);
//获得当前控件的位置
float curTranslationX = mButton.getTranslationX();

//动画作用的对象的属性是X轴平移，translationX
//在Y轴上平移同理，采用属性translationY
//动画效果：从当前位置平移到x=300，再平移到初始位置
ObjectAnimator anim = ObjectAnimator.ofFloat(mButton, "translationX", curTranslationX, 300, curTranslationX);
anim.setDuration(5000);
anim.start();
```
d.缩放：
```Java
mButton = findViewById(R.id.button);

//动画作用的对象的属性是X轴缩放，sacleX
//在Y轴上缩放同理，采用属性scaleY
//动画效果：放大到3倍，再缩小到原始大小
ObjectAnimator anim = ObjectAnimator.ofFloat(mButton, "scaleX", 1f, 3f, 1f);
anim.setDuration(5000);
anim.start();
```

| 属性 | 作用 | 数值类型 |
| :-: | :-: | :-: |
| Alpha | 控制View的透明度 | float |
| TranslationX | 控制X方向的位移 | float |
| TranslationY | 控制Y方向的位移 | float |
| ScaleX | 控制X方向的缩放倍数 | float |
| ScaleY | 控制Y方向的缩放倍数 | float |
| Rotation | 控制以屏幕方向为轴的旋转度数 | float |
| RotationX | 控制以X轴为轴的旋转度数 | float |
| RotationY | 控制以Y轴为轴的旋转度数 | float |
