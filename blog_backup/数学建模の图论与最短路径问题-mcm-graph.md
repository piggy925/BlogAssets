### 作图

**在线做图工具**：https://csacademy.com/app/graph_editor/

**Matlab作无向图：**

1. 无权重

````matlab
% 无权重（每条边的权重默认为1）
% 函数graph(s,t)：可在 s 和 t 中的对应节点之间创建边，并生成一个图
% s 和 t 都必须具有相同的元素数；这些节点必须都是从1开始的正整数，或都是字符串元胞数组。
s1 = [1,2,3,4];
t1 = [2,3,1,1];
G1 = graph(s1, t1);
plot(G1)
% 注意哦，编号最好是从1开始连续编号，不要自己随便定义编号
s1 = [1,2,3,4];
t1 = [2,3,1,1];
G1 = graph(s1, t1);
plot(G1)

% 注意字符串元胞数组是用大括号包起来的哦
s2 = {'学校','电影院','网吧','酒店'};
t2 = {'电影院','酒店','酒店','KTV'};
G2 = graph(s2, t2);
plot(G2, 'linewidth', 2)  % 设置线的宽度
% 下面的命令是在画图后不显示坐标
set( gca, 'XTick', [], 'YTick', [] ); 
````

2. 有权重

````matlab
% （2）有权重
% 函数graph(s,t,w)：可在 s 和 t 中的对应节点之间以w的权重创建边，并生成一个图
s = [1,2,3,4];
t = [2,3,1,1];
w = [3,8,9,2];
G = graph(s, t, w);
plot(G, 'EdgeLabel', G.Edges.Weight, 'linewidth', 2) 
set( gca, 'XTick', [], 'YTick', [] );  
````

**matlab作有向图：**

1. 无权重

````matlab
% 无权图 digraph(s,t)
s = [1,2,3,4,1];
t = [2,3,1,1,4];
G = digraph(s, t);
plot(G)
set( gca, 'XTick', [], 'YTick', [] );  
````

2. 有权重

```matlab
% 有权图 digraph(s,t,w)
s = [1,2,3,4];
t = [2,3,1,1];
w = [3,8,9,2];
G = digraph(s, t, w);
plot(G, 'EdgeLabel', G.Edges.Weight, 'linewidth', 2) 
set( gca, 'XTick', [], 'YTick', [] ); 
```

### 计算

#### 计算最短路径

```matlab
% 注意哦，Matlab中的图节点要从1开始编号，所以这里把0全部改为了9
% 编号最好是从1开始连续编号，不要自己随便定义编号
s = [9 9 1 1 2 2 2 7 7 6 6  5  5 4];
t = [1 7 7 2 8 3 5 8 6 8 5  3  4 3];
w = [4 8 3 8 2 7 4 1 6 6 2 14 10 9];
G = graph(s,t,w);
plot(G, 'EdgeLabel', G.Edges.Weight, 'linewidth', 2) 
set( gca, 'XTick', [], 'YTick', [] );  
% shortestpath参数：
% G：输入图（graph对象 ｜ digraph对象）
% 9：start 起始节点
% 4：end 目标节点
[P,d] = shortestpath(G, 9, 4)
% 输出参数：
% P：最短路径经过的节点
% d：最短路径
```

#### 高亮最短路径

```matlab
%首先将图赋给一个变量
myplot = plot(G, 'EdgeLabel', G.Edges.Weight, 'linewidth', 2); 
%对这个变量即我们刚刚绘制的图形进行高亮处理（给边加上r红色）
highlight(myplot, P, 'EdgeColor', 'r')   
```

#### 求任意两点之间的最短距离

```matlab
D = distances(G)
D(1,2)  % 1 -> 2的最短路径
D(9,4)  % 9 -> 4的最短路径
```

#### 找给定范围内所有的点

```matlab
% nearest(G,s,d)
% 返回图形 G 中与节点 s 的距离在 d 之内的所有节点
[nodeIDs,dist] = nearest(G, 2, 10)
```