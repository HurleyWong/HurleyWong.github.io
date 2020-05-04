---
title: Android秋招面试总结（转载）
tags:
  - 面试
categories: 
  - Android
date: 2018-09-19
---

### Android

#### Activity

* Activity的生命周期
* onStart()和onResume()/onPause()和onStop()的区别
* Activity A启动另一个Activity B会回调哪些方法？如果Activity B是完全透明呢？如果启动的是一个Dialog呢？
* 谈谈onSaveInstanceState()方法？何时会调用？
* 如何避免配置改变时Activity重建？
* 优先级低的Activity在内存不足被回收后怎样做可以恢复到销毁前状态？
* 说下Activity的四种启动模式？
* 谈谈singleTop和singleTask的区别以及应用场景
* onNewIntent()调用时机？
* 了解哪些Activity启动模式的标记位？
* 如何启动其他应用的Activity？
* Activity的启动过程？

#### Fragment

* Fragment的生命周期
* Activity和Fragment的异同
* Activity和Fragment的关系
* 何时会考虑使用Fragment

#### Service

* Service的生命周期

* Service的两种启动方式？区别在哪

* 一个Activty先start一个Service后，再bind时会回调什么方法？此时如何做才能回调Service的destory()方法？
* Service如何和Activity进行通信？
* 用过哪些系统Service？
* 是否能在Service进行耗时操作？如果非要可以怎么做？
* AlarmManager能实现定时的原理？
* 前台服务是什么？和普通服务的不同？如何去开启一个前台服务？
* 是否了解ActivityManagerService，谈谈它发挥什么作用？
* 如何保证Service不被杀死？

#### Broadcast Receiver

* 广播有几种形式？什么特点？
* 广播的两种注册形式？区别在哪？

#### ContentProvider

* ContentProvider了解多少？

#### 数据存储

* Android中提供哪些数据持久存储的方法？
* Java中的I/O流读写怎么做？
* SharePreferences适用情形？使用中需要注意什么？
* 了解SQLite中的事务处理吗？是如何做的？
* 使用SQLite做批量操作有什么好的方法吗？
* 如果现在要删除SQLite中表的一个字段如何做？
* 使用SQLite时会有哪些优化操作?

#### IPC

* Android中进程和线程的关系？区别？
* 为何需要进行IPC？多进程通信可能会出现什么问题？
* 什么是序列化？Serializable接口和Parcelable接口的区别？为何推荐使用后者？
* Android中为何新增Binder来作为主要的IPC方式？
* 使用Binder进行数据传输的具体过程？
* Binder框架中ServiceManager的作用？
* Android中有哪些基于Binder的IPC方式？简单对比下？
* 是否了解AIDL？原理是什么？如何优化多模块都使用AIDL的情况？

#### View

* MotionEvent是什么？包含几种事件？什么条件下会产生？
* scrollTo()和scrollBy()的区别？
* Scroller中最重要的两个方法是什么？主要目的是？
* 谈一谈View的事件分发机制？
* 如何解决View的滑动冲突？
* 谈一谈View的工作原理？
* MeasureSpec是什么？有什么作用？
* 自定义View/ViewGroup需要注意什么？
* onTouch()、onTouchEvent()和onClick()关系？
* SurfaceView和View的区别？
* invalidate()和postInvalidate()的区别？

#### Drawable等资源

* 了解哪些Drawable？适用场景？
* mipmap系列中xxxhdpi、xxhdpi、xhdpi、hdpi、mdpi和ldpi存在怎样的关系？
* dp、dpi、px的区别？
* res目录和assets目录的区别？

#### Animation

* Android中有哪几种类型的动画？
* 帧动画在使用时需要注意什么？
* View动画和属性动画的区别？
* View动画为何不能真正改变View的位置？而属性动画为何可以？
* 属性动画插值器和估值器的作用？

#### Window

* Activity、View、Window三者之间的关系
* Window有哪几种类型？
* Activity创建和Dialog创建过程的异同？

#### Handler

* 谈谈消息机制Hander？作用？有哪些要素？流程是怎样的？
* 为什么系统不建议在子线程访问UI？
* 一个Thread可以有几个Looper？几个Handler？
* 如何将一个Thread线程变成Looper线程？Looper线程有哪些特点？
* 可以在子线程直接new一个Handler吗？那该怎么做？
* Message可以如何创建？哪种效果更好，为什么？
* 这里的ThreadLocal有什么作用？
* 主线程中Looper的轮询死循环为何没有阻塞主线程？
* 使用Hanlder的postDealy()后消息队列会发生什么变化？

#### 线程

* Android中还了解哪些方便线程切换的类？
* AsyncTask相比Handler有什么优点？不足呢？
* 使用AsyncTask需要注意什么？
* AsyncTask中使用的线程池大小？
* HandlerThread有什么特点？
* 快速实现子线程使用Handler
* IntentService的特点？
* 为何不用bindService方式创建IntentService？
* 线程池的好处、原理、类型？
* ThreadPoolExecutor的工作策略？
* 什么是ANR？什么情况会出现ANR？如何避免？在不看代码的情况下如何快速定位出现ANR问题所在？

#### Bitmap

* 加载图片的时候需要注意什么？
* LRU算法的原理？
* Android中缓存更新策略？

#### 性能优化

* 项目中如何做性能优化的？
* 了解哪些性能优化的工具？
* 布局上如何优化？列表呢？
* 内存泄漏是什么？为什么会发生？常见哪些内存泄漏的例子？都是怎么解决的？
* 内存泄漏和内存溢出的区别？
* 什么情况会导致内存溢出？

