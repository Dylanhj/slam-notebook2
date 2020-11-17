#4.1李群与李代数基础
旋转和变换矩阵对于加法不封闭；
对乘法封闭，乘法对应着旋转或者变换的集合，两个旋转矩阵相乘表示做了两次旋转。
##4.1.1群
群是一种集合加上一种运算的代数结构
- 封闭性：$\forall a_1,a_2\in A,a_1\cdot a_2 \in A.$
- 结合律：$\forall a_1,a_2,a_3\in A,(a_1\cdot a_2)\cdot a_3 = a_1\cdot (a_2\cdot a_3)$
- 幺元：$\exist a_0 \in A , s.t. \forall a \in A, a_0 \cdot a_0 =a$
- 逆：$\forall a \in A, \exist a^{-1} \in A, s.t.  a \cdot a^{-1} = a_0$

李群是指具有连续（光滑）性质的群。
##4.1.2李代数的引出
$$RR^T =I$$
$$R(t)R(t)^T=I$$
对$t$求导得：
$$\dot{R}(t)R(t)^T=-(\dot{R}(t)R(t)^T)^T$$
$$\dot{R}(t)R(t)^T=\phi (t)^{\wedge}$$
$$\dot{R}(t)=\phi(t)^{\wedge}R(t)$$
$$
\begin{aligned}
R(t)  \approx &  R(t_0)+\dot{R}(t_0)(t-t_0) \\
            = & I +\phi(t_0)^{\wedge}(t)
\end{aligned}
$$
$\phi$反应了$R$的导数性质，称其在$SO(3)$原点附近的正切空间上。在$t_0$附近，设$\phi(t_0)=t_0$,则
$$\dot{R}(t)=\phi(t_0)^{\wedge}R(t)=\phi_0^{\wedge}R(t)$$
$$R(t)=exp(\phi_0^{\wedge}t)$$

##4.1.3李代数的定义
每个李群都有对应的李代数，由一个集合$V$,一个数域$F$和一个二元运算$[,]$组成：
- 封闭性 $\forall X,Y \in V,  [X,Y]\in V$
- 双线性 $\forall X,Y,Z \in V,a,b \in F$，有
$[aX+bY,Z]=a[X,Z]+b[Y,Z],[Z,aX+bY]=a[Z,X]+b[Z,Y]$
- 自反性 $\forall X \in V, [X,X]=0$
- 雅可比等价 $\forall X,Y,Z \in V, [X,[Y,Z]]+[Z,[X,Y]]+[Y,[Z,X]]=0$
##4.1.4李代数so(3)
$$so(3)=\{\phi \in R^3,\Phi = \phi ^{\wedge}\in R^{3\times 3}\}$$
$$R=exp(\phi ^{\wedge})$$

##4.1.5李代数se(3)
$$se(3)=\begin{cases}
\xi = \left[ 
      \begin{matrix}
      \rho \\
      \phi
      \end{matrix}
      \right] \in R^6 ,\rho \in R^3, \phi \in so(3),\xi^{\wedge}=\left[
          \begin{matrix}
          \phi ^{\wedge} & \rho \\
          0^T & 0
          \end{matrix}
      \right]
\end{cases}$$

#4.2指数与对数映射
##4.2.1SO(3)上的指数映射
$$exp(A)=\sum_{n=0}^{\infty}\frac{1}{n!}A^n$$
$$exp(\phi^{\wedge})=\sum_{n=0}^{\infty}\frac{1}{n!}(\phi ^{\wedge})^n$$
设$\phi=\theta a$,$||a||=1$
$$a^{\wedge}a^{\wedge}=aa^T-I$$
$$a^{\wedge}a^{\wedge}a^{\wedge}=a^{\wedge}(aa^T-I)=-a^{\wedge}$$
$$
\begin{aligned}
exp(\phi^{\wedge})&=\sum_{n=0}^{\infty}\frac{1}{n!}(\theta a ^{\wedge})^n \\
&= cos\theta I + (1-cos\theta)aa^T +sin \theta a^{\wedge}
\end{aligned}$$
其类型与罗德里格斯公式相似，$so(3)$实际就是旋转向量组成的空间，指数映射即为罗德里格斯公式
##4.2.2SE(3)上的指数映射
$$\begin{aligned}
exp(\xi ^)&=\left[
    \begin{matrix}
    \sum_{n=0}^{\infty}\frac{1}{n!} & \sum_{n=0}^{\infty}\frac{1}{(n+1)!}(\phi^{\wedge})^n \rho \\
    0^T & 1
    \end{matrix}
    \right] \\
    &=\left [
        \begin{matrix}
R & J\rho \\
0^T & 1
        \end{matrix}
    \right]=T
    \end{aligned}
$$
$$J=\frac{sin\theta}{\theta}I+(1-\frac{sin\theta}{\theta})aa^T+\frac{1-cos\theta}{\theta}a^{\wedge}$$

#4.2李代数求导与扰动模型
##4.3.1BCH公式与近似形式
$$ln(exp(A)exp(B))=A+B+\frac{1}{2}[A,B]+\frac{1}{12}[A,[A,B]]-\frac{1}{12}[B,[A,B]]+...$$
$$ln(exp(\phi _1^{\wedge})exp(\phi _2^{\wedge}))^{\vee}\approx \begin{cases}
J_1(\phi _2)^{-1}\phi _1 +\phi _2  当\phi _1为小量 \\
J_2(\phi _1)^{-1}\phi _2 +\phi _1  当\phi _2为小量
\end{cases}$$

$$exp(\Delta \phi ^{\wedge})exp(\phi ^ {\wedge})=exp((\phi+J_1^{-1}(\phi)\Delta \phi)^{\wedge})$$
$$exp((\phi+\Delta\phi)^{\wedge})=exp((J_l\Delta\phi)^{\wedge})exp(\phi^{\wedge})=exp(\phi ^{\wedge})exp((J_r\Delta\phi)^{\wedge})$$

##4.3.2 SO(3)上的李代数求导
$$z=Tp+w$$
$$e=z-Tp$$
$$minJ(T)=\sum_{i=1}^{N}\lVert z_i -Tp_i\rVert _2^2$$
##4.3.3李代数求导
$$\frac{\partial(Rp)}{\partial R}$$
$$\frac{\partial (exp(\phi ^{\wedge}))p}{\partial \phi}=-(Rp)^{\wedge}J_l$$

##4.3.4扰动模型（左乘）
$$\frac{\partial(Rp)}{\partial \varphi}=\lim _{\varphi \rightarrow0}\frac{exp(\varphi ^{\wedge})exp(\varphi ^{\wedge})p-exp(\varphi ^{\wedge})p}{\varphi}=-(Rp)^{\wedge}$$

##4.3.5 SE(3)上的李代数求导
$$\frac{\partial(Rp)}{\partial \delta \xi}=\lim _{\delta \xi \rightarrow0}\frac{exp(\delta \xi ^{\wedge})exp(\xi ^{\wedge})p-exp(\xi ^{\wedge})p}{\delta \xi}=\left[ \begin{matrix} I & -(Rp+t) \\
                       0^T & 0^T \end{matrix} \right]$$
