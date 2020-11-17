#9.1概述
##9.1.1 状态估计的概率解释
$$\begin{cases}
x_k = f(x_{k-1},u_k)+w_k \\
z_{k,j} = h(y_i,x_k)+v_{k,j}
\end{cases}$$
$$\begin{cases}
x_k = f(x_{k-1},u_k)+w_k \\
z_{k} = h(x_k)+v_{k}
\end{cases}$$
$$p(x_k|x_0,u_{1:k},z_{1:k})$$
$$p(x_k|x_0,u_{1:k},z_{1:k})\propto P(z_k|x_k)P(x_k|x_0,u_{1:k},z_{1:k-1})$$
第一项为似然，第二项为先验。
$$P(x_k|x_0,u_{1:k},z_{1:k-1})=\int P(x_k|x_{k-1},x_0,u_{1:k},z_{1:k-1})P(x_{k-1}|x_0,u_{1:k},z_{1:k-1})dx_{k-1}$$
- 假设马尔可夫性，k时刻状态只与k-1时刻有关，就会得到以EKF为代表的滤波器方法；
- 考虑k时刻与之前所有状态的关系，得到非线性优化为主体的优化框架。
##9.1.2 线性系统和KF
假设马尔可夫性，则k时刻只与k-1时刻有关：
$$P(x_k|x_{k-1},x_0,u_{1:k},z_{1:k-1})=P(x_k|x_{k-1},u_k)$$
$$P(x_{k-1}|x_0,u_{1:k},z_{1:k-1})=P(x_{k-1}|x_0,u_{1:k-1},z_{1:k-1})$$
从线性高斯系统开始，运动方程和观测方程由线性方程来描述：
$$\begin{cases}
x_k = A_kx_{k-1}+u_k+w_k \\
z_k = C_kx_k+v_k
\end{cases}$$
 假设所有状态和噪声均满足高斯分布，记噪声服从零均值高斯分布：
 $$w_k \sim N(0,R)  \qquad v_k\sim N(0,Q)$$
 以上帽子$\hat{x}_k$表示后验，下帽子$\check{x}_k$表示先验分布。
 第一步，通过运动方程确定$x_k$的先验分布，此步骤为线性，因此仍然满足高斯分布：
 $$P(x_k|x_0,u_{1:k},z_{1:k-1})=N(A_k\hat{x}_{k-1}+u_k,A_k\hat{P}_{k-1}A_k^T+R)$$
 这一步被称为预测，它显示了如何从上一个时刻的状态，根据输入信息推断当前时刻的状态分布，这个分布也就是先验
 $$\check{x}_k=A_k\hat{x}_{k-1}+u_k, \qquad \check{P}_k=A_k\hat{P}_{k-1}A_k^T+R$$
 因为添加了噪声，所以状态的不确定会增大，由观测方程，可以计算某个状态下应该产生怎样的观测数据。
 $$P(z_k|x_k)=N(C_kx_k,Q)$$
 为了得到后验概率，想要计算他们的乘积。但目前只知道最后会得到一个$x_k$的高斯分布，直接计算会有麻烦，设结果满足$x_k \sim N(\hat{x}_k,\check{P}_k)$,则：
 $$N(\hat{x}_k,\check{P}_k)=\eta N(C_kx_k,Q)·N(\check{x}_k,\check{P}_k)$$
 若允许相差与$x_k$无关的常数
 $$(x_k-\hat{x_k})^T \hat{P}^{-1}_k(x_k - \hat{x}_k)=(z_k-C_kx_k)^T Q^{-1}(z_k - C_kx_k)+(x_k-\check{x_k})^T \check{P}^{-1}_k(x_k - \check{x}_k)$$
 对于$x_k$的二次系数：
 $$\hat{P}_k^{-1}=C_k^TQ^{-1}C_k+\check{P}_k^{-1}$$
 定义$K=\hat{P}_kC_k^TQ^{-1}$
 $$I=\hat{P}_kC_k^TQ^{-1}C_k+\hat{P}_k\check{P}_k^{-1}=KC_k+\hat{P}_k\check{P}_k^{-1}$$
 $$\hat{P}_k = (I-KC_k)\check{P}_k$$
 同样的方式比较一次项的系数，得到：
 $$\hat{x}_k=\check{x}_k + K(z_k - C_k\check{x}_k)$$
 于是上面的步骤可以归纳为"预测"和"更新"两个步骤
 1.预测：
 $$P(x_k|x_0,u_{1:k},z_{1:k-1})=N(A_k\hat{x}_{k-1}+u_k,A_k\hat{P}_{k-1}A_k^T+R)$$
 2.更新，先计算$K$,他又称为卡尔曼增益
 $$K=\hat{P}_kC_k^T(C_k\check{P}_kC_k^T+Q_k)^{-1}$$
 然后计算后验概率的分布：
 $$\hat{x}_k=\check{x}_k + K(z_k - C_k\check{x}_k)$$
 $$\hat{P}_k = (I-KC_k)\check{P}_k$$

