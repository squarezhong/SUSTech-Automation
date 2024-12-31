<p align='center'><font size=8><b>最小二乘和系统辨识</b></font></p>

# 回顾-最小二乘法

对于某个系统$y(t)= \Theta x(t)$，我们可以选取一系列的y和x，组成矩阵$Y,X$，对参数进行估计：
$$
\begin{aligned}
Y&=X\Theta\\
\Theta&=(X^TX)^{-1}X^TY
\end{aligned}
$$

# 使用最小二乘法进行系统辨识

对于系统：
$$
y(k)=W_y(q^{-1},\theta)y(k)+W_u(q^{-1,\theta})u(k)+e(k)
$$
通过预估参数$W_y,~W_u$，可以得到预测值：
$$
\hat y(k|\theta)=W_y(q^{-1},\theta)y(k)+W_u(q^{-1},\theta)u(k)
$$
换句话说，使用最小二乘法，我们的目的是辨识系统的$\pmb a,~\pmb b$参数。值得注意的是，噪声项通常是干扰，所以我们通常不对噪声项前的参数进行辨识。不过可能会对噪声的分布情况进行计算。

这样可能太过于晦涩难懂了。让我们来以某个假想中的系统为例，来理解最小二乘法和系统辨识。

* **案例**-对某个系统：

$$
\begin{aligned}
y(k)-a_1(k-1)-a_2y(k-2)&=b_1u(k-3)+b_2u(k-4)+\xi(k)\\
a_1= 1.5,&~a_2=-0.7	\\
b_1= 1.0,&~b_2 = 0.5
\end{aligned}
$$

其中，$\xi(k)$是噪声。现在，让我们采用最小二乘法对其进行系统辨识。

在解答这个题前，让我们假设，当时间小于0的时候，我们假设所有的输出、输入均为0。课程官方文档见[example211.m](../../matcodes/cpt2/example211.m)

我们将带有需要预估参数的部分写在等式右侧，这个系统可以被写为：
$$
\begin{aligned}
y(k)&=
a_1y(k-1)+a_2y(k-2)+b_1u(k-3)+b_2u(k-4)+\xi(k)\\
&=
\begin{bmatrix}y(k-1)~y(k-2)~u(k-3)~u(k-4)\end{bmatrix}
\begin{bmatrix}a_1~a_2~b_1~b_2\end{bmatrix}^T
\end{aligned}
$$
因此，我们将需要估计的参数构造成参数矩阵$\Theta=\begin{bmatrix}a_1~a_2~b_1~b_2\end{bmatrix}^T$，单次输入$x=[y(k-1)~y(k-2)~u(k-3)~u(k-4)]$

通过计算，我们可以得出一系列的y和x，将它们组合：
$$
\begin{aligned}
\begin{bmatrix}y(1)\\y(2)\\y(3)\\...\\y(N)\end{bmatrix}
=\begin{bmatrix}
y(0)&y(-1)&u(-2)&u(-3)\\
y(1)&y(0)&u(-1)&u(-2)\\
y(2)&y(1)&u(0)&u(-1)\\
...&...&...&...\\
y(N-1)&y(N-2)&u(N-3)&u(N-4)\end{bmatrix}
\begin{bmatrix}
a_1\\a_2\\b_1\\b_2
\end{bmatrix}
\end{aligned}
$$
最后我们解出这个方程就可以了。

# 有权最小二乘法

上文中提到，最常见的最小二乘法，代价函数通常选用Square Function：
$$
J=\sum(z(k)-y(k))^2
$$
考虑权重，人们提出了一种新的代价函数：
$$
J_k=\beta_k\sum(z(k)-y(k))^2
$$
其中，$\beta_k$表示第k次迭代计算的时候选区的代价函数的权重。在矩阵下，我们可以将权重构造成一个对角矩阵：
$$
\pmb\beta=\begin{bmatrix}
\beta(1)&0&...&0\\
0&\beta(2)&...&0\\
...&...&...&...\\
0&0&...&\beta(N)\end{bmatrix}
$$


采用这种方法，得到的参数的计算方法为：
$$
\Theta=(\pmb \beta^T\Phi\Phi^T)^{-1}\pmb \beta\Phi Y
$$

