#12.1概述
#12.2 单目稠密重建
##12.2.1 立体视觉
##12.2.2 极限搜索与块匹配
如何计算小块与小块间的差异：
- SAD
- SSD
- NCC
##12.2.3 高斯分布的深度滤波器
设某个像素点的深度d服从:
$$p(d)=N(\mu , \sigma^{2})$$
每当新的数据到来，都会观测到他的深度，假设这次的观测也是一个高斯分布：
$$P(d_{obs})=N(\mu_{obs},\sigma^{2}_{obs})$$
设融合后的$d$的分布为$N(\mu_{fuse},\sigma_{fuse}^2)$，那么根据高斯分布的乘积，有:
$$\mu_{fuse}=\frac{\sigma_{obs}^2\mu+\sigma^2_{obs}}{\sigma^2+\sigma_{obs}^2},\qquad \sigma_{fuse}^2=\frac{\sigma^2\sigma_{obs}^2}{\sigma^2+\sigma_{obs}^2}$$
综合来说，可以给出估计稠密深度的一个完整的过程:
1.假设所有像素的深度满足某个初始的高斯分布；
2.当新数据产生时，通过极限搜索和块匹配确定投影点位置；
3.根据几何关系计算三角化后的深度及不确定性；
4.将当前观测融入上一次的估计中。若收敛停止计算，否则返回第2步。
