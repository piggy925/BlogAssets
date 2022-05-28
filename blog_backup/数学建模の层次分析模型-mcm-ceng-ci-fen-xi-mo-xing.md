## 层次分析模型
---

层次分析模型是建模比赛中最基础的模型之一，主要用于解决各种评价类问题，例如：选择哪种方案更好、哪位员工更优秀等等。

> 层次分析法的一道例题：
>
> 填好志愿后，小明同学想出去旅游。在查阅了网上的攻略后，他初步选择了苏杭、北戴河和桂林三地之一作为目标景点。
> 请你**确定评价指标、形成评价体系**来为小明同学选择最佳的方案。

一般见到**确定评价指标、形成评价体系**等字样基本可以确定属评价类问题。

在解决评价类问题时，首先要想到三个问题：

1. 我们的评价**目标**是什么？

   在上面的例题中：就是选择最佳的旅游景点。

2. 我们为了达到这个目标有哪几种可选的**方案**？

   在上面的例题中：有三种，苏杭、北戴河和桂林。

3. 评价的**准则**或者说指标是什么？（我们根据什么东西来评价好坏）

   评价的标准题目中往往不会直接给出，需要我们根据题目中的**背景材料、常识以及网上搜集到的参考资料**进
   行结合，从中筛选出最合适的指标。

   优先选择知网（或者万方、百度学术、谷歌学术等平台）搜索相关的文献。推荐[虫部落学术搜索](https://scholar.chongbuluo.com/)。

   

针对上面的例题：

假设我们选择了以下五个指标：景点景色、旅游花费、居住环境、饮食情况、交通便利程度。

可以先建立下面的权重表格：

![](https://blog.caowei.xyz/blog/Math-2.png)

首先来确定五个指标的权重：

如果一次性考虑这五个指标，往往会出现考虑不周的情况。

所以往往采取每两个指标进行比较，进而推算出权重结果。

![](https://blog.caowei.xyz/blog/Math-3.png)

![](https://blog.caowei.xyz/blog/Math-4.png)

分析比较后，将上面的两两对比表填写完，如下图：

![](https://blog.caowei.xyz/blog/Math-5.png)

### 判断矩阵（正互反矩阵）

![](https://blog.caowei.xyz/blog/Math-6.png)

通过上面的表格得到了权重的判断矩阵，同理通过同样的方法可以得到景色、花费、居住、饮食、交通的判断矩阵。

![](https://blog.caowei.xyz/blog/Math-7.png)

![](https://blog.caowei.xyz/blog/Math-8.png)

### 一致矩阵

若正互反矩阵的各行、各列之间成倍数关系即为一致矩阵。

![](https://blog.caowei.xyz/blog/Math-11.png)

![](https://blog.caowei.xyz/blog/Math-9.png)

![](https://blog.caowei.xyz/blog/Math-10.png)

### 一致性检验

检验我们构造的判断矩阵和一致矩阵是否有太大的差别。

![](https://blog.caowei.xyz/blog/Math-12.png)

通过比较矩阵的**最大**特征值与n相差的大不大即可检验矩阵与一致矩阵相差的大不大。

### 一致性检验的步骤

![](https://blog.caowei.xyz/blog/Math-13.png)

CR>=0.1时的修正方法：

往一致矩阵上调整，一致矩阵的各行成倍数关系。

RI的求法：

![](https://blog.caowei.xyz/blog/Math-14.png)

### 一致矩阵计算权重

![](https://blog.caowei.xyz/blog/Math-15.png)

![](https://blog.caowei.xyz/blog/Math-16.png)

### 判断矩阵计算权重

![](https://blog.caowei.xyz/blog/Math-17.png)

#### **方法一：算术平均法**

![](https://blog.caowei.xyz/blog/Math-18.png)

使用数学符号描述：

![](https://blog.caowei.xyz/blog/Math-19.png)

#### 方法二：几何平均法

![](https://blog.caowei.xyz/blog/Math-20.png)

#### 方法三：特征值法（使用最多）

![](https://blog.caowei.xyz/blog/Math-21.png)

假如我们的判断矩阵一致性可以接受，那么我们可以仿照一致矩阵权重的求法。
第一步：求出矩阵A的最大特征值以及其对应的特征向量
第二步：对求出的特征向量进行归一化即可得到我们的权重

###  层次分析法的步骤

1. 分析系统中各因素之间的关系，建立系统的递阶层次结构

![](https://blog.caowei.xyz/blog/Math-34.png)

可使用亿图图示或[ProcessOn](https://www.processon.com/)等软件绘制。

2. 对于同一层次的各元素关于上一层次中某一准则的重要性进行两两比较，构造两两比较矩阵（判断矩阵）

![](https://blog.caowei.xyz/blog/Math-35.png)

![](https://blog.caowei.xyz/blog/Math-36.png)

3. 由判断矩阵计算被比较元素对于该准则的相对权重，并进行一致性检验（检验通过权重才能用）

4. 根据权重矩阵计算得分，并进行排序

   使用Excel计算比较方便。

### 层次分析法的局限性

1. 评价的决策层不能太多，太多的话n会很大（最大为15），判断矩阵和一致矩阵差异可能会很大。

2. 如果决策层中指标的数据是已知的，往往不适合使用层次分析法。