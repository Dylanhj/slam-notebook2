#9.1����
##9.1.1 ״̬���Ƶĸ��ʽ���
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
��һ��Ϊ��Ȼ���ڶ���Ϊ���顣
$$P(x_k|x_0,u_{1:k},z_{1:k-1})=\int P(x_k|x_{k-1},x_0,u_{1:k},z_{1:k-1})P(x_{k-1}|x_0,u_{1:k},z_{1:k-1})dx_{k-1}$$
- ��������ɷ��ԣ�kʱ��״ֻ̬��k-1ʱ���йأ��ͻ�õ���EKFΪ������˲���������
- ����kʱ����֮ǰ����״̬�Ĺ�ϵ���õ��������Ż�Ϊ������Ż���ܡ�
##9.1.2 ����ϵͳ��KF
��������ɷ��ԣ���kʱ��ֻ��k-1ʱ���йأ�
$$P(x_k|x_{k-1},x_0,u_{1:k},z_{1:k-1})=P(x_k|x_{k-1},u_k)$$
$$P(x_{k-1}|x_0,u_{1:k},z_{1:k-1})=P(x_{k-1}|x_0,u_{1:k-1},z_{1:k-1})$$
�����Ը�˹ϵͳ��ʼ���˶����̺͹۲ⷽ�������Է�����������
$$\begin{cases}
x_k = A_kx_{k-1}+u_k+w_k \\
z_k = C_kx_k+v_k
\end{cases}$$
 ��������״̬�������������˹�ֲ����������������ֵ��˹�ֲ���
 $$w_k \sim N(0,R)  \qquad v_k\sim N(0,Q)$$
 ����ñ��$\hat{x}_k$��ʾ���飬��ñ��$\check{x}_k$��ʾ����ֲ���
 ��һ����ͨ���˶�����ȷ��$x_k$������ֲ����˲���Ϊ���ԣ������Ȼ�����˹�ֲ���
 $$P(x_k|x_0,u_{1:k},z_{1:k-1})=N(A_k\hat{x}_{k-1}+u_k,A_k\hat{P}_{k-1}A_k^T+R)$$
 ��һ������ΪԤ�⣬����ʾ����δ���һ��ʱ�̵�״̬������������Ϣ�ƶϵ�ǰʱ�̵�״̬�ֲ�������ֲ�Ҳ��������
 $$\check{x}_k=A_k\hat{x}_{k-1}+u_k, \qquad \check{P}_k=A_k\hat{P}_{k-1}A_k^T+R$$
 ��Ϊ���������������״̬�Ĳ�ȷ���������ɹ۲ⷽ�̣����Լ���ĳ��״̬��Ӧ�ò��������Ĺ۲����ݡ�
 $$P(z_k|x_k)=N(C_kx_k,Q)$$
 Ϊ�˵õ�������ʣ���Ҫ�������ǵĳ˻�����Ŀǰֻ֪������õ�һ��$x_k$�ĸ�˹�ֲ���ֱ�Ӽ�������鷳����������$x_k \sim N(\hat{x}_k,\check{P}_k)$,��
 $$N(\hat{x}_k,\check{P}_k)=\eta N(C_kx_k,Q)��N(\check{x}_k,\check{P}_k)$$
 �����������$x_k$�޹صĳ���
 $$(x_k-\hat{x_k})^T \hat{P}^{-1}_k(x_k - \hat{x}_k)=(z_k-C_kx_k)^T Q^{-1}(z_k - C_kx_k)+(x_k-\check{x_k})^T \check{P}^{-1}_k(x_k - \check{x}_k)$$
 ����$x_k$�Ķ���ϵ����
 $$\hat{P}_k^{-1}=C_k^TQ^{-1}C_k+\check{P}_k^{-1}$$
 ����$K=\hat{P}_kC_k^TQ^{-1}$
 $$I=\hat{P}_kC_k^TQ^{-1}C_k+\hat{P}_k\check{P}_k^{-1}=KC_k+\hat{P}_k\check{P}_k^{-1}$$
 $$\hat{P}_k = (I-KC_k)\check{P}_k$$
 ͬ���ķ�ʽ�Ƚ�һ�����ϵ�����õ���
 $$\hat{x}_k=\check{x}_k + K(z_k - C_k\check{x}_k)$$
 ��������Ĳ�����Թ���Ϊ"Ԥ��"��"����"��������
 1.Ԥ�⣺
 $$P(x_k|x_0,u_{1:k},z_{1:k-1})=N(A_k\hat{x}_{k-1}+u_k,A_k\hat{P}_{k-1}A_k^T+R)$$
 2.���£��ȼ���$K$,���ֳ�Ϊ����������
 $$K=\hat{P}_kC_k^T(C_k\check{P}_kC_k^T+Q_k)^{-1}$$
 Ȼ����������ʵķֲ���
 $$\hat{x}_k=\check{x}_k + K(z_k - C_k\check{x}_k)$$
 $$\hat{P}_k = (I-KC_k)\check{P}_k$$

