#5.1相机模型
##5.1.1针孔相机模型
$$\begin{cases}
u=\alpha X^{\prime}+c_x \\
v = \beta Y^{\prime} + c_y
\end{cases}$$
$$
\begin{cases}
u = f_x \frac{X}{Z}+c_x \\
v = f_y \frac{Y}{Z}+c_y
\end{cases}$$

$$
\left \{
\begin{matrix}
u \\
v \\
1
\end{matrix}
\right \}
=\frac{1}{Z}
\left \{
\begin{matrix}
f_x & 0   & c_x \\
0   & f_y & c_y \\
0   & 0   & 1
\end{matrix}
\right \}
\left \{
\begin{matrix}
X \\
Y \\
Z
\end{matrix}
\right \}=\frac{1}{Z}KP$$

$$
Z\left \{
\begin{matrix}
u \\
v \\
1
\end{matrix}
\right \}
=\frac{1}{Z}
\left \{
\begin{matrix}
f_x & 0   & c_x \\
0   & f_y & c_y \\
0   & 0   & 1
\end{matrix}
\right \}
\left \{
\begin{matrix}
X \\
Y \\
Z
\end{matrix}
\right \}=KP$$
$K$为相机的内参数矩阵，而运动过程则用外参来表示
$$ZP_{uv}=Z
\left [
\begin{matrix}
u \\
v \\
1
\end{matrix}
\right ]=K(RP_w+t)=KTP_w$$
归一化投影：
$$(RP_w+t)=[X,Y,Z]^T \rightarrow [X/Z,Y/Z,1]^T$$
##5.1.2畸变模型
通过五个畸变系数找到点在像素平面上的正确位置
1.设三维空间点的归一化坐标为$[x,y]^T$
2.计算径向畸变和切向畸变
$$
\begin{cases}
x_{distored}=x(1+k_1r^2+k_2r^4+k_3r^6)+2p_1xy+p_2(r^2+2x^2) \\
y_{distored}=y(1+k_1r^2+k_2r^4+k_3r^6)+p_1(r^2+2y^2)+2p_2xy
\end{cases}$$
3.将畸变后的点通过内参数矩阵投影到像素平面，得到该点在图像上的正确位置
$$\begin{cases}
u = f_x x_{distored}+c_x \\
v = f_y y_{distored}+c_y
\end{cases}$$
##5.1.3双目相机模型
$$\frac{z-f}{z}=\frac{b-u_L+u_R}{b}$$
$$z=\frac{fb}{d},d=u_L-u_R$$
##5.1.4RGB-D相机模型
#5.2图像
```cpp
unsigned char image[480][640]
```
#5.3计算机中的图像
##5.3.1OpenCV的基本使用方法
