> 这一讲是前几讲最重要最难的一讲。

## 旋转矩阵是正交矩阵

旋转矩阵：

$$
R_{\theta}=
\begin{pmatrix}
\cos\theta & -\sin\theta \\
\sin\theta & \cos\theta
\end{pmatrix}
$$

旋转 $-\theta$ 的矩阵：
$$
R_{-\theta}=
\begin{pmatrix}
\cos\theta & \sin\theta \\
-\sin\theta & \cos\theta
\end{pmatrix}
$$
可以发现，$R_{-\theta}$ 恰好是 $R_{\theta}$ 转置，即：

$$
R_{-\theta}=R_{\theta}^{T}
$$
从定义上来看（by defination）$R_{-\theta}$ 和 $R_{\theta}^{-1}$ 刚好是一个互逆的操作。所以：$R_{-\theta}=R_{\theta}^{-1}$。

> 从数学上说，该矩阵是一个正交矩阵，非常好的性质。

## Viewing 变换

- View（视图）/Camera 变换
- Projection（投影）变换
	- （Orthographic）正交投影
	- （Perspective）透视投影

## 3D Transformation 三维变换

### 3D 齐次坐标


- 点：$(x,y,z,1)^{T}$
- 向量：$(x,y,z,0)^{T}$

对于一个 $w\neq0$ 的点，$(x,y,z,w)$ 一般认为是一个点，只需要同除以 $w$ 即可：
$$
(x/w, y / w, z / w, 1)^{T}
$$


### 3D 变换

对于仿射变换：

$$
\begin{pmatrix}
x' \\
y' \\
z' \\
1
\end{pmatrix}
=
\begin{pmatrix}
a & b & c & t_{x} \\
d & e & f & t_{y} \\
g & h & i & t_{z} \\
0 & 0 & 0 & 1
\end{pmatrix}
\cdot
\begin{pmatrix}
x \\
y \\
z \\
1
\end{pmatrix}
$$
类似于二维空间中的变换。


### 3D 缩放

$$
S(s_{x},s_{y},s_{z})=
\begin{pmatrix}
s_{x} & 0 & 0 & 0 \\
0 & s_{y} & 0 & 0 \\
0 & 0 & s_{z} & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

### 3D 平移

$$
T(t_{x},t_{y},t_{z})=
\begin{pmatrix}
1 & 0 & 0 & t_{x} \\
0 & 1 & 0 & t_{y} \\
0 & 0 & 1 & t_{z} \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

### 3D 绕轴旋转

可能是三维空间中最复杂的操作。

$$
R_{x}(\alpha)
=
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & \cos\alpha & -\sin\alpha & 0 \\
0 & \sin\alpha & \cos\alpha & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
$$
R_{y}(\alpha)
=
\begin{pmatrix}
\cos\alpha & 0 & \sin\alpha & 0 \\
0 & 1 & 0 & 0 &  \\
-\sin\alpha & 0 & \cos\alpha & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

$$
R_{z}(\alpha)=\begin{pmatrix}
\cos\alpha & -\sin\alpha & 0 & 0 \\
\sin\alpha & \cos\alpha & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

![image.png](https://ccccooh.oss-cn-hangzhou.aliyuncs.com/img/202602182023094.png)

一个有趣的规律，绕对应的轴旋转，对应行不改变。比如绕 $y$ 轴旋转，第二行是不变的。

那么，为什么这里的 $y$ 轴旋转矩阵形式不太一样？

如果给你 $x \times y$ 轴，通过右手螺旋定则可以得到 $z$ 轴。同样的，用 $y \times z$ 也可以得到 $x$ 轴，称之为 `循环对称` 性质。但是用 $x \times z$ 得到的是 $-y$，用 $z\times x$ 才能得到 $y$。

> 任何复杂旋转都可以分解为绕轴旋转的组合。