##9.1.3 ������ϵͳ��EKF
��$k-1$ʱ�̵ľ�ֵ��Э�������Ϊ$\hat{x}_{x-1},\hat{P}_{k-1}$����$k$ʱ�̣����ǽ��˶����̺͹۲ⷽ����$\hat{x}_{k-1},\hat{P}_{k-1}$���������Ի����õ�:
$$x_k \approx f(\hat{x}_{k-1})+\frac{\partial f}{\partial x_{k-1}}|_{\hat{x}_{k-1}}(x_{k-1}-\hat{x}_{k-1})+w_k$$
�������ƫ����Ϊ��
$$F=\frac{\partial f}{\partial x_{k-1}}|_{\hat{x}_{k-1}}$$
ͬ�������ڹ۲�����У�
$$z_k \approx h(\check{x}_k)+\frac{\partial h}{\partial x_k}|\check {x}_k$$
��ô����Ԥ�ⲽ���У������˶����̣�
$$P(x_k|x_0,u_{1:k},z_{0,k-1})=N(f(\hat{x}_{k-1},u_k),F\hat{P}_{k-1}F^T+R_k)$$
������������Э����ľ�ֵΪ��
$$\check {x}_k = f(\hat{x}_{k-1},u_k), \qquad \check{P}_k = F\hat{P}_{k-1}F^T+R_k$$
Ȼ�󣬿����ڹ۲����У�
$$P(z_k|x_k)=N(h(\check{x}_{k})+H(x_k-\check{x}_k),Q_k)$$
���ȶ���һ������������$K_k$
$$K_k=\check{P}_kH^T(H\check{P}_kH^T+Q_k)^{-1}$$
$$\hat{x}_k = \check{x}_k + K_k(z_k-h(\check{x}_k)), \qquad \hat{P}_k = (I-K_kH)\check{P}_k$$

#9.2 BA��ͼ�Ż�
##9.2.1 ͶӰģ�ͺ�BA���ۺ���
1.����������ϵת�����������ϵ
$$P^{\prime}=[X^{\prime},Y^{\prime},Z^{\prime}]^T$$
2.��$P^{\prime}$Ͷ����һ��ƽ�棬�õ���һ�����꣺
$$P_c = [u_c,v_c,1]^T=[X^{\prime}/Z^{\prime},Y^{\prime}/Z^{\prime},1]^T$$
3.���ǹ�һ������Ļ���������õ�ȥ����֮ǰ��ԭʼ�������꣬����ֻ���Ǿ�����䣺
$$\begin{cases}
u_c^{\prime}=u_c(1+k_1r_c^2+k_2r_c^4) \\
v_c^{\prime}=v_c(1+k_1r_c^2+k_2r_c^4)
\end{cases}$$
4.�����ڲ�ģ�ͣ�������������:
$$\begin{cases}
u_s=f_xu_c^{\prime}+c_x \\
v_s=f_yv_c^{\prime}+c_y
\end{cases}$$
���ϵļ���ó���**�۲ⷽ��**,��$z=h(x,y)$
$x$ָ���Ǵ�ʱ�����λ�ˣ������$R,t$����Ӧ����ȺΪ$T$,�����Ϊ$\xi$,·��$y$��ָ�����������ά��$p$,���۲�����������������$z=[u_s,v_s]^T$������С���˵ĽǶ������ǣ���ôд���˴ι۲�����Ϊ:
$$e=z-h(T,p)$$
������Ĵ��ۺ���Ϊ��
$$\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^n||e_{ij}||^2=\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^n||z_{ij}-h(T_i,p_j)||^2$$
�������С���˽�����⣬�൱�ڶ�λ�˺�·��ͬʱ���˵�����Ҳ����BA��
##9.2.2 BA�����
���ݷ������Ż���˼�룬Ӧ�ô�ĳ����ʼֵ��ʼ������Ѱ���½�����$\Delta x$�����ҵ�Ŀ�꺯�������Ž⣬������BAĿ�꺯���ϣ�Ӧ�ð��Ա�����������д��Ż�������
$$x=[T_1,\dots,T_m,p_1,\dots,p_n]^T$$
�����������е�$\Delta x$���Ƕ������Ա����������������Ǹ��Ա���һ������ʱ��Ŀ�꺯����Ϊ��
$$\frac{1}{2}||f(x+\Delta x)||^2 \approx \frac{1}{2}\sum_{i=1}^m \sum_{j=1}^n||e_{ij}+F_{ij}\Delta \xi_i+E_{ij}\Delta p_j||^2$$
���У�$F_{ij}$��ʾ�������ۺ����ڵ�ǰ״̬�¶������̬��ƫ��������$E_{ij}$��ʾ�ú�����·���λ�õ�ƫ������
���ڽ����λ�˱�������һ��Ϊ$x_c$���ռ���������һ��Ϊ$x_p$,��ʽ�ӿɼ�Ϊ:
$$\frac{1}{2}||f(x+\Delta x)||^2=\frac{1}{2}||e+F\Delta x_c + E\Delta x_p||^2$$
##9.2.3 ϡ���Ժͱ�Ե��
$H$�����ϡ���������ſɱȾ���$J(x)$����ģ�������Щ���ۺ����е�һ��$e_{ij}$����Ϊֻ�漰��$i$�����λ�˺͵�$j$��·��㣬�����ﲿ�ֱ����ĵ�����Ϊ0��
$$J_{ij}=(0_{2\times6},\dots,0_{2\times6},\dots,\frac{\partial e_{ij}}{\partial T_i},0_{2\times6},\dots,0_{1\times3},\frac{\partial e_{ij}}{\partial p_j},0_{2\times3},\dots,0_{2\times3})$$
����ϡ���ԣ�����$H$�����Ϊ��ͷ�;��󣬶�Ӧ�����Է����������$H\Delta x =g$���������ʽ:
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
��Խǿ����������Ѷ�ԶС��һ��������Ҫ�����Է�������и�˹��Ԫ���Ա�����ȥ���ϽǵķǶԽǲ���:
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
�����λ�˲��ֵ���������Ϊ:
$$[B-EC^{-1}E^T]\Delta x_c = v-EC^{-1}w$$
������������������̣�֮��ѽ�õ�$\Delta x_c$����ԭ���̣������$\Delta x_p$��������̳�ΪSchur��Ԫ��
