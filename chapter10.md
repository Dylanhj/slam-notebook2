#10.1 滑动窗口滤波和优化
##10.1.1 实际环境下的BA结构
实际使用中需要用手段控制BA的规模
##10.1.2 滑动窗口法
考虑一个滑动窗口，假设窗口内有N个关键帧，它们的位姿表达为:
$$x_1,\dots,x_N$$
$$[x_1,\dots,x_N]^T\sim N([\mu_1,\dots,\mu_N]^T,\Sigma)$$
#10.2位姿图
##10.2.1 位姿图的意义
省去大量的特征点优化计算，只保留关键帧的轨迹，从而构建出了位姿图
##10.2.2 位姿图的优化
位姿图中，以节点表示相机位姿，用$T_1,\dots,T_n$来表达，而边则是两个位姿之间相对运动的估计，估计来自于特征点法或者直接法，也可以来自GPS或IMU积分。
$$\Delta \xi _{ij}=\ln(T^{-1}_iT_j)^{\vee}$$
按照李群的写法:
$$T_{ij}=T_i^{-1}T_j$$
因为误差的存在，所以等式并不能完全成立，构建误差$e_{ij}$：
$$e_{ij}=\Delta\xi_{ij}\ln(T_{ij}^{-1}t_i^{-1}T_j)^{\vee}$$
优化变量为$\xi_i$和$\xi_j$，因此要求$e_{ij}$关于这两个变量的导数。按照李代数的方式，给$\xi_i$和$\xi_j$各一个左扰动:$\delta\xi_i$和$\delta\xi_j$。于是误差变为:
$$\hat{e}_{ij}=\ln(T^{-1}_{ij}T^{-1}_iexp((-\delta\xi_i)^{\wedge})exp(\delta\xi_j^{\wedge})T_j)^{\vee}$$
通过引入一个伴随阵，能够交换扰动项左右侧的$T$，利用这样的性质，可以将扰动挪到最右，导出右乘形式的雅可比矩阵:
$$\hat{e}_{ij}\approx e_{ij}+\frac{\partial e_{ij}}{\partial \delta \xi_i}\delta \xi_i + \frac{\partial e_{ij}}{\partial \delta \xi_j}\delta \xi_j$$
因此求出了误差关于两个位姿的雅各比矩阵