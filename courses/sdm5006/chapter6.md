<p align='center'><font size=8><b>自校正控制</b></font></p>

# 最小方差自校正控制

温馨提示：当您在查阅本节内容时，我们强烈推荐您挑选一个较为连续的时间段，携带笔和草稿纸，并保证草稿纸有充足的空间。我们强烈的推荐您一边对照本节内容一边进行内容推导。

## 丢番图方程

对于方程：
$$
\sum a_ix_i=0
$$
要求所有解必须是整数的方程，称为丢番图方程；所有整数解的集合，称为丢番图方程的解。例如：
$$
2x+3y=15,x\in R^+,y\in R^+
$$
这个方程的解将会是$\left\{x,y\right\}=\{\{3,2\},\{6,1\}\}$。

尽管我还不知道丢番图方程和系统辨识的关系……

## Diophantine方程与自适应控制

对于系统：
$$
A(q^{-1})y(k)=B(q^{-1})u(k-d)+C(q^{-1})\xi(k)\tag{6.1.1}
$$
接下来的这组方程，被称为Diophantine方程：
$$
\begin{aligned}
C(q^{-1})&=A(q^{-1})E(q^{-1})+q^{-d}G(q^{-1})\\
F(q^{-1})
&=B(q^{-1})E(q^{-1})
\end{aligned}\tag{6.2.1}
$$

解方程：
$$
e_i=c_i-\sum_{j=1}^ie_{i-j}a_j,~i=1,2,...,n_e\\
g_i=c_{i+d}-\sum_{j=0}^{n_e}e_{n_e-j}a_{i+j+1},~i=0,1,...,n_g
$$


也许你会认为上面的描述过于抽象。接下来，让我们以一个例子来对其进行解释。例如，系统为：
$$
y(k) - 1.7y(k-1) + 0.7y(k-2) = u(k-4) + 0.5u(k-5) + \xi(k) + 0.2\xi(k-1)
$$

可知其参数为：
$$
\begin{aligned}
a_1 = -1.7,& \quad a_2 = 0.7, \\
b_0 = 1,& \quad b_1 = 0.5\\
c_0 = 1,& \quad c_1 = 0.2, \\
n_a = 2, \quad n_b = 1,& \quad n_c = 1, \quad d = 4
\end{aligned}
$$

According to Eq. xxx,

$$
\begin{aligned}
n_e &= d - 1 = 3\\
n_g &= n_a - 1 = 1 \\
n_f &= n_b + d - 1 = 4
\end{aligned}
$$



## 最小方差自校正控制律

目标：最小化输出$y(t)$的方差。

有一说一，单纯对于最小方差自校正控制律的分析，知乎这一份回答值得一看，尽管它和课件略有出入。https://zhuanlan.zhihu.com/p/656282259

对于上述系统而言，假设F，C，G为其丢番图方程解，最小方差控制律将会是：
$$
F(q^{-1})u(k)=C(q^{-1})y_r(k+d)-G(q^{-1})y(k)
$$

这里我们需要用到式（6.1.1）和（6.2.1）

>它们分别是：

$$
\begin{align}
\begin{cases}
C&=A(q^{-1})E(q^{-1})+q^{-d}G(q^{-1})\\
F(q^{-1})&=B(q^{-1})E(q^{-1})\\
\end{cases}\tag{6.1.1}\\
A(q^{-1})y(k)=q^{-d}B(q^{-1})u(k)+C(q^{-1})\xi(k)\tag{6.2.1}
\end{align}
$$

首先，把（6.1.1）带入（6.2.1）得到：

$$
\begin{aligned}
A(q^{-1})y(k) &= q^{-d}B(q^{-1}) u(k) + A(q^{-1})E(q^{-1}) + q^{-d}G(q^{-1})\xi(k)\\
\rightarrow
y(k) &= \frac{q^{-d}B(q^{-1})}{A(q^{-1})} u(k) + \frac{A(q^{-1})E(q^{-1}) + q^{-d}G(q^{-1})}{A(q^{-1})} \xi(k)\\
&=\frac{q^{-d}B(q^{-1})}{A(q^{-1})} u(k) + \left(E(q^{-1})+\frac{q^{-d}G(q^{-1})}{A(q^{-1})}\right) \xi(k)\\
&=E(q^{-1})\xi(k)+\frac{q^{-d}B(q^{-1})}{A(q^{-1})} u(k) +\frac{q^{-d}G(q^{-1})}{A(q^{-1})}\xi(k)
\end{aligned}
$$

然后，我们将它k改为k+d时刻的输出：
$$
\begin{aligned}
y(k+d) &= E(q^{-1})\xi(k+d)+\frac{q^{-d}B(q^{-1})}{A(q^{-1})} u(k+d) +\frac{q^{-d}G(q^{-1})}{A(q^{-1})}\xi(k+d)\\
&= E(q^{-1})\xi(k+d)+\frac{B(q^{-1})}{A(q^{-1})} u(k) +\frac{G(q^{-1})}{A(q^{-1})}\xi(k)
\end{aligned}
$$
随后，我们根据（6.2.1）式可以知道$\xi(k)=\frac{A(q^{-1})y(k)-q^{-d}B(q^{-1})u(k)}{C(q^{-1})}$，将它带入上式第三项：
$$
\begin{aligned}
y(k+d) &= E(q^{-1})\xi(k+d)+\frac{q^{-d}B(q^{-1})}{A(q^{-1})} u(k+d) +\frac{q^{-d}G(q^{-1})}{A(q^{-1})}\xi(k+d)\\
&= E(q^{-1})\xi(k+d)+\frac{B(q^{-1})}{A(q^{-1})} u(k) +\frac{G(q^{-1})}{A(q^{-1})}
\frac{A(q^{-1})y(k)-q^{-d}B(q^{-1})u(k)}{C(q^{-1})}\\
&= E(q^{-1})\xi(k+d)+\frac{B(q^{-1})}{A(q^{-1})} u(k) +
\frac{G(q^{-1})}{C(q^{-1})}y(k)-
\frac{q^{-d}G(q^{-1})B(q^{-1})}{A(q^{-1})C(q^{-1})}u(k)\\
&= E(q^{-1})\xi(k+d)+
\frac{G(q^{-1})}{C(q^{-1})}y(k)+
\frac{B(q^{-1})\left(C(q^{-1})-q^{-d}G(q^{-1})\right)}{A(q^{-1})C(q^{-1})}u(k)\\
\end{aligned}
$$
由式（6.1.1）我们可以知道，$C(q^{-1})q^{-d}G(q^{-1})=A(q^{-1})E(q^{-1}),~B(q^{-1})E(q^{-1})=F(q^{-1})$，因此：
$$
\begin{aligned}
\frac{B(q^{-1})\left(C(q^{-1})-q^{-d}G(q^{-1})\right)}{A(q^{-1})C(q^{-1})}&=\frac{B(q^{-1})A(q^{-1})E(q^{-1})}{A(q^{-1})C(q^{-1})}\\
&=\frac{B(q^{-1})E(q^{-1})}{C(q^{-1})}\\
&=\frac{F(q^{-1})}{C(q^{-1})}
\end{aligned}
$$
最终得出：
$$
y(k+d) = E(q^{-1})\xi(k+d)+
\frac{G(q^{-1})}{C(q^{-1})}y(k)+
\frac{F(q^{-1})}{C(q^{-1})}u(k)\tag{6.2.3*}
$$

因此，代价函数可以被改写为：
$$
\begin{aligned}
J(k) &= \mathbb{E} \left\{ e^2(k+d|k) \right\} \\
     &= \mathbb{E} \left\{ \left( y(k+d) - \hat{y}(k+d|k) \right)^2 \right\} \\
     &= \mathbb{E} \left\{ \left( E(q^{-1}) \xi(k+d) + \frac{F(q^{-1})}{C(q^{-1})} u(k) + \frac{G(q^{-1})}{C(q^{-1})} y(k) - \hat{y}(k+d|k) \right)^2 \right\} \\
     &= \mathbb{E} \left\{ \left( E(q^{-1}) \xi(k+d) \right)^2 \right\} \\
     &\quad+ \mathbb{E} \left\{ 2 E(q^{-1}) \xi(k+d) \left( \frac{F(q^{-1})}{C(q^{-1})} u(k) + \frac{G(q^{-1})}{C(q^{-1})} y(k) - \hat{y}(k+d|k) \right) \right\} \\
     &\quad + \mathbb{E} \left\{ \left( \frac{F(q^{-1})}{C(q^{-1})} u(k) + \frac{G(q^{-1})}{C(q^{-1})} y(k) - \hat{y}(k+d|k) \right)^2 \right\}.
\end{aligned}\tag{6.2.4}
$$
第二项中，由于白噪声$\mathbb{E}\left(\xi(k+d)\right)$的数学期望为0，因此第二项也为0。第一项因为噪声是我们无法控制的部分且和控制u无关，因此我们不进行分析。因此，我们期望使得第三项最小，第三项取最小的时候，显然：
$$
\frac{F(q^{-1})}{C(q^{-1})} u(k) + \frac{G(q^{-1})}{C(q^{-1})} y(k) - \hat{y}(k+d|k)=0
$$
最好的情况下，**预测输出和期望输出相等**，即$\hat y(k+d|k)=y_r(k+d)$。课件Chapter6-part的第17小页（第9大页）证明了为什么这种情况会最好，不过我相信聪明的你的直觉已经告诉你这一点了，因此这里我将不作证明。

最终得出控制律为：
$$
F(q^{-1})u(k)=C(q^{-1})y_r(k+d)-G(q^{-1})y(k)
$$

# 最小方差间接自校正控制

通俗来说，在不知道系统参数的时候，我们需要辨识得到系统参数才能进行自校正控制。其实就是**一边进行系统辨识，一边进行自校正控制**。

# 广义最小方差自校正控制

其实就是算方差的时候加了权重，甚至给控制信号也添加了权重。

对于（6.1.1）所表示的系统：
$$
A(q^{-1})y(k)=B(q^{-1})u(k-d)+C(q^{-1})\xi(k)
$$
在设立方差的时候，我们可以给**实际输出、期望输出和输入带上权重**，构造带有权重的方差。我们期望最小化系统输出和期望输出与输入的**加权方差**。因此，我们可以使用三组权重$P,R,Q$,让我们期望的式子变成：
$$
J_{\text{min}} = \mathbb{E} \left\{ \left(P(q^{-1})y(k + d)-R(q^{-1})y_r(k + d)\right)^2+\left(Q(q^{-1})u(k) \right)^2 \right\}
$$

## 广义最小方差控制律

使得该方差最小的系统输入是：
$$
u(k) = \frac{R(q^{-1})y_r(k+d) - P(q^{-1})y^*(k+d|k)}{\frac{q_0}{b_0} Q(q^{-1})}\tag{6.3.3}
$$
也可以是：
$$
u(k) = \frac{C(q^{-1})R(q^{-1})y_r(k+d) - G(q^{-1})P(q^{-1})y(k)}{\frac{q_0}{b_0} C(q^{-1})Q(q^{-1}) + F(q^{-1})P(q^{-1})}\tag{6.3.4}
$$




# 极点配置的自校正控制

对于下面这个控制系统：

![c6-pole-tuning](imgs/c6-pole-tuning.svg)

一通计算猛如虎，我们可以计算出，上面这个系统的输出是：
$$
\begin{align}
y(k) &= \frac{\frac{R(q^{-1})q^{-d}B(q^{-1})}{F(q^{-1})A(q^{-1})} y_r(k+d) + \frac{1}{A(q^{-1})} v(k)}
{1 + \frac{q^{-d}B(q^{-1})G(q^{-1})}{A(q^{-1})F(q^{-1})}}
\\
&= \frac{q^{-d}R(q^{-1})B(q^{-1})y_r(k+d) + F(q^{-1})v(k)}
{A(q^{-1})F(q^{-1}) + q^{-d}B(q^{-1})G(q^{-1})}
\tag{6.4.3}
\end{align}
$$

他的闭环特征式，用丢番图方程可以表示为：

$$
A(q^{-1})F(q^{-1}) + q^{-d}B(q^{-1})G(q^{-1}) = T(q^{-1}) \tag{6.4.4}
$$

>接下来，为了方便起见，我将输出的表达式写为：
$$
y(k) = \frac{q^{-d}RB}{AF + q^{-d}BG}y_r(k+d) + \frac{F}{AF + q^{-d}BG}v(k)
\tag{6.4.3*}
$$

控制器的设计思路是，让参考输入到输出的闭环传递函数等于我们所期望的传递函数，从而确定F，G，R的值。换句话说，我们希望能够找到稳定的极点配置，使得下面这个传递函数稳定：
$$
\frac{y(k)}{y_r(k+d)}=\frac{q^{-d}RB}{AF + q^{-d}BG}=\frac{q^{-d}B_m}{A_m}
$$

它的特征方程是：
$$
A(q^{-1})F(q^{-1})+q^{-d}B(q^{-1})G(q^{-1})=T(q^{-1})
$$
f,g是原系统的丢番图方程的解。这种方法是课件所提供的，如果期末考试考到的话，给出的条件应该是往推到这个方程上靠的。
$$
\begin{bmatrix}
    a_0 & 0 & \cdots & 0 & b_0 & 0 & \cdots & 0 \\
    a_1 & a_0 & \cdots & 0 & b_1 & b_0 & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots & \vdots & \vdots & \ddots & \vdots \\
    a_{n_a} & \vdots & \ddots & a_1 & b_{n_b} & \vdots & \ddots & b_1 \\
    0 & a_{n_a} & \cdots & \vdots & 0 & b_{n_b} & \cdots & b_2 \\
    \vdots & \vdots & \ddots & a_{n_a} & \vdots & \vdots & \ddots & 0 \\
    0 & \cdots & 0 & a_{n_a} & 0 & \cdots & 0 & b_{n_b} \\
\end{bmatrix}
\begin{bmatrix}
    f_0 \\ f_1 \\ \vdots \\ f_{n_t} \\ g_0 \\ g_1 \\ \vdots \\ g_{n_g}
\end{bmatrix}
=
\begin{bmatrix}
    t_0 \\ t_1 \\ \vdots \\ t_{n_t} \\ 0 \\ 0 \\ \vdots \\ 0
\end{bmatrix}
$$



## 总结

背公式吧~~这一部分可能由这几个地方需要注意：


# 自校正PID控制

## PID控制

在自动控制原理中，我们学过，PID控制器的基本结构为：
$$
u(k)=K_pe(k)+\sum^k K_ie(i)+K_d\left(e(k)-e(k-1)\right)
$$
因此，两次PID输出的差距为：
$$
\begin{aligned}
\Delta u(k)&=u(k)-u(k-1)\\
&=K_p\left(e(k)-e(k-1)\right)+K_ie(k)+K_d\left(e(k)-2e(k-1)+e(k-2)\right)
\end{aligned}
$$
进行整理可以得到：
$$
\begin{aligned}
\Delta u(k)
&=K_p\left(e(k)-e(k-1)\right)+K_ie(k)+K_d\left(e(k)-2e(k-1)+e(k-2)\right)\\
&=(K_p+K_i)e(k)+(-K_p-2K_d)e(k-1)+K_de(k-2)\\
&=g_0e(k)+g_1e(k-1)+g_2e(k-2)
\end{aligned}
$$

> $\Delta$算子：该运算符计算某变量的变化值，在时间序列上它可以写作$\Delta=1-q^{-1}$
> $$
> \Delta u(k)=u(k)-u(k-1)=(1-q^{-1})u(k)
> $$

最终我们可以得到：
$$
\begin{aligned}
(1-q^{-1})u(k)&=\left(g_0+g_1q^{-1}+g_2q^{-2}\right)e(k)\\
\frac{u(k)}{e(k)}&=\frac{g_0+g_1q^{-1}+g_2q^{-2}}{1-q^{-1}}
\end{aligned}
$$
假设参考输出为$y_r$，真实输出为$y$，延迟为$d$，上式改写成：
$$
\begin{aligned}
(1-q^{-1})u(k)&=\left(g_0+g_1q^{-1}+g_2q^{-2}\right)\left(y_r(k+d)-y(k)\right)\\
F(q^{-1})u(k)&=R(q^{-1})y_r(k+d)-G(q^{-1})y(k)\\
F(q^{-1})&=1-q^{-1}\\
R(q^{-1})=G(q^{-1})&=g_0+g_1q^{-1}+g_2q^{-2}
\end{aligned}
$$
上述即为PID控制器下的模型。因此，PID自校正控制便期望得到更好的$g_0,g_1,g_2$参数。

## 自校正PID控制器的原理

对于某个系统：
$$
A(q^{-1})y(k)=q^{-d}B(q^{-1})u(k)+\xi(k)
$$
上文我们推导出，PID控制器的控制输出、参考输入和真实输出的关系是：

$$
\begin{aligned}
F(q^{-1})u(k)&=R(q^{-1})y_r(k+d)-G(q^{-1})y(k)\\
F(q^{-1})&=1-q^{-1}\\
R(q^{-1})=G(q^{-1})&=g_0+g_1q^{-1}+g_2q^{-2}
\end{aligned}
$$
我们整合这两个式子，可以解算出：
$$
\begin{aligned}
u(k)&=\frac{R(q^{-1})y_r(k+d)-G(q^{-1})y(k)}{F(q^{-1})}\\
A(q^{-1})y(k)&=\left(q^{-d}B(q^{-1})u(k)+\xi(k)\right)\\
&=\left(q^{-d}B(q^{-1})\frac{R(q^{-1})y_r(k+d)-G(q^{-1})y(k)}{F(q^{-1})}+\xi(k)\right)\\
\left(A(q^{-1})+\frac{q^{-d}B(q^{-d})G(q^{-d})}{F(q^{-1})}\right)y(k)&=\left(q^{-d}B(q^{-1})\frac{R(q^{-1})y_r(k+d)}{F(q^{-1})}+\xi(k)\right)\\

y(k)&=\frac{F(q^{-1})}{A(q^{-1})F(q^{-1})+q^{-d}B(q^{-d})G(q^{-d})}\left(q^{-d}B(q^{-1})\frac{R(q^{-1})y_r(k+d)}{F(q^{-1})}+\xi(k)\right)

\end{aligned}
$$
注意到，

$$
\begin{aligned}
q^{-d}B(q^{-1}){R(q^{-1})y_r(k+d)} &= B(q^{-1})R(q^{-1})q^{-d}y_r(k+d)\\&=B(q^{-1})R(q^{-1})y_r(k)
\end{aligned}
$$
, 因此：
$$
y(k)=\frac{B(q^{-1})R(q^{-1})y_r(k)+F(q^{-1}\xi(k))}{A(q^{-1})F(q^{-1})+q^{-d}B(q^{-d})G(q^{-d})}
$$
我们令
$$
A(q^{-1})F(q^{-1})+q^{-d}B(q^{-d})G(q^{-d})=A_m(q^{-1})
$$
就可以用上一部分我们提到的极点配置法来进行设计了。



# 广义预测控制（GPC）

## j-step最优预测

对于系统：
$$
A(q^{-1})y(k)=q^{-1}B(q^{-1})u(k)+\frac{C(q^{-1})}{\Delta}\xi(k)
$$
* **定理 6.6.1 （CARIMA模型的j步最优预测）**

对于受控对象（6.6.1），假设在时间 \( k + j \) 的输出预测误差为：

$$
\tilde{y}(k + j|k) = y(k + j) - \hat{y}(k + j|k)
$$

我们定义预测误差的方差为：

$$
J(k) = \mathbb{E}\{\tilde{y}^2(k + j|k)\}
$$

我们希望将其最小化。

* 根据前k步的结果，预测k+j步的输出

参考我们在第一章中的模型，**j步最优预测** $ y^*(k + j|k) $可由以下差分方程给出：
$$
C(q^{-1})y^*(k + j|k) = G_j(q^{-1})y(k) + F_j(q^{-1})\Delta u(k) \tag{6.6.4}
$$

其中，$F_j(q^{-1}) $ 和 $ G_j(q^{-1}) $ 满足以下丢番图方程：

$$
C(q^{-1}) = A(q^{-1})E_j(q^{-1}) + q^{-j}G_j(q^{-1}) \quad
F_j(q^{-1}) = B(q^{-1})E_j(q^{-1}) \tag{6.6.5}
$$

其中：

$$
\begin{aligned}
F_j(q^{-1}) &= f_{j,0} + f_{j,1}q^{-1} + \dots + f_{j,n_{fj}}q^{-n_{fj}} \quad (n_{fj} = n_b + j - 1)\\
G_j(q^{-1}) &= g_{j,0} + g_{j,1}q^{-1} + \dots + g_{j,n_{gj}}q^{-n_{gj}} \quad (n_{gj} = n_a - 1)\\
E_j(q^{-1}) &= 1 + e_{j,1}q^{-1} + \dots + e_{j,n_{ej}}q^{-n_{ej}} \quad (n_{ej} = j - 1)
\end{aligned}
$$

* 第k+j步的实际输出的计算

参考我们在本章第一节所学的方式，我们解开$\bar A(q^{-1})y(k)=B(q^{-1})\Delta u(k-1)+C(q^{-1})\xi(k)$的丢番图方程后（同上），可以得到：
$$
y(k+j)=E_j(q^{-1})\xi(k+j)+\frac{B(q^{-1})}{\bar A(q^{-1})}\Delta u(k+j-1)+\frac{G_j(q^{-1})}{\bar A(q^{-1})}\xi(k)
$$

而我们知道：
$$
\xi(k)=\frac{\bar A(q^{-1})}{C(q^{-1})}y(k)-\frac{B(q^{-1})}{C(q^{-1})}\Delta u(k-1)
$$
且由公式6.6.5可知：
$$
C(q^{-1})-q^{-j}G_j(q^{-1})=A(q^{-1})E_j(q^{-1})
$$


因此：
$$
\begin{aligned}
y(k+j)&=E_j(q^{-1})\xi(k+j)+\frac{B(q^{-1})}{\bar A(q^{-1})}\Delta u(k+j-1)+\frac{G_j(q^{-1})}{\bar A(q^{-1})}\xi(k)
\\
&=E_j(q^{-1})\xi(k+j)+\frac{B(q^{-1})}{\bar A(q^{-1})}\Delta u(k+j-1)+\frac{G_j(q^{-1})}{\bar A(q^{-1})}\frac{A(q^{-1})}{C(q^{-1})}y(k)-\frac{G_j(q^{-1})}{\bar A(q^{-1})}\frac{B(q^{-1})}{C(q^{-1})}\Delta u(k-1)
\\
&=E_j(q^{-1})\xi(k+j)+\frac{G_j(q^{-1})}{C(q^{-1})}y(k)+\frac{B(q^{-1})}{\bar A(q^{-1})C(q^{-1})}\left(C(q^{-1})\Delta u(k+j-1)-G(q^{-1})q^{-j}\Delta u(k+j-1)\right)
\\
&=E_j(q^{-1})\xi(k+j)+\frac{G_j(q^{-1})}{C(q^{-1})}y(k)+\frac{B(q^{-1})\left[C(q^{-1})-q^{-j}G_j(q^{-1})\right]}{\bar A(q^{-1})C(q^{-1})}\Delta u(k+j-1)
\\
&=E_j(q^{-1})\xi(k+j)+\frac{G_j(q^{-1})}{C(q^{-1})}y(k)+\frac{B(q^{-1})A(q^{-1}E_j(q^{-1}))}{\bar A(q^{-1})C(q^{-1})}\Delta u(k+j-1)
\\
&=E_j(q^{-1})\xi(k+j)+\frac{G_j(q^{-1})}{C(q^{-1})}y(k)+\frac{F_j(q^{-1}))}{C(q^{-1})}\Delta u(k+j-1)
\end{aligned}
$$

将它们代入代价函数 $ J(k) $中，得到：

$$
\begin{aligned}
J(k) &= \mathbb{E}\{(y(k + j) - \hat{y}(k + j|k))^2\}
\\
&= \mathbb{E} \left\{ \left( E_j(q^{-1})\xi(k + j) + \frac{F_j(q^{-1})}{C(q^{-1})}\Delta u(k + j - 1) + \frac{G_j(q^{-1})}{C(q^{-1})}y(k) - \hat{y}(k + j|k) \right)^2 \right\}\\

&= \mathbb{E} \left\{ \left( E_j(q^{-1})\xi(k + j) \right)^2 \right\} + \mathbb{E} \left\{ \left( \frac{F_j(q^{-1})}{C(q^{-1})}\Delta u(k + j - 1) + \frac{G_j(q^{-1})}{C(q^{-1})}y(k) - \hat{y}(k + j|k) \right)^2 \right\}
\end{aligned}
$$

为了使 $J(k) $ 最小化，$ \hat{y}(k + j|k) $ 应满足以下条件：

$$
\hat{y}(k + j|k) = \frac{F_j(q^{-1})}{C(q^{-1})}\Delta u(k + j - 1) + \frac{G_j(q^{-1})}{C(q^{-1})}y(k) = y^*(k + j|k)
$$

即方程 (6.6.4) 成立，并且此时：

$$
J_{\text{min}} = \mathbb{E} \left\{ \left( E_j(q^{-1})\xi(k + j) \right)^2 \right\}
$$

最优预测误差为：
$$
\tilde{y}^*(k + j|k) = E_j(q^{-1})\xi(k + j)
$$

我4了，这个证明太抽象了，就这样吧（）
