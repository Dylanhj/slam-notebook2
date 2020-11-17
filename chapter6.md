#6.1状态估计问题
##6.1.1批量状态估计与最大后验估计
$$\begin{cases}
x_k &= f(x_{k-1},u_k) \\
z_{k,j} &= h(y_i,x_k)+v_{k,j}
\end{cases}$$
$$sz_{k,j}=K(R_ky_j+t_k)$$
$$w_k\sim N(0,R_k) , v_k \sim N(0,Q_{k,j})$$
定义所有时刻的机器人位姿和路标点坐标为：
$$x=\{x_1,\dots,x_N\}, y=\{y_1,\dots,y_N\}$$
在已知输入数据$u$和观测数据$z$的条件下，求状态$x,y$的条件概率分布:$P(x,y|z,u)$
$$P(x,y|z,u)=\frac{P(z,u|x,y)P(x,y)}{P(z,u)}\propto P(z,u|x,y)P(x,y)$$
左侧为后验概率，右侧$P(z|x)$部分称为似然，另一部分称为先验，直接求解后验概率是困难的，但是求一个状态最优估计，使得该状态下后验概率最大化则是可行的。
$$(x,y)^*_{MAP}=argmaxP(x,y|z,u)=argmaxP(z,u|x,y)P(x,y)$$
求解最大后验概率等价于最大化似然和先验的乘积
若没有先验，可以求解最大似然估计：
$$(x,y)^*_{MLE}=arg maxP(z,u|x,y)$$
可以理解为：***在什么样的状态下，最可能产生现在观测到的数据***
##6.1.2最小二乘的引出
$$z_{k,j}=h(y_j.x_k)+v_{k,j}$$
$$P(z_{j,k}|x_k,y_j)=N(h(y_j,x_k),Q_{k,j})$$
使用最小化负对数来求一个高斯分布的最大似然：
$$\begin{aligned}(x_k.y_j)^*&=argmax N(h(y_j,x_k),Q_{k,j})\\
&=argmin((z_{k,j}-h(x_k,y_j))^TQ_{k,j}^{-1}(z_{k,j}-h(x_k,y_j)))
\end{aligned}$$
$$P(z,u|x,y)=\prod _kP(u_k|x_{k-1},x_k)\prod _{k,j}P(z_{k,j}|x_k,y_j)$$
$$e_{u,k}=x_k-f(x_{k-1},u_k)$$
$$e_{z,j,k}=z_{k,j}-h(x_k,y_j)$$
$$minJ(x,y) = \sum _k e_{n,k}^TR_k^{-1}e_{u,k}+\sum _k \sum _je_{z,k,j}^{T}Q_{k,j}^{-1}e_{z,k,j}$$
##6.1.3批量状态估计
$$\begin{aligned}
x_k &=x_{k-1}+u_k+w_k, &w_k \sim N(0,Q_k) \\
z_k &=x_k + n_k, &n_k \sim N(0,R_k)
\end{aligned}$$
令批量状态变量为$x=[x_0,x_1,x_2,x_3]^T$,令批量观测为$z=[z_1,z_2,z_3]^T$,$u=[u_1,u_2,u_3]^T$最大似然估计为：
$$x_{map}^*=argmaxP(x|u,z)=argmaxP(u,z|x)=\prod _{k=1}^3P(u_k|x_{k-1},x_k)\prod_{k=1}^3P(z_k|x_k)$$
$$P(u_k|x_{k-1},x_k)=N(x_k,R_k)$$
$$P(z_k|x_k)=N(x_k,R_k)$$
定义向量$y=[u,z]^T$,则有矩阵$H$，使得：
$$y-Hx=e \sim N(0,\Sigma)$$
则$H$为：
$$\left[
\begin{matrix}
1 & -1 & 0 & 0 \\
0 & 1  & -1& 0 \\
0 & 0  & 1 &-1 \\
0 & 1  & 0 & 0 \\
0 & 1  & 1 & 0 \\
0 & 0  & 0 & 1 
\end{matrix}    \right]$$
$\Sigma=diag(Q_1,Q_1,Q_3,R_1,R_2,R_3)$。问题简化为：
$$x^*_{map}=argmine^T\Sigma^{-1}e$$
$$x^*_{map}=(H^T\Sigma^{-1}H)^{-1}H^T\Sigma^{-1}y$$

#6.2非线性最小二乘
##6.2.1一阶和二阶梯度法
$$J+H\Delta x=0 \Rightarrow H\Delta x = -J$$
求解这个线性方程，就得到了增量，该方法称为牛顿法。
##6.2.2高斯牛顿法
$$J(x)J^T(x)\Delta x = -J(x)f(x)$$
$$H\Delta x = g$$
高斯牛顿法用$JJ^T$作为牛顿法中二阶Hessian矩阵的近似，求解增量方程式整个优化问题的核心所在。
1.给定初始值$x_0$;
2.对于第$k$次迭代，求出当前的雅可比矩阵$J(x_k)$和误差$f(x_k)$;
3.求解增量方程：$H\Delta x_k=g$;
4.若$\Delta x_k$足够小，则停止。否则，令$x_{k+1}=x_k+\Delta x_k$,返回第二步。
##6.2.3列文伯格-马夸尔特方法
1.给定初始值$x_0$，以及初始优化半径$\mu$;
2.对于第$k$次迭代，在高斯牛顿法上加上信赖区域，求解:
$$min_{\Delta x_k}\frac{1}{2}||f(x_k)+J(x_k)^T\Delta x_k||^2 , s.t. ||D\Delta x_k||^2 \leq \mu$$
其中，$\mu$是信赖区域的半径，$D$为系数矩阵；
3.$\rho=\frac{f(x+\Delta x)-f(x)}{J(x)^T\Delta x}$
4.若$\rho > \frac{3}{4}$，则设置$\mu=2\mu$;
5.若$\rho < \frac{1}{4}$，则设置$\mu=0.5\mu$;
6.如果$\rho$大于某阈值，则认为近似可行，令$x_{k+1}=x_k+\Delta x_k$;
7.判断算法是否收敛，如不收敛返回第二步，否则结束。

视觉SLAM中，常常使用ICP和Pnp提供优化初始值
求解线性增量方程组：使用矩阵分解的方式，如QR、Cholesky