> 延伸
>
> 1. 当$\pmb\beta=I$时，它将变成普通的最小二乘法
> 2. 当$\beta(k)=\alpha\lambda^{N-k}~(\alpha>0,~0<\lambda<1)$时，这样的有权最小二乘法也叫*消失记忆最小二乘法*。其中，$N$为样本总数。
> 3. The weighted least squares method is only used to estimate the influence of the measurement errors on parameter estimates in advance.

# 递归最小二乘法

* 在线辨识

暂略

事实上，递归最小二乘相当于，每次迭代到k时刻的输入和输出，就对参数$\theta$进行一次更新（因此其可以用来实现在线更新），其基本结构为：
$$
\hat\theta_k=\hat\theta_{k-1}+R^{-1}(k)\phi(k)[y(k)-\phi^{T}(k)\hat\theta_{k-1}]\\
R(k)=R(k-1)+\phi(k)\phi^T(k)
$$
其中，$\phi(k)$为第k次的输入。

> 事实上，我们将上面的式子交换一下顺序：
$$
\begin{aligned}
\hat\theta_k&=\hat\theta_{k-1}+R^{-1}(k)\phi(k)y(k)-R^{-1} (k)\phi(k)\phi^{T}(k)\hat\theta_{k-1}\\
&=(I-R^{-1}(k)\phi(k)\phi^{T}(k))\hat\theta_{k-1}+R^{-1}(k)\phi(k)\cdot y(k)\\
&=(I-R^{-1}(k)\phi(k)\phi^{T}(k))\hat\theta_{k-1}+R^{-1}(k)\phi(k)\cdot\phi(k)^T\theta_k\\
&=(I-F)\hat\theta_{k-1}+F\theta_k
\end{aligned}
$$
> 惊讶的发现，这是一个一阶低通滤波器的模型。因而，若系统稳定，我们想办法让该方法递归得到的$\theta_k$随着时间趋近于收敛，就能够实现递归的最小二乘法。

==todo== 推导

最终，在线更新的方程将变为：
$$
\begin{aligned}
\hat{\theta}(k) &= \hat{\theta}(k-1) + K(k) \left[ y(k) - \phi^T(k)\hat{\theta}(k-1) \right]\\
K(k) &= \frac{P(k-1)\phi(k)}{1 + \phi^T(k)P(k-1)\phi(k)}\\
P(k) &= P(k-1) - \frac{P(k-1)\phi(k)\phi^T(k)P(k-1)}{1 + \phi^T(k)P(k-1)\phi(k)}
\end{aligned}
$$
# 递归最小二乘法

课程官方教学matlab文件：[example232.m](../../matcodes/cpt2/example232.m)

乘上具有遗忘因子性质的权重$\beta$即可。例如，当$\beta(k)=\lambda^{N-k}$时：
$$
\begin{aligned}
\hat\theta_k=\hat\theta_{k-1}+R^{-1}(k)\phi(k)[y(k)-\phi^{T}(k)\hat\theta_{k-1}]\\
R(k)=\lambda R(k-1)+\phi(k)\phi^T(k)
\end{aligned}
$$
递归公式为：
$$
\begin{aligned}
\hat{\theta}(k) &= \hat{\theta}(k-1) + K(k) \left[ y(k) - \phi^T(k)\hat{\theta}(k-1) \right]\\
K(k) &= \frac{P(k-1)\phi(k)}{1 + \phi^T(k)P(k-1)\phi(k)}\\
P(k) &= \frac1\lambda\left[ P(k-1) - \frac{P(k-1)\phi(k)\phi^T(k)P(k-1)}{\lambda + \phi^T(k)P(k-1)\phi(k)}\right]
\end{aligned}
$$
# 泛最小二乘

课程官方教学matlab文件：[example241.m](../../matcodes/cpt2/example241.m)

==todo==（大概是一窝蜂的把所有的a，b都写上去，时间不够，先跳过了。）

# 多变量系统的最小二乘系统辨识方法

课程官方教学matlab文件：[example251.m](../../matcodes/cpt2/example251.m)

==todo==（大概是相当于把单变量的矩阵拼接起来，时间不够，先跳过了）