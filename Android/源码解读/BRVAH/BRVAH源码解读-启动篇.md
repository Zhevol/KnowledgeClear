### BRVAH 源码解读 - 启动篇

#### 一、BRVAH 简介

　　BRVAH 是 BaseRecyclerViewAdapterHelper 的简称，它是针对于 RecyclerView 的内容适配器的一个开源框架。作为一个开发者，在使用的过程中能真实的体会到这个框架的强大。同时，阅读及解析这个框架，能够更有利于以后在开发中使用这个框架，进而提高自己的分析能力。对于其中包含的一些设计和操作的思想，做一个汲取和整理，有利于个人的进步。

　　If I have seen further,it is by standing on the shoulders of giants.　　——Isaac Newton

　　如果说我比别人看得更远，那是因为我站在巨人的肩膀上。　　——牛顿

#### 二、 BRVAH 的包结构

　　![BRVAH 的包结构](/pictures/BRVAH包结构.png)

　　将以上未展开的包，展开后如下图所示：

　　![BRVAH 的包结构](/pictures/BRVAH各个包展开后的内容.png)

　　从上面这两张图上，可以了解到以下信息：

- animation：这个包下面，包含了动画相关的类，每一个类，都定义了一个动画的类型。其中 BaseAnimation 是接口类，其他几个类都是一个独立的动画类；
- callback：这个包下面，只有一个类，这个类定义了 RecyclerView 的子项的拖动及刷新操作的回调；
- entity：这个包下面，有四个类，其中两个是接口类型，两个是抽象类类；
- listener：这个包下面，有六个类，分别实现对不同事件类型的监听，其中两个是接口类，其他四个是抽象类；
- loadmore：这个包下面，有两个类，定义了加载更多的视图；
- util：这个包下面，有两个类，其中一个是多类型的代理，另一个是触摸事件的方法类；
- 其他的类：剩余的五个类，其中四个是实现不同类型的 RecyclerView 的内容适配器的各个抽象类；还有一个类，是一个基础的 BaseViewHolder 类，用于管理控件。

#### 三、BRVAH 的解读计划安排

　　本篇源码解读计划，拟以从上到下，从辅助包（第二部分中见到的各个包）到内容适配器的核心实现类的顺序进行解读。从源码的角度，解读 BRVAH 框架的实现过程。进而分析其优势与劣势、实现思想、架构思想，从而完善自己对于此框架的知识体系的认知及架构体系的熟悉。在此基础上，对该框架进行拓展与优化，更上一层楼。