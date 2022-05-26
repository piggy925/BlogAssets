插值与拟合的区别：

插值算法中，得到的多项式f(x)要经过所有样本点。但是如果样本点太多，那么这个多项式次数过高，会造成龙格现象。

尽管我们可以选择分段的方法避免这种现象，但是更多时候我们更倾向于得到一个确定的曲线，尽管这条曲线**不能经过每一个样本点**，但只要保证误差足够小即可，这就是**拟合**的思想。

1. 示例代码

````matlab
clear;clc
load  data1
plot(x,y,'o')
% 给x和y轴加上标签
xlabel('x的值')
ylabel('y的值')
n = size(x,1);
k = (n*sum(x.*y)-sum(x)*sum(y))/(n*sum(x.*x)-sum(x)*sum(x))
b = (sum(x.*x)*sum(y)-sum(x)*sum(x.*y))/(n*sum(x.*x)-sum(x)*sum(x))
hold on % 继续在之前的图形上来画图形
grid on % 显示网格线

% % 画出y=kx+b的函数图像 plot(x,y)
% % 传统的画法：模拟生成x和y的序列，比如要画出[0,5]上的图形
% xx = 2.5: 0.1 :7  % 间隔设置的越小画出来的图形越准确
% yy = k * xx + b  % k和b都是已知值
% plot(xx,yy,'-')

% 匿名函数的基本用法。
% handle = @(arglist) anonymous_function
% 其中handle为调用匿名函数时使用的名字。
% arglist为匿名函数的输入参数，可以是一个，也可以是多个，用逗号分隔。
% anonymous_function为匿名函数的表达式。
% 举个小例子
%  z=@(x,y) x^2+y^2; 
%  z(1,2) 
% % ans =  5
% fplot函数可用于画出匿名一元函数的图形。
% fplot(f,xinterval) 将匿名函数f在指定区间xinterval绘图。xinterval =  [xmin xmax] 表示定义域的范围

f=@(x) k*x+b;
fplot(f,[2.5,7]);
legend('样本数据','拟合函数','location','SouthEast')
````

2. 拟合评价

````matlab
% 拟合优度：评价拟合的好坏 %
y_hat = k*x+b; % y的拟合值
SSR = sum((y_hat-mean(y)).^2)  % 回归平方和
SSE = sum((y_hat-y).^2) % 误差平方和
SST = sum((y-mean(y)).^2) % 总体平方和
SST-SSE-SSR   % 5.6843e-14  =   5.6843*10^-14   matlab浮点数计算的一个误差
R_2 = SSR / SST 
% R^2越接近1，说明误差平方和越接近0，误差越小说明拟合的越好 %
% R^2只能用于拟合函数是线性函数时候，拟合结果的评价 %
````

3. 使用matlab拟合工具箱

打开：APP -> Curve Fitting

![image-20210926152105774](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Math-69.png)

拟合方法说明：

+ **Custom Equations**：用户自定义的函数类型
+ Exponential：指数逼近，有2种类型， a*exp(b*x) 、 a*exp(b*x) + c*exp(d*x)
+ Fourier：傅立叶逼近，有7种类型，基础型是 a0 + a1*cos(x*w) + b1*sin(x*w)
+ Gaussian：高斯逼近，有8种类型，基础型是 a1*exp(-((x-b1)/c1)^2)*
+ Interpolant：插值逼近，有4种类型，linear、nearest neighbor、cubic spline、shape-preserving
+ **Polynomial**：多项式逼近，有9种类型，linear ~、quadratic ~、cubic ~、4-9th degree ~
+ Power：幂逼近，有2种类型，a*x^b 、a*x^b + c
+ Rational：有理数逼近，分子、分母共有的类型是linear ~、quadratic ~、cubic ~、4-5th degree ~；此外，分子还包括constant型
+ Smoothing Spline：平滑逼近（翻译的不大恰当，不好意思）
+ Sum of Sin Functions：正弦曲线逼近，有8种类型，基础型是 a1*sin(b1*x + c1)
+ Weibull：只有一种，a*b*x^(b-1)*exp(-a*x^b)