#### Android新特征

* 是否了解和使用过谷歌推出的新技术？
* 有了解刚发布的Android P的特性吗？
* Kotlin对Java做了哪些优化？



### Java

#### 基础

* 面向对象编程的四大特性及其含义
* String、StringBuffer和StringBuilder的区别
* String a = ""和String a = new String("")的关系和异同
* Object的equal()和==的区别
* 装箱、拆箱的含义
* int和Integer的区别
* 遇见过哪些运行时的异常？异常处理机制？
* 什么是反射？有什么作用和应用？
* 什么是内部类？有什么作用？静态内部类和非静态内部类的区别？
* final、finally、finalize()分别表示什么含义？
* 重写和重载的区别？
* 抽象类和接口的异同？
* 为什么匿名内部类中使用局部变量要用final修饰？
* Object有哪些公用方法？

#### 集合

* Java集合框架中有哪些类？都有什么特点？
* 集合、数组、泛型的关系，并比较
* ArrayList和LinkedList的区别
* ArrayList和Vector的区别
* HashSet和TreeSet的区别
* HashMap和HashTable的区别
* HashMap在put、get元素的过程？体现了什么数据结构？
* 如何解决Hash冲突
* 如何保证HashMap线程安全？什么原理？
* HashMap是有序的吗？如何实现有序？
* HashMap是如何扩容的？如何避免扩容？
* hashcode()的作用，与equal()有什么区别？

#### 并发

* 开启一个线程的方法有哪些？销毁一个线程的方法呢？
* 同步和非同步、阻塞和非阻塞的概念
* Thread的join()有什么作用？
* 线程有哪些状态？
* 什么是线程安全？保障线程安全有哪些手段？
* ReentrantLock和synchronized的区别?
* synchronized和volatile的区别？
* synchronized同步代码块还有同步方法本质上锁住的是谁？为什么？
* sleep()和wait()的区别

#### Java新动态

* 是否了解Java1.x的特性吗？
* 谈谈对面向过程编程、面向对象编程还有面向切面编程的理解



### 计算机网络

#### 基础

* 五层协议的体系结构分别是什么？每一层都有哪些协议？
* 为什么有MAC地址还要IP地址？

#### TCP

* TCP和UDP的区别？
* 拥塞控制和流量控制都是什么，两者的区别？
* 谈谈TCP为什么要三次握手？为什么要四次握手？
* 播放视频用TCP还是UDP？为什么？

#### HTTP

* 了解哪些响应状态码？

* get和post的区别？

* Http1.0、Http1.1、Http2.0的区别？

* HTTP和TCP的区别？

* HTTP和HTTPS的区别？
  HTTP和Socket的区别？

* 在地址栏输入http://www.baidu.com会发生什么？

  A：地址链接会转化为https://www.baidu.com



### 操作系统

* 操作系统中进程和线程的区别？
* 死锁的产生和避免？



### 数据结构和算法

* 怎么理解数据结构？
* 什么是斐波那契数列？
* 迭代和递归的特点，并比较优缺点
* 了解哪些查找算法，时间复杂度都是多少？
* 了解哪些排序算法，并比较一下以及适用场景
* 快排的基本思路是什么？最差的时间复杂度是多少？如何优化？
* AVL树插入或删除一个节点的过程是怎样的？
* 什么是红黑树？
* （手写算法）二分查找
* （手写算法）反转链表
* （手写算法）用两个栈实现队列
* （手写算法）多线程轮流打印问题
* （手写算法）如何判断一个链有环/两条链交叉
* （手写算法）快速从一组无序数中找到第k大的数/前k个大的数
* （手写算法）最长（不）重复子串



### 设计模式

* 谈谈MVC、MVP和MVVM，好在哪里，不好在哪里？
* 如何理解生产者消费者模型？
* 是否能从Android中举几个例子说说用到了什么设计模式？
* 装饰模式和代理模式有哪些区别？
* 实现单例模式有几种方法？懒汉式中双层锁的目的是什么？两次判空的目的是什么？
* 谈谈了解的设计模式原则



### 数据库

* 数据库中的事务了解吗？事务的四大特性？
* 如何理解数据库的范式？



### 版本

* 使用过哪些版本控制工具？git和svn的区别？
* 了解git工具吗？用过哪些命令？了解冲突时的git merge和git rebase的区别？



### HR问题

* 简单介绍一下自己
* 谈谈项目经历，为什么会做，怎么做的，遇到的难点？
* 谈谈实习经历，做了什么，有哪些收获？
* 谈谈学习Android的经历，有哪些学习方法和技巧？
* 是否会考研，为何不考研？
* 成绩怎么样？奖学金情况？
* 职业规划？
* 为什么想来我们公司，为何不留在XXX？
* 对公司是否有了解？
* 为什么会选择做技术？对女生做开发的看法？
* 还投过哪些公司，进展如何？
* 家是哪里的？
* 平时有哪些兴趣爱好？大学参加了了哪些校园活动？
* 有女朋友吗？未来有什么规划？
* 评价一下自己的优缺点？用一些词形容你自己，别人都是怎样评价你的？
* 觉得自己的优势是什么？
* 如何看待加班？
* 意向工作城市是哪？是否考虑在XX长期发展？
* 对于薪酬有什么想法？
* 还有什么问题要问我的吗？



