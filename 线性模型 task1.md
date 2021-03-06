## 线性模型

1. ### 基本形式：

给定由$d$个属性描述的示例$x =(x_1; x_2;...;x_i)$,其中$x_i$

 是$x$在第$ i$个的属性上的取值，一般式为：
$$
f(x)= w_1x_1 +w_2x_2+...+w_ix_i\tag{1}
$$
即：
$$
f(x)=w^Tx+b\tag{2}
$$

2. ### 线性回归：

给定数据集$ D={(x_1, y_1), (x_2,y_2 ), …,(x_i, y_i)}$，其中$x_i=(x_{i1}; x_{i2};…;x_{id}), y\in R$。"线性回归"试图学的一个线性模型以尽可能准确的预测输出标记。线性回归试图学得：
$$
f(x_i) = wx_i +b,使得f(x_i)\simeq y_i\tag{3}
$$
我们使用均方误差衡量$f( x_i)$与$y$之间的关系， 以求得$w$和$b$, 均方误差最小化， 即
$$
（w^*, b^*） = argmin\sum_{i=1}^m(f(x_i)-y_i)^2 \\
=argmin\sum_{i= 1}^{m}(y_i-wx_i-b)^2\tag{4}
$$
基于均方误差最小化来进行模型求解的方法称为“最小二乘”， 最小二乘试图找到一条直线，使所有的样本到直线上的欧式距离之和最小。

求解$w $和$b$ 使$E_{(w,b)}=\sum_{i=1}^m(y-wx_i-b)^2$最小化的过程，成为线性回归模型的最小二乘“参数估计”， 将$E_{w,b}$分别对$w$和$b$求导：


$$
\frac{\partial E_{w, b}}{\partial w}=2(w\sum_{i=1}^mx^3_i -\sum_{i=1}^m(y_i-b)x_i),\tag{5}
$$

$$
\frac{\partial E_{(w, b)}}{\partial{b}}=2(mb-\sum_{i=1}^m(y_i-wx_i))\tag{6}
$$

