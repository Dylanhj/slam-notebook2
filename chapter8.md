#8.1 ֱ�ӷ�������
- SVO LSD-SLAM DSO
#8.2 2D����
���㲿�������˶���Ϊ��ϡ�����
�������������˶���Ϊ�����ܹ���
LK����
- �ҶȲ������
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
�ٶ�ĳһ�����ڣ���СΪ$w^2$���ڵ����ؾ�����ͬ���˶�,����һ���������Է��̣�ʹ����С���˽⡣
#8.4 ֱ�ӷ�
##8.4.1 ֱ�ӷ����Ƶ�

