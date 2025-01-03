<p align='center'><font size=8><b>系统辨识方法</b></font></p>

# 阶跃响应法

见第一章。

# 最大似然估计法

见第一章。

# 相关分析法

* 相关分析原理：根据输入和输出数据，辨识出系统的**脉冲响应函数**g(t)。

在频域下，我们知道，对于某开环传递系统，其传递函数为G(s)时，
$$
Y(s)=G(s)U(s)
$$
转换到频域，将会是我们熟悉的卷积：
$$
y(t)=\int_{-\infty}^{\infty}g(\tau)u(t-\tau)d\tau
$$
离散状态下，它将被写作：
$$
y(nT)=\sum_{i=0}^{n-1}g(iT)u(nT-iT-T)\cdot T
$$

* 进行系统辨识-脉冲响应方法

$$
y(nT)= T\sum_{i=0}^{n-1}g(iT)u(nT-iT-T)\\
$$

无噪声情况下，
$$
Y=\begin{bmatrix} y(T)\\y(2T)\\...\\y(nT)\end{bmatrix},~
G=\begin{bmatrix} g(u)\\g(1)\\...\\g(NT-T)\end{bmatrix},~
U=\begin{bmatrix} 
u(0)	&0		&...	&0		\\
u(T)	&u(0)	&...	&0		\\
...&...&...&...\\
u(nT-T)	&...	&u(T)	&0
\end{bmatrix}
$$
则：
$$
\begin{aligned}
Y&=T\cdot UG\\
G&=\frac1T U^{-1}Y
\end{aligned}
$$
接下来，对于传递函数$G(q^{-1})=\sum_{i=1}^{\infty}g(i)q^{-i}$, 



* 相关性分析法

通常我们的系统包含噪声（理想情况下，测量噪声将会与输入信号相互独立；此外，通常假设测量噪声是白噪声，即均值为0的高斯噪声），假设z(t)为实际的输出变量，y为被我们观测到的含噪声的输出，在t时刻：
$$
\begin{aligned}
z(t)&=\int_{-\infty}^{\infty}g(\lambda)u(t-\lambda)d\lambda\\
y(t)&=z(t)+v(t)\\
&=\int_{-\infty}^{\infty}g(\lambda)u(t-\lambda)d\lambda+v(t)
\end{aligned}
$$
通常，我们在0时刻后给予输入u，也就是说，$u(t)=0,~t<0$，因此，我们可以直接将积分下限改为0。

左右两边同时乘以$u(t-\tau)$:
$$
\begin{aligned}
y(t)u(t-\tau)&=[\int_{0}^{\infty}g(\lambda)u(t-\lambda)d\lambda+v(t)]\cdot u(t-\tau)\\
\end{aligned}
$$
根据期望公式求取左右两边期望，也必然是相等的。（注意：求期望时，$t$是自变量，$\tau, \lambda$当作参量，因为我们用的是卷积的结果来求期望）
$$
\begin{aligned}
\lim_{t\rightarrow\infty}\frac1T\int_0^T y(t)u(t-\tau)dt
&=
\int_0^\infty g(\lambda)[\lim_{t\rightarrow \infty}\frac1T\int^T_0u(t-\lambda)u(t-\tau)dt]d\lambda\\
&+&\lim_{t\rightarrow \infty}\frac1T\int^T_0 v(t)u(t-\tau)dt
\\
\end{aligned}
$$

当$v(t),~u(t)$无关时，$\int^T_0 v(t)u(t-\tau)dt=0$（协方差为0）：

$$
\lim_{t\rightarrow\infty}\frac1T\int_0^T y(t)u(t-\tau)dt
=
\int_0^\infty g(\lambda)[\lim_{t\rightarrow \infty}\frac1T\int^T_0u(t-\lambda)u(t-\tau)dt]d\lambda
$$

现在，接下来，我们根据协方差计算公式，计算u，y有关的协方差和方差：
$$
\begin{aligned}
R_{uy}(\tau)&=\lim_{t\rightarrow\infty}\frac1T\int_0^Ty(t)u(t-\tau)dt\\
R_{uu}(\tau)&=\lim_{t\rightarrow\infty}\frac1T\int_0^Tu(t)u(t-\tau)dt
\end{aligned}
$$
因此，上面的式子可以被改写为：
$$
\begin{aligned}
\lim_{t\rightarrow\infty}\frac1T\int_0^T y(t)u(t-\tau)dt
&=
\int_0^\infty g(\lambda)[\lim_{t\rightarrow \infty}\frac1T\int^T_0u(t-\lambda)u(t-\tau)dt]d\lambda
\\
R_{uy}(\tau)&=\int_0^\infty g(\lambda)R_{uu}(\tau-\lambda)d\lambda
\end{aligned}
$$

如果u输入为白噪声（均值为0，方差为$\sigma$的高斯函数），根据白噪声的特性，$R_{uu}(\tau)=\sigma^2\delta(\tau)$。

据此，我们可以计算得出：
$$
\begin{aligned}
R_{uy}(\tau)&=\int_0^\infty g(\lambda)R_{uu}(\tau-\lambda)d\lambda\\
&=\int_0^\infty g(\lambda)\sigma^2\delta(\tau-\lambda)d\lambda\\
&=\sigma^2g(\tau)\\
g(\tau)&=\frac1{\sigma^2}R_{uy}(\tau)
\end{aligned}
$$

> $\int_0^\infty g(\lambda)\sigma^2\delta(\tau-\lambda)d\lambda$中，$\delta(\tau-\lambda)$只有在$\tau-\lambda=0$的时候，有值且满足$\int_{\tau-}^{\tau+}\delta(\tau-\lambda)d\lambda$；其他时候值为0:
> $$
> \int_0^\infty g(\lambda)\sigma^2\delta(\tau-\lambda)d\lambda\\
> =\sigma^2g(\tau)\int_{\tau-}^{\tau+} \delta(\tau-\lambda)d\lambda
> $$

* 使用M序列辨识脉冲响应

将上述的式子调整到离散空间中，可得：
$$
\begin{aligned}
R_{uu}(m-j)&=\frac1{n_p}\sum_{k=0}^{n_p-1}u(k-m)u(k-j)\\
R_{uy}(m)&=\sum_{j=0}^{n_p-1}g(j)R_{uu}(m-j)\\
&=\frac 1{n_p}\sum_{k=0}^{n_p-1}u(k-m)y(k)
\end{aligned}
$$
由于我们需要使用m序列作为输入，m序列的自相关函数满足：
$$
R_{uu}(m-j) = 
\begin{cases} 
a^2 & \text{if } m-j = 0 \\
-\frac{a^2}{n_p} & \text{if } 1 \leq (m-j) \leq n_p - 1 
\end{cases}
$$
其中，a是m序列的幅度。这时，我们再带入：
$$
\begin{aligned}
R_{uy}(m)&=\sum_{j=0}^{n_p-1}g(j)R_{uu}(m-j)\\
&=a^2g(m)-\frac{a^2}{n_p}[\sum_{j=0}^{m-1}g(j)+\sum_{j=m+1}^{n_p-1}g(j)]\\
&=a^2g(m)+\frac{a^2}{n_p}g(m)-\frac{a^2}{n_p}\sum_{j=0}^{n_p-1}g(j)\\
&=\frac{n_p+1}{n_p}a^2g(m)-\frac{a^2}{n_p}\sum^{n_p-1}_{j=0}g(j)\\
&=\frac{n_p+1}{n_p}a^2g(m)-c
\end{aligned}
$$
其中， $c=\frac{a^2}{n_p}\sum^{n_p-1}_{j=0}g(j)$。

而：

$$
\begin{aligned}
\sum_{j=0}^{N_p - 1} R_{uy}(j) 
&= \sum_{j=0}^{N_p - 1} \left( \frac{N_p + 1}{N_p} a^2 g(j) - c \right)\\

&= \sum_{j=0}^{N_p - 1} \left( \frac{N_p + 1}{N_p} a^2 g(j) \right) - N_p c\\

&= \sum_{j=0}^{N_p - 1} \left( \frac{N_p + 1}{N_p} a^2 g(j) \right) - a^2 \sum_{j=0}^{N_p - 1} g(j)\\

&= a^2 \left( \frac{N_p + 1}{N_p} - 1 \right) \sum_{j=0}^{N_p - 1} g(j)\\

&= \frac{a^2}{N_p} \sum_{j=0}^{N_p - 1} g(j)\\ &= c
\end{aligned}
$$

取出上式的$g(m)=\frac{n_p}{n_p+1}\cdot\frac 1{a^2}(R_{uy}(m)+c)$，当m趋近于无穷大时，$g(m)=0$，此时，$c=-R_{uy}(\infty)$；而当采样点数$n_p$足够大的时候，由上式可知，c可以被忽略，即：
$$
g(m)=\frac{n_p}{n_p+1}\cdot\frac 1{a^2}R_{uy}(m)
$$
为了让系统辨识更准确，我们让M序列重复r次，那么：
$$
R_{uy}(m)=\frac1{rn_p}\sum_{k=0}^{rn_p-1}u(k-m)y(k),~m=0,1,...,n_p-1
$$