​		令式（5）、（6）为0， 可得$w$和$b$最优的闭解：
$$
w=\frac{\sum_{i=1}^m(y_i(x_i- \bar{x})}{\sum_{i=1}^m x_i^2 -\frac{1}{m}(\sum_{i=1}^m x_i)^2} \tag{7}
$$

$$
b=\frac{1}{m}\sum_{i=1}^i(y_i-wx_i)\tag{8}
$$

​		其中$\bar{x} =\frac{1}{m}\sum_{i=1}^m x_i$为$x$的均值。 

​		同时数据集$D$ ,样本由多个$ d$个属性描述， 此时$f(x_i)= w^Tx+b, f(x_i)\simeq y_i$		为“多元线性回归”

​		将（4）式写成矩阵的形式，即：
$$
\hat{w^*}= argmin(y-X\hat{w})^T(y-X\hat{w}) \tag{9}
$$
​		对$ \hat{w}$求导得：
$$
\frac{\partial E_{\hat{w}}}{\partial \hat{w}}= 2X^T(X\hat{w}-y)\tag{10}
$$
​		当$X^ TX$为满秩矩阵或者正定矩阵时， （10）式可得闭解， 即：
$$
\hat{w}^*= (X^TX)^{-1}X^Ty
$$
​		当$X^TX$不是满秩矩阵时， 需要引入正则化项。

3. ### 对数几率回归（逻辑回归）

   对于二元分类问题， 其输出得标记$y \in   \{0, 1\}$,而线性回归模型产生得预测值$z=w^Tx +b$是实值， 最理想得是“单位阶跃函数”，由于其不是单调可微的。但是对数几率函数常用的替代函数, 它将$z$值转化成一个接近0或1的$y$值， 并且其输出值再$z=0$附近变化很陡。
   $$
   y=\frac{1}{1+e^{-z}}\tag{11}
   $$
   即：
   $$
   y=\frac{1}{1+e^{-(w^Tx+b)}}\tag{12}
   $$
   

对（12）式取对数，
$$
ln\frac{y}{1-y} = w^Tx+b\tag{13}
$$
若将$y$视为样本$x$作为正例的可能性， 则$1-y$是其反例的可能性， 两者的比值
$$
\frac{y}{1-y}\tag{14}
$$
称为"几率"， 反应了$x$作为正例的可能性， 对几率取对数则可以得到“对数几率”
$$
ln\frac{y}{1-y}\tag{15}
$$
“对数几率回归”实际是一种分类学习方法， 可以直接对分类可能性进行建模， 无需假设数据分布， 他不仅预测出“类别”， 而且还可得到近似概率预测。

4. ### 线性判别分析

   线性判别分析（Linear Discriminant Analysis 简称LDA）是一种经典的线性学习方法，最早称"Fisher 判别分析"。

   LDA的思想很朴素： 给定训练样例集， 设法将样例投影到一条直线上， 使得同类样例的投影点尽可能接近， 异类样例的投影点尽可能远离；在对新样本进行分类时，将其投影在这条直线上， 再根据投影点的位置来确定新的样本类别。

   数据集： $D=\{(x_i, y_i)\}^m_{i=1}$,$y_i=\{0, 1\}$, 令 $X_i, \mu_i, \Sigma_i$分别表示第$i\in \{0, 1\}$类实例的集合，均值向量， 协方差矩阵。

   样本在直线上的投影为 $w^T\mu_0,w^T\mu_1$, 协方差为：$w^T\Sigma_0w, w^T\Sigma_1w$

   ------

   欲使同类的投影点尽可能接近， 可以让同类的投影点的协方差尽可能小 （$w^T\Sigma_0 w+w^T\Sigma_1 w$）, 而欲使异类样例的投影点尽可能远离， 可以让类中心的距离尽可能大（$||w^T\mu_0 -w^T\mu_1||^2_2$）尽可能大， 同时考虑两者， 则可得到最大化目标：
   $$
   J=\frac{||w^T\mu_0 -w^T\mu_1||^2_2}{w^T\Sigma_0 w+w^T\Sigma_1 w}\\
   =\frac{w^T(\mu_0-\mu_1)(\mu_0-\mu_1)w}{w^T(\Sigma_0+\Sigma_1)w}\tag{16}
   $$
   定义“类内散度矩阵”
   $$
   S_w=\Sigma_0+\Sigma_1\\
   =\sum_{x\in X_0}(x-\mu_0)(x-\mu_0)^T+\sum_{x\in X_1}(x-\mu_1)(x-\mu_1)^T\tag{17}
   $$
   

以及“内间散度矩阵”
$$
S_b =(\mu_0-\mu_1)(\mu_0-\mu_1)^T \tag{18}
$$
则
$$
J=\frac{w^TS_bw}{w^TS_ww}\tag{19}
$$
这就是LDA欲最大化的目标， 即$S_b$,$S_w$的“广义瑞利商”， 分子和分母都是关于$w$的二次项， 因此式（19）的解和$w$的长度无关， 只与其方向有关，不失一般性， 令$w^TS_ww =1$

即： 
$$
min_{w} -w^TS_bw\\
s.t. w^TS_ww =1\tag{20}
$$
由拉格朗日乘子,$S_bw=\lambda S_ww$， 其中$\lambda$是拉格朗日乘子 ,注意到$S_bw$的方向恒为$\mu_0-\mu_1$, 不妨令：
$$
S_bw=\lambda (\mu_0-\mu_1)
$$
即得：
$$
w=S_w^{-1}(\mu_0-\mu_1)
$$
使用奇异值分解$S_w$, 即$S_w=U\Sigma V^T$, 再由
$$
S_w^{-1}=V\Sigma^{-1}U^T
$$
可以将LDA推广到多分类任务中， 假定存在$N$个类， 且第$i$类示例数为$m_i$,我们先定义“全局散度矩阵”
$$
S_t = S_b+S_w\\
=\sum_{i=1}^m(x_i-\mu)(x_i-\mu)^T
$$
其中$\mu$是所有样例的均值， 将类内散度矩阵$Sw$重定义为每个类别的散度矩阵之和，即
$$
S_w=\sum^n_{i=1}S_{w_i}\\
S_{w_i}=\sum_{x\in X_i}(x-\mu_i)(x-\mu_i)^T
$$
可得：
$$
S_b=S_t-S_w
$$
可以使用多种实现方法使用$S_b, S_w, S_t$三者中的任何两种即可。常见的一种实现是采用优化目标
$$
max\frac{tr(W^TS_bW)}{tr(W^TS_wW)}\tag{21}
$$
可通过广义特征值问题求解：
$$
S_bW=\lambda S_wW
$$
$W$的闭解形式是$S^{-1}_wS_b$的$N-1$个最大广义特征值所对应的特征向量组成的矩阵。

5. ### 多分类学习

   不失一般性， 考虑$N$个类别$C_1, C_2, ...., C_N$多分类学习的基本思路是“拆解法”， 最经典的拆分策略有三种：“一对一”（One vs. One 简称OvO）、“一对其余”（One vs. Rest 简称 OvR）和“多对多”（Many vs. Many 简称MvM）.

   OvO将这$N$个类别两两配对， 从而产生$N(N-1)/2$个二元分类任务。

   OvR 则是每次将一个类的样例作为正例、所有其他类的样例作为反例来训练N个分类器。

   MvM是每次将若干个类作为正类， 若干个其他类作为反类。MVM技术常用的叫“纠错输出码”，由于纠错编码实用性不强，所以在这里不过多介绍。

   

   接下来我会找一些编程题来实现对线性回归算法的复盘。

   