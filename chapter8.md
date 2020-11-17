#8.1 直接法的引出
- SVO LSD-SLAM DSO
#8.2 2D光流
计算部分像素运动称为：稀疏光流
计算所有像素运动称为：稠密光流
LK光流
- 灰度不变假设
$$I(x+dx,y+dy,t+dt)=I(x,y,t)$$
$$I(x+dx,y+dy,t+dt)\approx I(x,y,t)+\frac{\partial I}{\partial x}dx+\frac{\partial I}{\partial y}dy+\frac{\partial I}{\partial t}dt$$
$$\frac{\partial I}{\partial x}dx+\frac{\partial I}{\partial y}dy+\frac{\partial I}{\partial t}dt=0$$
$$\frac{\partial I}{\partial x}\frac{dx}{dt}+\frac{\partial I}{\partial y}\frac{dy}{dt}=-\frac{\partial I}{\partial t}$$
$$\left[
    \begin{matrix}
    I_x & I_y
    \end{matrix}
    \right]
    \left[
        \begin{matrix}
        u \\
        v
        \end{matrix}
        \right]=-I_t$$
假定某一个窗口（大小为$w^2$）内的像素具有相同的运动,构造一个超定线性方程，使用最小二乘解。
#8.4 直接法
##8.4.1 直接法的推导