##9.1.3 非线性系统和EKF
令$k-1$时刻的均值和协方差矩阵为$\hat{x}_{x-1},\hat{P}_{k-1}$。在$k$时刻，我们讲运动方程和观测方程在$\hat{x}_{k-1},\hat{P}_{k-1}$处进行线性化，得到:
$$x_k \approx f(\hat{x}_{k-1})+\frac{\partial f}{\partial x_{k-1}}|_{\hat{x}_{k-1}}(x_{k-1}-\hat{x}_{k-1})+w_k$$
记这里的偏导数为：
$$F=\frac{\partial f}{\partial x_{k-1}}|_{\hat{x}_{k-1}}$$
同样，对于观测矩阵，有：
$$z_k \approx h(\check{x}_k)+\frac{\partial h}{\partial x_k}|\check {x}_k$$
那么，在预测步骤中，根据运动方程：
$$P(x_k|x_0,u_{1:k},z_{0,k-1})=N(f(\hat{x}_{k-1},u_k),F\hat{P}_{k-1}F^T+R_k)$$
记这里的先验和协方差的均值为：
$$\check {x}_k = f(\hat{x}_{k-1},u_k), \qquad \check{P}_k = F\hat{P}_{k-1}F^T+R_k$$
然后，考虑在观测中有：
$$P(z_k|x_k)=N(h(\check{x}_{k})+H(x_k-\check{x}_k),Q_k)$$
首先定义一个卡尔曼增益$K_k$
$$K_k=\check{P}_kH^T(H\check{P}_kH^T+Q_k)^{-1}$$
$$\hat{x}_k = \check{x}_k + K_k(z_k-h(\check{x}_k)), \qquad \hat{P}_k = (I-K_kH)\check{P}_k$$

#9.2 BA与图优化
##9.2.1 投影模型和BA代价函数
1.把世界坐标系转换到相机坐标系
$$P^{\prime}=[X^{\prime},Y^{\prime},Z^{\prime}]^T$$
2.将$P^{\prime}$投至归一化平面，得到归一化坐标：
$$P_c = [u_c,v_c,1]^T=[X^{\prime}/Z^{\prime},Y^{\prime}/Z^{\prime},1]^T$$
3.考虑归一化坐标的畸变情况，得到去畸变之前的原始像素坐标，首先只考虑径向畸变：
$$\begin{cases}
u_c^{\prime}=u_c(1+k_1r_c^2+k_2r_c^4) \\
v_c^{\prime}=v_c(1+k_1r_c^2+k_2r_c^4)
\end{cases}$$
4.根据内参模型，计算像素坐标:
$$\begin{cases}
u_s=f_xu_c^{\prime}+c_x \\
v_s=f_yv_c^{\prime}+c_y
\end{cases}$$
以上的计算得出了**观测方程**,即$z=h(x,y)$
$x$指的是此时相机的位姿，即外参$R,t$，对应的李群为$T$,李代数为$\xi$,路标$y$即指的是这里的三维点$p$,而观测数据则是像素坐标$z=[u_s,v_s]^T$。以最小二乘的角度来考虑，那么写出此次观测的误差为:
$$e=z-h(T,p)$$
则整体的代价函数为：
$$\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^n||e_{ij}||^2=\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^n||z_{ij}-h(T_i,p_j)||^2$$
对这个最小二乘进行求解，相当于对位姿和路标同时做了调整，也就是BA。
##9.2.2 BA的求解
根据非线性优化的思想，应该从某个初始值开始，不断寻找下降防线$\Delta x$，来找到目标函数的最优解，在整体BA目标函数上，应该把自变量定义成所有待优化的量：
$$x=[T_1,\dots,T_m,p_1,\dots,p_n]^T$$
则增量方程中的$\Delta x$便是对整体自变量的增量，当我们给自变量一个增量时，目标函数变为：
$$\frac{1}{2}||f(x+\Delta x)||^2 \approx \frac{1}{2}\sum_{i=1}^m \sum_{j=1}^n||e_{ij}+F_{ij}\Delta \xi_i+E_{ij}\Delta p_j||^2$$
其中，$F_{ij}$表示整个代价函数在当前状态下对相机姿态的偏导数，而$E_{ij}$表示该函数对路标点位置的偏导数。
现在将相机位姿变量放在一起为$x_c$，空间点变量放在一起为$x_p$,则式子可简化为:
$$\frac{1}{2}||f(x+\Delta x)||^2=\frac{1}{2}||e+F\Delta x_c + E\Delta x_p||^2$$
##9.2.3 稀疏性和边缘化
$H$矩阵的稀疏性是由雅可比矩阵$J(x)$引起的，考虑这些代价函数中的一个$e_{ij}$，因为只涉及第$i$个相机位姿和第$j$个路标点，对其语部分变量的导数均为0。
$$J_{ij}=(0_{2\times6},\dots,0_{2\times6},\dots,\frac{\partial e_{ij}}{\partial T_i},0_{2\times6},\dots,0_{1\times3},\frac{\partial e_{ij}}{\partial p_j},0_{2\times3},\dots,0_{2\times3})$$
由于稀疏性，最终$H$矩阵变为箭头型矩阵，对应的线性方程组可以由$H\Delta x =g$变成如下形式:
$$\left[
    \begin{matrix}
    B   &   E \\
    E^T &   C
    \end{matrix}
    \right]
    \left[
        \begin{matrix}
        \Delta x_c \\
        \Delta x_p
        \end{matrix}
        \right]=
        \left[
            \begin{matrix}
            v \\
            w
            \end{matrix}
            \right]$$
因对角块矩阵求逆的难度远小于一般矩阵，因此要对线性方程组进行高斯消元，以便于消去右上角的非对角部分:
$$\left[
    \begin{matrix}
    B-EC^{-1}E^T   &   0 \\
    E^T &   C
    \end{matrix}
    \right]
    \left[
        \begin{matrix}
        \Delta x_c \\
        \Delta x_p
        \end{matrix}
        \right]=
        \left[
            \begin{matrix}
            v-EC^{-1}w \\
            w
            \end{matrix}
            \right]$$
则关于位姿部分的增量方程为:
$$[B-EC^{-1}E^T]\Delta x_c = v-EC^{-1}w$$
做法是先求解整个方程，之后把解得的$\Delta x_c$带入原方程，以求解$\Delta x_p$，这个过程称为Schur消元。
