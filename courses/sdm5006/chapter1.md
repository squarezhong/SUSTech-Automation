<p align='center'><font size=7><b>系统辨识基础</b></font></p>

# 系统辨识的概念

系统辨识包含以下的三个内容。

* 模型：

模型有以下几类：Intuitionistic model, Chart model, Physical model, Mathematical model etc.

**建模方法**：

Theoretical analysis method

practical test method

hybrid method

## 系统的性质

* 确定性和随机性

看有没有不确定项。比如：
$$
\begin{aligned}
y(k+1)&=ay(k)+bu(k)\\
y(k+1)&=ay(k)+bu(k)+\xi(k)
\end{aligned}
$$
$\xi(k)$是随机噪声。这两个式子可以发现，上一行我们可以根据a和b的值来酸楚确定的输出，体现了**确定性**；而下一行的式子由于随机噪声的存在，无法算出准确的输出，更不能逐级递推往后算出更远的输出，体现了**随机性**。

* 模型和时间的关系：静态和动态

静态系统：**所有state对时间的导数为0**，例如$ y(k)=au(k)$

动态系统：**所有state对时间的导数不全为0**（导数值大小可以随时间变化），例如$ y(k+1)=ay(k)+bu(k) $，因为$\dot y = \frac{y(k+1)-y(k)}{dt}\neq0~for~a\neq0 $

* Time scale: 连续模型和离散模型

略。

* 参数和时间的关系：时变性和时不变性

$$
\begin{aligned}
y(k+1)&=ay(k)+bu(k)\\
y(k+1)&=a(k)y(k)+b(k)u(k)
\end{aligned}
$$

当参数a，b为常数的时候，为时不变系统（第一行）；如果a，b中至少有一个是和时间有关的参数，则为时变系统（第二行）。

* 参数和输入输出的关系：线性和非线性

线性模型：同时满足叠加性和齐次性。例如：
$$
y(k+1)=ay(k-1)+bu(k)
$$
非线形模型：不满足叠加性或齐次性。例如：
$$
\dot y(t)=ay(t)+by(t)u(t)
$$

> 叠加性：$ f(a+b)=f(a)+f(b) $; 齐次性：$ f(ak)=af(k) $
>
> 对于第一个系统：假设k时刻，状态和输入$y_1(k-1),u_1(k),y_2(k-1),u_2(k)$分别得到$y_1(k+1),y_2(k+1)$
$$
\begin{aligned}
y_1(k+1) &= a y_1(k-1) + b u_1(k)\\
y_2(k+1) &= a y_2(k-1) + b u_2(k)\\
\end{aligned}
$$
> 当$y(k-1)=y_1(k-1)+y_2(k-1),~u(k)=u_1(k)+u_2(k)$时，假设得到$y(k+1)$：
$$
\begin{aligned}
y(k+1)&=ay(k-1)+bu(k)\\
&=a y_1(k-1) + b u_1(k)+a y_2(k-1) + b u_2(k)
\end{aligned}
$$
> 叠加性证毕；
>
> 齐次性证明：假设状态和输入为$y_1(k-1),~u_1(k)$和$\lambda y_1(k-1),~\lambda u_1(k)$
$$
\begin{aligned}
y_1(k+1)&=ay_1(k-1)+bu(k)\\
y(k+1)&=\lambda ay_1(k-1)+\lambda bu_1(k)\\
&=\lambda y_1(k+1)
\end{aligned}
$$
> 齐次性证毕。
>
> 对于第二个系统，假设状态和输入分别为$y_1(t),u_1(t)$ $和 y_2(t),u_2(t) $叠加性：
$$
\begin{aligned}
\dot y_1(t)&=ay_1(t)+by_1(t)u_1(t)\\
\dot y_2(t)&=ay_2(t)+by_2(t)u_2(t)\\
\dot y(t)&=a\left[y_1(t)+y_2(t)\right]+b\left[y_1(t)+y_2(t)\right]\left[u_1(t)+u_2(t)\right]\\
&=y_1(t)+y_2(t)+by_1(t)u_2(t)+by_2(t)u_1(t)\\
&\neq y_1(t)+y_2(t)
\end{aligned}
$$
> 不满足叠加性，它不是一个线性系统。
>
> 同样，让我们来看看齐次性：
$$
\begin{aligned}
y_1(t)&=ay_1(t)+by_1(t)u_1(t)\\
y(t)&=a\lambda y_1(t)+b\lambda y_1(t)\lambda u_1(t)\\
&\neq\lambda y_1(t)
\end{aligned}
$$
> 不满足齐次性，因此也不是一个线性系统。

* 模型的表达式：参数模型（parametric）和非参数模型（non-parametric）

**非参数模型**：通过实验过程中实际系统的响应（直接或间接地）建立的，比如：

阶跃响应

脉冲响应

频率响应

例如：
$$
y(k)=(\sum_{i=0}^{\infty}g(i)q^{-1})u(k)
$$
其中，$g(i)$是单位脉冲序列。

**参数模型**：通过逻辑推导方法建立的模型称。它有固定的数学形式，参数数量通常较少。例如：
$$
y(k+1)=ay(k)+bu(k)
$$

* 参数性质：集中参数系统（centralized parameters）和分布参数系统（distributed parameters）

集中参数系统：系统的状态参数仅仅是时间的函数。例如$\dot y(t)=ay(t)+bu(t)$

分部参数系统：系统状态参数不只是时间的函数。例如$ \dot y(t)=\frac{\partial y(t)}{\partial u(t)}y(t)+bu(t)$

* 输入和输出的数量。

单输入单输出SISO，多输入单输出MISO，单输入多输出SIMO，多输入多输出MIMO。



## 系统辨识的分类

* 实验方法分类：白盒，灰盒，黑盒

对于系统的结构，组成，控制律等，

白盒：全部清楚

黑盒：全部不清楚

灰盒：部分清楚

* 辨识方式：在线辨识、离线辨识

* 系统辨识手段：开环辨识盒闭环辨识



## 一种系统辨识方法——两点辨识法

对于某个**一阶系统**，可以使用**阶跃函数**采用**两点辨识法**对齐进行系统辨识。

某一阶系统的传递函数为$G(s)=\frac{K}{Ts+1}e^{-\tau s}$。它包含了三个需要被辨识的参数：增益K，时间常数T和延迟$\tau$。

我们学过，频域到时域可以使用反拉普拉斯变换。我们使用单位阶跃函数来对其进行系统辨识：
$$
Y(s)=G(s)U(s)=G(s)\cdot\frac{1}{s}
$$
转到时域：
$$
\begin{aligned}
y(t)&=L^{-1}\left[\frac{Ke^{-\tau s}}{Ts+1}\cdot\frac1s\right]\\
&=L^{-1}\left[(\frac{1}{s}-\frac{T}{Ts+1})Ke^{-\tau s}\right]\\
&=K(1-e^{\frac{\tau-t}{T}})
\end{aligned}
$$

* 得到K：显然，当时间趋于无穷的时候，
  $$
  \lim_{t\rightarrow\infty}y(t)=K
  $$
  因此，K的大小为无穷时间处的输出值；

* 得到T和$ \tau $：选取两个时刻$t_1,t_2$，获得这两个时刻的输出，建立方程：

$$
\begin{aligned}
y(t_1)=K(1-e^{\frac{\tau-t_1}{T}})\\
y(t_2)=K(1-e^{\frac{\tau-t_2}{T}})
\end{aligned}
$$

解开即可。

> 解方程：
$$
\begin{aligned}
\frac{y(t_1)}{K}&=1-e^{\frac{\tau-t_1}{T}}\\
1-\frac{y(t_1)}{K}&=e^{\frac{\tau-t_1}{T}}\\
\rightarrow\ln\left(\frac{K-y(t_1)}{K}\right)&=\frac{\tau-t_1}{T}
\end{aligned}
$$
> 同理，对$t_2$时刻的方程也进行车养的处理，然后解开两个方程的两个未知数即可。

### 示例——以某水位控制系统为例

对于某个水位控制系统，其基本的传递函数为$G(s)=\frac{K}{Ts+1}e^{-\tau s}$。它包含了三个需要被辨识的参数：增益K，时间常数T和延迟$\tau$。

![2p_identification](imgs/c1-2p_identification.svg)

现在，在$ t=0 $时刻给这个系统施加一个单位阶跃响应$ u(t) $，同时测出以下数据：

* $t_1=2s,~y(t_1)=1.95$
* $t_2=3s,~y(t_2)=3.16$

显然，观察图像我们发现，t趋于无穷的时候，值为5，因此K等于5。

然后带入方程可以解算出$T=2,\tau=1$。最终得到系统的传递函数为
$$
G(s)=\frac{5}{2s+1}e^{-s}
$$




## 线性时不变系统

满足线性和叠加性的系统。

线性：满足叠加性和齐次性，在上文已有证明的阐述；

时不变性：系统的参数不会随着时间改变。其数学表达为，**如果$y(t)=T[u(t)]$，那么$ y(t-t_0)=T[u(t-t_0)] $**。比如我们假设系统是$y(t)=a(t)u(t)$。$ a(t) $是随时间变化的参数。在$ t,t+\delta t $的时候，输出分别是：
$$
\begin{aligned}
y(t)&=a(t)u(t)\\
y(t+\delta t)&=a(t+\delta t)u(t+\delta t)
\end{aligned}
$$
对于第二行的式子，我们把$u(t+\delta t-\delta t)$带入：
$$
\begin{aligned}
y(t+\delta t-\delta t)&=a(t+\delta t)u(t+\delta t-\delta t)\\
&=a(t+\delta t)u(t)\\
&\neq y(t)
\end{aligned}
$$
可以注意到，当a是随时间变化的参数的时候，不满足时不变系统的定义；倘若a是一个常数，那么$a(t)=a(t+\delta t)$，那么这个系统才会是一个时不变系统。

### 干扰

干扰分为测量误差（比如噪声、漂移）和不受控制的输入（比如气温变化）

### 传递函数-时间移动（drift）

把q作为移动因子。
$$
\begin{aligned}
q^{-1}y(t)&=y(t-1)\\
(1.8q^2+1.2-0.5q^{-1})&=1.8y(t+2)+1.2y(t)-0.5y(t-1)
\end{aligned}
$$



# 系统辨识的几种方法

均对于离散化的系统。

## 脉冲响应法（Impulse Response）

对于系统：
$$
y(k)=G(q^{-1})u(k)\\
G(q^{-1})=\sum_{i=1}^{\infty}g(i)q^{-1}
$$
输入脉冲，即只有$ u(0)=1 $，其它时候均为0.因此，对于上面的系统：
$$
\begin{aligned}
y(k)&=\sum_{i=1}^{\infty}g(i)q^{-1}\\
&=\sum_{i=1}^{\infty}g(i)u(k-i)\\
&=g(k)
\end{aligned}
$$
从而辨识出g。

## 阶跃响应法（Step Response）

$$
\begin{aligned}
\Delta u(k)&=u(k)-u(k-1)\\
&=(1-q^{-1})u(k)\\\rightarrow
u(k)&=\frac{\Delta u(k)}{1-q^{-1}}\\\rightarrow
y(k)&=\frac{G(q^{-1})}{1-q^{-1}}\Delta u(k)
\end{aligned}
$$

让传递函数变为：
$$
\widetilde G(q^{-1})=\frac{G(q^{-1})}{1-q^{-1}}
$$
惊讶地发现，$\Delta u(t)$只有在t=0的时候是1，其它时候都是0，也就是说，接下来的步骤和阶跃响应的系统辨识类似。
$$
\begin{aligned}
\widetilde g_i(k)&=y(k)\\
G(q^{-1})=(1-q^{-1})\widetilde G(q^{-1})
\end{aligned}
$$

> 噪声影响：如果考虑噪声带来的影响，例如$v(k)=H(q^{-1})e(k)$，系统将被写作：
$$
y(k)=G(q^{-1})u(k)+H(q^{-1})e(k)
$$

# 系统的稳定性

如果一个系统的传递函数满足：
$$
G(q^{-1})=\sum_{k=1}^{\infty}g(k)q^{-k},~\sum_{k=1}^{\infty}|g(k)q^{-k}|<\infty
$$
那么这个系统将会是**有界输入-有界输出的稳定**（bounded input bounded output stability，BIBO stable）。

**稳定：**传递函数的极点在单位圆内；

**不稳定：**传递函数的极点在单位圆外；

**临界稳定：**至少有一个传递函数的极点在单位圆上，且其它极点均在单位圆内。

# 线性时不变模型

* Auto-regressive moving average model with control  - ARMAX （也叫CARMA）

$$
A(q^{-1})y(k)=B(q^{-1})u(k)+D(q^{-1})\xi(k)
$$

* Auto-regressive model with control - ARX （CAR）

$$
A(q^{-1})y(k)=B(q^{-1})u(k)+\xi(k)
$$

* Auto-regressive moving average - ARMA

$$
A(q^{-1})y(k)=D(q^{-1})\xi(k)
$$

* Auto-regressive - AR

$$
A(q^{-1})y(k)=\xi(k)
$$

* Moving average - MA

$$
y(k)=D(q^{-1})\xi(k)
$$

* Box-Jenkins model - BJ

$$
y(k)=\frac{B(z^{-1})}{F(z^{-1})}u(k)+\frac{C(z^{-1})}{D(z^{-1})}\xi(k)
$$

注意，$ \xi(k) $是**白噪声**。相信聪明的你已经总结出了：

* Auto-regression（AR）：$ A(q^{-1})y(k) $
* Moving-average （MA）: $D(q^{-1})\xi(k)$
* Control（C or X）：$B(q^{-1})u(k)$

且系统中必须考有y和噪声$\xi$。然后排列组合吧。不过似乎不止上面这几种（）比如ppt part2中第25小页13大页中的Self Assessment Question，似乎是只包含control和moving average的项，是个CMA（MAX）模型。



# 单步预测

## 不考虑误差的单步预测

对于：
$$
y(k)=G(q^{-1})u(k)+H(q^{-1})e(k)
$$
其中，$e(k)$为白噪声（建模过程中通常考虑将白噪声经过一个传递函数后变成一个有色噪声）。显然，不考虑误差的话，在仅知道第k时刻和之前的输入u、k-1时刻及之前的测量误差e的时候，由于我们不知道第k时刻的测量误差，因此，如果我们不考虑误差带来的影响：
$$
\hat y(k|k-1)=G(q^{-1})u(k)
$$
## 考虑误差的单步估计

方便起见，我们假设$ v(k)= H(q^{-1})e(k) $。显然，真的输出和预测输出之前的差是：
$$
y(k)-\hat y(k|k-1)=v(k)
$$
我们并不知道$ v(k) $，但是我们知道k-1时刻之前的测量误差，它们将等于：
$$
v(k-i)=y(k-i)-G(q^{-1})u(k-i),i=1,2,3,...
$$
值的注意的是，在对误差项进行建模的时候，我们通常将$ H(q^{-1})$的第一项设为1，即$ H(q^{-1})=1+h(1)q^{-1}+... $。因此，可以将$ v(k) $表示为：
$$
v(k)=\sum_{i=0}^{\infty}h(i)e(k-i)=e(k)+\sum_{i=1}^{\infty}h(i)e(k-i)
$$

* 误差项的最优估计

方便起见，我们令$ m(k-1)=\sum_{i=1}^{\infty}h(i)e(k-i) $。在上面的式子中，除了$ e(k) $之外，都是已知量。如果我们希望误差最小，即$ \min [(v(k)-\hat v(k)]^2$，由于$ v(k) $不可知，我们可以最小化其期望$ E\left[\left(v(k)-\hat v(k)\right)^2\right] $：
$$
\begin{aligned}
\left(v(k)-\hat v(k)\right)^2&=\left(e(k)+m(k-1)-\hat v(k)\right)^2\\
&= e^2(k) + \left(m(k-1)-\hat v(k)\right)^2+2e(k)\left(m(k-1)-\hat v(k)\right)\\
E\left[\left(v(k)-\hat v(k)\right)^2\right]&=E[e(k)^2]+E\left[\left(m(k-1)-\hat v(k)\right)^2\right]+E\left[2e(k)\left(m(k-1)-\hat v(k)\right)\right]
\end{aligned}
$$
由于$ e(k) $是白噪声，均值为0，因此上式第三项可以表示为：
$$
\begin{aligned}
E\left[2e(k)\left(m(k-1)-\hat v(k)\right)\right]&=
2E[e(k)]\cdot E[m(k-1)\hat v(k)]\\
&=0\\\rightarrow
E\left[\left(v(k)-\hat v(k)\right)^2\right]&=E[e(k)^2]+E\left[\left(m(k-1)-\hat v(k)\right)^2\right]
\end{aligned}
$$
 由于$ e(k) $我们无法操作，因此我们只能最小化$ E\left[\left(m(k-1)-\hat v(k)\right)^2\right] $, 显然，预测误差取$ \hat v(k) = m(k-1)$的时候，是最可能接近真实误差的。

> 注意，为了方便起见，课件中有时候用$\hat v(k|k-1)$表示的测量误差，在本文中均用$ \hat v(k) $表示。

* 预测误差$ \hat v(k) $和真实误差$ v(k) $的误差

由于$ v(k)=H(q^{-1})e(k) $:
$$
\begin{aligned}
\hat v(k)&=\sum_{i=1}^{\infty}h(i)q^{-i}e(k)\\
&=[H(q^{-1})-1]e(k)\\
&=[H(q^{-1})-1]\frac{v(k)}{H(q^{-1})}\\
&=[1-H^{-1}(q^{-1})]v(k)
\end{aligned}
$$

* 重新整理单步预测-单步预测和真实输出的关系

真实输出下，误差项是$ v(k)=y(k)-G(q^{-1})u(k) $，因此：
$$
\begin{aligned}
\hat y(k|k-1)&=G(q^{-1})u(k)+\hat v(k)\\
&=G(q^{-1})u(k)+[1-H^{-1}(q^{-1})]v(k)\\
&=G(q^{-1})u(k)+[1-H^{-1}(q^{-1})]\left[\left(y(k)-G(q^{-1})u(k)\right)\right]\\
&=H^{-1}(q^{-1})G(q^{-1})u(k)+[1-H^{-1}(q^{-1})]y(k)
\end{aligned}
$$
同样，我们可以计算出：
$$
\begin{aligned}
y(k)-\hat y(k|k-1)&=y(k)-\left\{H^{-1}(q^{-1})G(q^{-1})u(k)+[1-H^{-1}(q^{-1})]y(k)\right\}\\
&=H^{-1}(q^{-1})y(k)-H^{-1}(q^{-1})G(q^{-1})u(k)\\
&=H^{-1}(q^{-1})\left[y(k)-G(q^{-1})u(k)\right]\\
&=H^{-1}(q^{-1})v(k)
\end{aligned}
$$

# 噪声和伪随机数

## 白噪声

白噪声是一种均值为0，方差为$ \sigma^2 $的**高斯噪声**。

* 白噪声序列的性质：

自相关性：仅在0处自相关函数不为0: $ R_\xi(k)=\sigma^2\delta(k) $

* 有色噪声：白噪声经过一个transfer function，即$G(q^{-1})\xi(k)$

## M序列

### M序列的性质

* 周期：寄存器数量（即为阶数）n，则该M序列周期为$N=2^n-1$. （课件原文：n级移位寄存器可能形成的PRBS的最大长度为: $N=2^n-1$）

* 游程（run）：序列中连续相同的元素的个数。每个周期内，长度为k的游程占$\frac1{2^k}$. 一个周期内，游程总数量为$\frac{N+1}2$(N表示周期)

* 自相关性：
  $$
  R_x(\tau)=\begin{cases}
  a^2\left(1-\frac{N+1}N\frac{|\tau|}{\Delta}\right),~-\Delta<\tau<\Delta\\
  -\frac{a^2}{N},\Delta<\tau<(N-1)\Delta
  \end{cases}
  $$
  

### M序列的计算更新方法

假设又这样一个结构的寄存器……好吧，寄存器可能有些抽象，假设有下图这样的系统：

![msequence](imgs/c1-msequence.svg)

限定$A_i,c_i$的值只能为1和0，其中$c_i$为0代表其对应的$A_i$不加入异或运算。对于这个系统，从时刻的更新公式为：
$$
\begin{aligned}
A_4(k+1)&=A_3(k)\\
A_3(k+1)&=A_2(k)\\
A_2(k+1)&=A_1(k)\\
A_1(k+1)&= A_1(k)c_1\oplus A_2(k)c_2 \oplus A_3(k)c_3\oplus A_4(k)c_4\\
\end{aligned}
$$
这个系统中，$ A_4$ 为输出，即$ y(k)=A_4(k) $。这样得到的输出序列称为m序列。上图中出现的的数量是m序列的阶数。注意到，如果希望得到m序列，则需要给出$c_i$ 和每个状态的初始值$A_i(0)$。

> 异或运算：对于两个输入信号（值只能是1或者0），若不同，则输出1；若相同，则输出0。即：
$$
\begin{aligned}
1\oplus1=0,&0\oplus0=0\\
1\oplus0=1,&0\oplus1=1
\end{aligned}
$$
> 观察可以发现，**0与任何输入异或，都保持该输入的值**，即：$0\oplus X=X$。

* 例题（chapter1-part3 第17-18小页第9大页）：设某个四阶m序列，$A_i(0)=1,c_1=c_2=0,c_3=c_4=1$，试着计算他们的输出。课件提供[example162.m](../../matcodes/cpt1/example162.m)为参考。

尽管我相信，由于上文提到c=0的时候，对应的状态不参与异或运算，聪明的你一定算出来了$A_1(k+1)=A_3(k)\oplus A_4(k)$，但是我仍然希望一步一步从数学上阐释为什么c=0的时候可以不参与计算。上文提到，$0\oplus X=X$，因此我们可以得出，
$$
\begin{aligned}
A_1(k+1)&=A_1(k)c_1\oplus A_2(k)c_2 \oplus A_3(k)c_3\oplus A_4(k)c_4\\
&=0\oplus 0 \oplus A_3(k)\oplus A_4(k)\\
&=A_3(k)\oplus A_4(k)
\end{aligned}
$$

因此，它的输出将会是：

| Time $k$ | $A_1(k)$ | $A_2(k)$ | $A_3(k)$ | $y(k)=A_4(k)$ | $A_1(k+1)$ |
| :------: | :------: | :------: | :------: | :------: | :--------: |
|    0     |    1     |    1     |    1     |    1     |     0      |
|    1     |    0     |    1     |    1     |    1     |     0      |
| 2 | 0 | 0 | 1 | 1 |     0      |
| 3 | 0 | 0 | 0 | 1 |     1      |
| 4 | 1 | 0 | 0 | 0 |     0      |
| 5 | 0 | 1 | 0 | 0 |     0      |
| 6 | 0 | 0 | 1 | 0 |     1      |
| 7 | 1 | 0 | 0 | 1 |     1      |
| 8 | 1 | 1 | 0 | 0 |     0      |
| 9 | 0 | 1 | 1 | 0 |     1      |
| 10 | 1 | 0 | 1 | 1 |     0      |
| 11 | 0 | 1 | 0 | 1 |     1      |
| 12 | 1 | 0 | 1 | 0 |     1      |
| 13 | 1 | 1 | 0 | 1 |     1      |
| 14 | 1 | 1 | 1 | 0 |     1      |
|15|1|1|1|1|0|

因此，一个周期下（k从0到14），输出为：111100010011010。

# Quiz

1. Why we need to simulate a system before establishing a real one?

<details>
    <summary>Answer:</summary>
    <p>
        1. The <b>cost</b> of experimenting with an actual system may be too high.<br>
        2. The system may be <b>unstable</b> during the experiment, which leads to certain dangers in the experiment process.<br>
        3. The <b>time</b> constant of the system may be very large, so that the experiment period is too long.
    </p>
</details>

2. What are the steps of system identification?

<details>
    <summary>Answer</summary><p>
    1. Obtain prior information on a system<br>
    2. Design an experiment<br>
    3. Collect data<br>
    4. Choose the model structure<br>
    5. Determine the parameters<br>
    6. Validate the model<br>
    7. Accept the model</p>
    <p>Here is a block diagram.<br>
    <img src='/doc/SDM5006/imgs/c1-q2-si-block.png' data-origin='imgs/c1-q2-si-block.png' alt=''c1-q2-si-block class="medium-zoom-image">
    </p>
</details>

3. Is $G(q^{-1})=\frac{q^{-1}-1.2}{q^{-2}+0.1q^{-1}-0.06}$a stable system?

<details>
    <summary>Answer</summary>
    <div contenteditable="false" spellcheck="false" class="mathjax-block md-end-block md-math-block md-rawblock md-rawblock-on-edit md-focus" id="mathjax-n0" cid="n0" mdtype="math_block" data-math-tag-before="0" data-math-labels="[]" data-math-tag-after="0"><div class="md-math-container"><mjx-container class="MathJax" jax="SVG" display="true" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="41.33ex" height="18.062ex" role="img" focusable="false" viewBox="0 -4241.8 18267.9 7983.6" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -8.466ex;"><defs><path id="MJX-115-TEX-I-1D43A" d="M50 252Q50 367 117 473T286 641T490 704Q580 704 633 653Q642 643 648 636T656 626L657 623Q660 623 684 649Q691 655 699 663T715 679T725 690L740 705H746Q760 705 760 698Q760 694 728 561Q692 422 692 421Q690 416 687 415T669 413H653Q647 419 647 422Q647 423 648 429T650 449T651 481Q651 552 619 605T510 659Q492 659 471 656T418 643T357 615T294 567T236 496T189 394T158 260Q156 242 156 221Q156 173 170 136T206 79T256 45T308 28T353 24Q407 24 452 47T514 106Q517 114 529 161T541 214Q541 222 528 224T468 227H431Q425 233 425 235T427 254Q431 267 437 273H454Q494 271 594 271Q634 271 659 271T695 272T707 272Q721 272 721 263Q721 261 719 249Q714 230 709 228Q706 227 694 227Q674 227 653 224Q646 221 643 215T629 164Q620 131 614 108Q589 6 586 3Q584 1 581 1Q571 1 553 21T530 52Q530 53 528 52T522 47Q448 -22 322 -22Q201 -22 126 55T50 252Z"></path><path id="MJX-115-TEX-N-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"></path><path id="MJX-115-TEX-I-1D45E" d="M33 157Q33 258 109 349T280 441Q340 441 372 389Q373 390 377 395T388 406T404 418Q438 442 450 442Q454 442 457 439T460 434Q460 425 391 149Q320 -135 320 -139Q320 -147 365 -148H390Q396 -156 396 -157T393 -175Q389 -188 383 -194H370Q339 -192 262 -192Q234 -192 211 -192T174 -192T157 -193Q143 -193 143 -185Q143 -182 145 -170Q149 -154 152 -151T172 -148Q220 -148 230 -141Q238 -136 258 -53T279 32Q279 33 272 29Q224 -10 172 -10Q117 -10 75 30T33 157ZM352 326Q329 405 277 405Q242 405 210 374T160 293Q131 214 119 129Q119 126 119 118T118 106Q118 61 136 44T179 26Q233 26 290 98L298 109L352 326Z"></path><path id="MJX-115-TEX-N-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"></path><path id="MJX-115-TEX-N-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"></path><path id="MJX-115-TEX-N-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"></path><path id="MJX-115-TEX-N-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"></path><path id="MJX-115-TEX-N-2E" d="M78 60Q78 84 95 102T138 120Q162 120 180 104T199 61Q199 36 182 18T139 0T96 17T78 60Z"></path><path id="MJX-115-TEX-N-32" d="M109 429Q82 429 66 447T50 491Q50 562 103 614T235 666Q326 666 387 610T449 465Q449 422 429 383T381 315T301 241Q265 210 201 149L142 93L218 92Q375 92 385 97Q392 99 409 186V189H449V186Q448 183 436 95T421 3V0H50V19V31Q50 38 56 46T86 81Q115 113 136 137Q145 147 170 174T204 211T233 244T261 278T284 308T305 340T320 369T333 401T340 431T343 464Q343 527 309 573T212 619Q179 619 154 602T119 569T109 550Q109 549 114 549Q132 549 151 535T170 489Q170 464 154 447T109 429Z"></path><path id="MJX-115-TEX-N-2B" d="M56 237T56 250T70 270H369V420L370 570Q380 583 389 583Q402 583 409 568V270H707Q722 262 722 250T707 230H409V-68Q401 -82 391 -82H389H387Q375 -82 369 -68V230H70Q56 237 56 250Z"></path><path id="MJX-115-TEX-N-30" d="M96 585Q152 666 249 666Q297 666 345 640T423 548Q460 465 460 320Q460 165 417 83Q397 41 362 16T301 -15T250 -22Q224 -22 198 -16T137 16T82 83Q39 165 39 320Q39 494 96 585ZM321 597Q291 629 250 629Q208 629 178 597Q153 571 145 525T137 333Q137 175 145 125T181 46Q209 16 250 16Q290 16 318 46Q347 76 354 130T362 333Q362 478 354 524T321 597Z"></path><path id="MJX-115-TEX-N-36" d="M42 313Q42 476 123 571T303 666Q372 666 402 630T432 550Q432 525 418 510T379 495Q356 495 341 509T326 548Q326 592 373 601Q351 623 311 626Q240 626 194 566Q147 500 147 364L148 360Q153 366 156 373Q197 433 263 433H267Q313 433 348 414Q372 400 396 374T435 317Q456 268 456 210V192Q456 169 451 149Q440 90 387 34T253 -22Q225 -22 199 -14T143 16T92 75T56 172T42 313ZM257 397Q227 397 205 380T171 335T154 278T148 216Q148 133 160 97T198 39Q222 21 251 21Q302 21 329 59Q342 77 347 104T352 209Q352 289 347 316T329 361Q302 397 257 397Z"></path><path id="MJX-115-TEX-N-33" d="M127 463Q100 463 85 480T69 524Q69 579 117 622T233 665Q268 665 277 664Q351 652 390 611T430 522Q430 470 396 421T302 350L299 348Q299 347 308 345T337 336T375 315Q457 262 457 175Q457 96 395 37T238 -22Q158 -22 100 21T42 130Q42 158 60 175T105 193Q133 193 151 175T169 130Q169 119 166 110T159 94T148 82T136 74T126 70T118 67L114 66Q165 21 238 21Q293 21 321 74Q338 107 338 175V195Q338 290 274 322Q259 328 213 329L171 330L168 332Q166 335 166 348Q166 366 174 366Q202 366 232 371Q266 376 294 413T322 525V533Q322 590 287 612Q265 626 240 626Q208 626 181 615T143 592T132 580H135Q138 579 143 578T153 573T165 566T175 555T183 540T186 520Q186 498 172 481T127 463Z"></path><path id="MJX-115-TEX-N-2192" d="M56 237T56 250T70 270H835Q719 357 692 493Q692 494 692 496T691 499Q691 511 708 511H711Q720 511 723 510T729 506T732 497T735 481T743 456Q765 389 816 336T935 261Q944 258 944 250Q944 244 939 241T915 231T877 212Q836 186 806 152T761 85T740 35T732 4Q730 -6 727 -8T711 -11Q691 -11 691 0Q691 7 696 25Q728 151 835 230H70Q56 237 56 250Z"></path><path id="MJX-115-TEX-N-2C" d="M78 35T78 60T94 103T137 121Q165 121 187 96T210 8Q210 -27 201 -60T180 -117T154 -158T130 -185T117 -194Q113 -194 104 -185T95 -172Q95 -168 106 -156T131 -126T157 -76T173 -3V9L172 8Q170 7 167 6T161 3T152 1T140 0Q113 0 96 17Z"></path><path id="MJX-115-TEX-N-35" d="M164 157Q164 133 148 117T109 101H102Q148 22 224 22Q294 22 326 82Q345 115 345 210Q345 313 318 349Q292 382 260 382H254Q176 382 136 314Q132 307 129 306T114 304Q97 304 95 310Q93 314 93 485V614Q93 664 98 664Q100 666 102 666Q103 666 123 658T178 642T253 634Q324 634 389 662Q397 666 402 666Q410 666 410 648V635Q328 538 205 538Q174 538 149 544L139 546V374Q158 388 169 396T205 412T256 420Q337 420 393 355T449 201Q449 109 385 44T229 -22Q148 -22 99 32T50 154Q50 178 61 192T84 210T107 214Q132 214 148 197T164 157Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mtable"><g data-mml-node="mtr" transform="translate(0,2731.9)"><g data-mml-node="mtd" transform="translate(3381.3,0)"><g data-mml-node="mi"><use data-c="1D43A" xlink:href="#MJX-115-TEX-I-1D43A"></use></g><g data-mml-node="mo" transform="translate(786,0)"><use data-c="28" xlink:href="#MJX-115-TEX-N-28"></use></g><g data-mml-node="msup" transform="translate(1175,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,413) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(2672.4,0)"><use data-c="29" xlink:href="#MJX-115-TEX-N-29"></use></g></g><g data-mml-node="mtd" transform="translate(6442.7,0)"><g data-mml-node="mi"></g><g data-mml-node="mo" transform="translate(277.8,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mfrac" transform="translate(1333.6,0)"><g data-mml-node="mrow" transform="translate(2468.9,676)"><g data-mml-node="msup"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,363) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(1719.6,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(2719.8,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="32" xlink:href="#MJX-115-TEX-N-32" transform="translate(778,0)"></use></g></g><g data-mml-node="mrow" transform="translate(220,-719.9)"><g data-mml-node="msup"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,289) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="32" xlink:href="#MJX-115-TEX-N-32"></use></g></g></g><g data-mml-node="mo" transform="translate(1719.6,0)"><use data-c="2B" xlink:href="#MJX-115-TEX-N-2B"></use></g><g data-mml-node="mn" transform="translate(2719.8,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="31" xlink:href="#MJX-115-TEX-N-31" transform="translate(778,0)"></use></g><g data-mml-node="msup" transform="translate(3997.8,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,289) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(5717.4,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(6717.7,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="30" xlink:href="#MJX-115-TEX-N-30" transform="translate(778,0)"></use><use data-c="36" xlink:href="#MJX-115-TEX-N-36" transform="translate(1278,0)"></use></g></g><rect width="8695.7" height="60" x="120" y="220"></rect></g></g></g><g data-mml-node="mtr" transform="translate(0,8)"><g data-mml-node="mtd" transform="translate(6442.7,0)"></g><g data-mml-node="mtd" transform="translate(6442.7,0)"><g data-mml-node="mi"></g><g data-mml-node="mo" transform="translate(277.8,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mfrac" transform="translate(1333.6,0)"><g data-mml-node="mrow" transform="translate(3246.9,676)"><g data-mml-node="msup"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,363) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(1719.6,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(2719.8,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="32" xlink:href="#MJX-115-TEX-N-32" transform="translate(778,0)"></use></g></g><g data-mml-node="mrow" transform="translate(220,-719.9)"><g data-mml-node="mo"><use data-c="28" xlink:href="#MJX-115-TEX-N-28"></use></g><g data-mml-node="msup" transform="translate(389,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,289) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(2108.6,0)"><use data-c="2B" xlink:href="#MJX-115-TEX-N-2B"></use></g><g data-mml-node="mn" transform="translate(3108.8,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="33" xlink:href="#MJX-115-TEX-N-33" transform="translate(778,0)"></use></g><g data-mml-node="mo" transform="translate(4386.8,0)"><use data-c="29" xlink:href="#MJX-115-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(4775.8,0)"><use data-c="28" xlink:href="#MJX-115-TEX-N-28"></use></g><g data-mml-node="msup" transform="translate(5164.8,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,289) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g></g><g data-mml-node="mo" transform="translate(6884.4,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(7884.7,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="32" xlink:href="#MJX-115-TEX-N-32" transform="translate(778,0)"></use><use data-c="33" xlink:href="#MJX-115-TEX-N-33" transform="translate(1278,0)"></use></g><g data-mml-node="mo" transform="translate(9662.7,0)"><use data-c="29" xlink:href="#MJX-115-TEX-N-29"></use></g></g><rect width="10251.7" height="60" x="120" y="220"></rect></g></g></g><g data-mml-node="mtr" transform="translate(0,-2145.9)"><g data-mml-node="mtd"><g data-mml-node="mo"><use data-c="2192" xlink:href="#MJX-115-TEX-N-2192"></use></g><g data-mml-node="msubsup" transform="translate(1277.8,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,413) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g><g data-mml-node="mn" transform="translate(479,-295.9) scale(0.707)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g><g data-mml-node="mo" transform="translate(3052.9,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mo" transform="translate(4108.7,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(4886.7,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="33" xlink:href="#MJX-115-TEX-N-33" transform="translate(778,0)"></use></g><g data-mml-node="mo" transform="translate(6164.7,0)"><use data-c="2C" xlink:href="#MJX-115-TEX-N-2C"></use></g></g><g data-mml-node="mtd" transform="translate(6442.7,0)"><g data-mml-node="mstyle"><g data-mml-node="mspace"></g></g><g data-mml-node="msubsup" transform="translate(1000,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="TeXAtom" transform="translate(543.7,413) scale(0.707)" data-mjx-texclass="ORD"><g data-mml-node="mo"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(778,0)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g><g data-mml-node="mn" transform="translate(479,-295.9) scale(0.707)"><use data-c="32" xlink:href="#MJX-115-TEX-N-32"></use></g></g><g data-mml-node="mo" transform="translate(2775.2,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mn" transform="translate(3830.9,0)"><use data-c="30" xlink:href="#MJX-115-TEX-N-30"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="32" xlink:href="#MJX-115-TEX-N-32" transform="translate(778,0)"></use></g></g></g><g data-mml-node="mtr" transform="translate(0,-3491.8)"><g data-mml-node="mtd" transform="translate(114.8,0)"><g data-mml-node="mo"><use data-c="2192" xlink:href="#MJX-115-TEX-N-2192"></use></g><g data-mml-node="msub" transform="translate(1277.8,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="mn" transform="translate(479,-150) scale(0.707)"><use data-c="31" xlink:href="#MJX-115-TEX-N-31"></use></g></g><g data-mml-node="mo" transform="translate(2438.1,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mo" transform="translate(3493.9,0)"><use data-c="2212" xlink:href="#MJX-115-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(4271.9,0)"><use data-c="33" xlink:href="#MJX-115-TEX-N-33"></use><use data-c="2E" xlink:href="#MJX-115-TEX-N-2E" transform="translate(500,0)"></use><use data-c="33" xlink:href="#MJX-115-TEX-N-33" transform="translate(778,0)"></use><use data-c="33" xlink:href="#MJX-115-TEX-N-33" transform="translate(1278,0)"></use></g><g data-mml-node="mo" transform="translate(6049.9,0)"><use data-c="2C" xlink:href="#MJX-115-TEX-N-2C"></use></g></g><g data-mml-node="mtd" transform="translate(6442.7,0)"><g data-mml-node="mstyle"><g data-mml-node="mspace"></g></g><g data-mml-node="msub" transform="translate(1000,0)"><g data-mml-node="mi"><use data-c="1D45E" xlink:href="#MJX-115-TEX-I-1D45E"></use></g><g data-mml-node="mn" transform="translate(479,-150) scale(0.707)"><use data-c="32" xlink:href="#MJX-115-TEX-N-32"></use></g></g><g data-mml-node="mo" transform="translate(2160.3,0)"><use data-c="3D" xlink:href="#MJX-115-TEX-N-3D"></use></g><g data-mml-node="mn" transform="translate(3216.1,0)"><use data-c="35" xlink:href="#MJX-115-TEX-N-35"></use></g></g></g></g></g></g></svg></mjx-container></div></div>
        <p>
            The absolute values of them are all larger than 1, it is unstable.<br>
            <b>Remember:</b> We should use q (rather than q<sup>-1</sup>) to determine whether it is a stable system. 
        </p>
</details>

4. What types are the 4 models?

   * a. $y(k)-0.1y(k-1)=\xi(k)+0.5\xi(k-1)+0.2u(k)+0.8u(k-1)$

   * b. $y(k)=\xi(k)+0.5\xi(k-1)+0.2u(k)+0.8u(k-1)$
   * c. $y(k)=\xi(k)+0.2\xi(k-1)$
   * d. $y(k)-0.1y(k-1)=\xi(k)$

   <details>
       <summary>Answer</summary>
       <p> From top to buttom, the models are:<br>
       a. CARMA model (or ARMAX).<br>
       b. CMA model (or MAX), because it <b>doesn't contain moving-average</b> for the coefficient of y(k) only contains 1.<br>
       c. MA model.<br>
       d. AR model.
       </p>
   </details>

5. Which one below is false? 

   A. Both a white noise sequence and a white noise process are white noises. 

   B. A random sequence $\xi(k)$ with zero mean is a white noise sequence. 

   C. The spectral density of a white noise must be a constant. 

   D. White noise signals at different time are not correlated.

   <details>
       <summary>Answer</summary><p>
       B. 零均值是白噪声的必要条件之一，但并不充分. 白噪声的定义不仅要求零均值，还要求<b>样本之间不相关</b>（即自相关函数为零，除了滞后为零的点），且具有有限的方差。
       </p>
   </details>

6. Consider the "state-space description"
   $$
   \begin{aligned}
   x(t+ 1)&= fx(t)+ w(t)\\
   y(t)&= hx(t)+ v(t)\end{aligned}
   $$

   where $x, f, h, w$ and $v$ are scalars. $\{w(t)\}$ and $\{v(t)\}$ are mutually independent white Gaussian noises with variances $R_1$ and $R_2$, respectively. Show that $y(t)$ can be represented as the ARMA form:
   $$
   y(t)+ a_1y(t- 1) +...+ a_ny(t- n)= e(t)+ c_1e(t- 1)+ ...+ c_ne(t- n)
   $$
   Determine $n, a_i, c_i$, and the variance of $e(t)$ in terms of $f, h, R_1$ and $R_2$. What is the relationship between $e(t)$, $w(t)$ and $v(t)$?

   <details>
       <summary>Answer</summary><p>其实我们要做的主要是，消掉<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="1.294ex" height="1.025ex" role="img" focusable="false" viewBox="0 -442 572 453" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.025ex;"><defs><path id="MJX-328-TEX-I-1D465" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D465" xlink:href="#MJX-328-TEX-I-1D465"></use></g></g></g></svg></mjx-container><script type="math/tex">x</script>项。显然对于这个题，由于它每次仅往后更新一步（因为t+1），所以相信聪明的你已经发现了，一定存在一个<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="1.319ex" height="1.597ex" role="img" focusable="false" viewBox="0 -694 583 706" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.027ex;"><defs><path id="MJX-122-TEX-I-1D706" d="M166 673Q166 685 183 694H202Q292 691 316 644Q322 629 373 486T474 207T524 67Q531 47 537 34T546 15T551 6T555 2T556 -2T550 -11H482Q457 3 450 18T399 152L354 277L340 262Q327 246 293 207T236 141Q211 112 174 69Q123 9 111 -1T83 -12Q47 -12 47 20Q47 37 61 52T199 187Q229 216 266 252T321 306L338 322Q338 323 288 462T234 612Q214 657 183 657Q166 657 166 673Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D706" xlink:href="#MJX-122-TEX-I-1D706"></use></g></g></g></svg></mjx-container><script type="math/tex">\lambda</script>使得<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="15.353ex" height="2.262ex" role="img" focusable="false" viewBox="0 -750 6785.9 1000" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.566ex;"><defs><path id="MJX-331-TEX-I-1D466" d="M21 287Q21 301 36 335T84 406T158 442Q199 442 224 419T250 355Q248 336 247 334Q247 331 231 288T198 191T182 105Q182 62 196 45T238 27Q261 27 281 38T312 61T339 94Q339 95 344 114T358 173T377 247Q415 397 419 404Q432 431 462 431Q475 431 483 424T494 412T496 403Q496 390 447 193T391 -23Q363 -106 294 -155T156 -205Q111 -205 77 -183T43 -117Q43 -95 50 -80T69 -58T89 -48T106 -45Q150 -45 150 -87Q150 -107 138 -122T115 -142T102 -147L99 -148Q101 -153 118 -160T152 -167H160Q177 -167 186 -165Q219 -156 247 -127T290 -65T313 -9T321 21L315 17Q309 13 296 6T270 -6Q250 -11 231 -11Q185 -11 150 11T104 82Q103 89 103 113Q103 170 138 262T173 379Q173 380 173 381Q173 390 173 393T169 400T158 404H154Q131 404 112 385T82 344T65 302T57 280Q55 278 41 278H27Q21 284 21 287Z"></path><path id="MJX-331-TEX-N-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"></path><path id="MJX-331-TEX-I-1D461" d="M26 385Q19 392 19 395Q19 399 22 411T27 425Q29 430 36 430T87 431H140L159 511Q162 522 166 540T173 566T179 586T187 603T197 615T211 624T229 626Q247 625 254 615T261 596Q261 589 252 549T232 470L222 433Q222 431 272 431H323Q330 424 330 420Q330 398 317 385H210L174 240Q135 80 135 68Q135 26 162 26Q197 26 230 60T283 144Q285 150 288 151T303 153H307Q322 153 322 145Q322 142 319 133Q314 117 301 95T267 48T216 6T155 -11Q125 -11 98 4T59 56Q57 64 57 83V101L92 241Q127 382 128 383Q128 385 77 385H26Z"></path><path id="MJX-331-TEX-N-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"></path><path id="MJX-331-TEX-N-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"></path><path id="MJX-331-TEX-I-1D706" d="M166 673Q166 685 183 694H202Q292 691 316 644Q322 629 373 486T474 207T524 67Q531 47 537 34T546 15T551 6T555 2T556 -2T550 -11H482Q457 3 450 18T399 152L354 277L340 262Q327 246 293 207T236 141Q211 112 174 69Q123 9 111 -1T83 -12Q47 -12 47 20Q47 37 61 52T199 187Q229 216 266 252T321 306L338 322Q338 323 288 462T234 612Q214 657 183 657Q166 657 166 673Z"></path><path id="MJX-331-TEX-N-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D466" xlink:href="#MJX-331-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(490,0)"><use data-c="28" xlink:href="#MJX-331-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(879,0)"><use data-c="1D461" xlink:href="#MJX-331-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(1240,0)"><use data-c="29" xlink:href="#MJX-331-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(1851.2,0)"><use data-c="2212" xlink:href="#MJX-331-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(2851.4,0)"><use data-c="1D706" xlink:href="#MJX-331-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(3434.4,0)"><use data-c="1D466" xlink:href="#MJX-331-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(3924.4,0)"><use data-c="28" xlink:href="#MJX-331-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(4313.4,0)"><use data-c="1D461" xlink:href="#MJX-331-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(4896.7,0)"><use data-c="2212" xlink:href="#MJX-331-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(5896.9,0)"><use data-c="31" xlink:href="#MJX-331-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(6396.9,0)"><use data-c="29" xlink:href="#MJX-331-TEX-N-29"></use></g></g></g></svg></mjx-container><script type="math/tex">y(t)-\lambda y(t-1)</script>能够抵消掉<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="1.294ex" height="1.025ex" role="img" focusable="false" viewBox="0 -442 572 453" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.025ex;"><defs><path id="MJX-328-TEX-I-1D465" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D465" xlink:href="#MJX-328-TEX-I-1D465"></use></g></g></g></svg></mjx-container><script type="math/tex">x</script>项。</p>
   <div contenteditable="false" spellcheck="false" class="mathjax-block md-end-block md-math-block md-rawblock" id="mathjax-n26" cid="n26" mdtype="math_block" data-math-tag-before="0" data-math-tag-after="0" data-math-labels="[]"><div class="md-math-container"><mjx-container class="MathJax" jax="SVG" display="true" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="73.391ex" height="8.145ex" role="img" focusable="false" viewBox="0 -2050 32438.7 3600" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -3.507ex;"><defs><path id="MJX-330-TEX-I-1D466" d="M21 287Q21 301 36 335T84 406T158 442Q199 442 224 419T250 355Q248 336 247 334Q247 331 231 288T198 191T182 105Q182 62 196 45T238 27Q261 27 281 38T312 61T339 94Q339 95 344 114T358 173T377 247Q415 397 419 404Q432 431 462 431Q475 431 483 424T494 412T496 403Q496 390 447 193T391 -23Q363 -106 294 -155T156 -205Q111 -205 77 -183T43 -117Q43 -95 50 -80T69 -58T89 -48T106 -45Q150 -45 150 -87Q150 -107 138 -122T115 -142T102 -147L99 -148Q101 -153 118 -160T152 -167H160Q177 -167 186 -165Q219 -156 247 -127T290 -65T313 -9T321 21L315 17Q309 13 296 6T270 -6Q250 -11 231 -11Q185 -11 150 11T104 82Q103 89 103 113Q103 170 138 262T173 379Q173 380 173 381Q173 390 173 393T169 400T158 404H154Q131 404 112 385T82 344T65 302T57 280Q55 278 41 278H27Q21 284 21 287Z"></path><path id="MJX-330-TEX-N-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"></path><path id="MJX-330-TEX-I-1D461" d="M26 385Q19 392 19 395Q19 399 22 411T27 425Q29 430 36 430T87 431H140L159 511Q162 522 166 540T173 566T179 586T187 603T197 615T211 624T229 626Q247 625 254 615T261 596Q261 589 252 549T232 470L222 433Q222 431 272 431H323Q330 424 330 420Q330 398 317 385H210L174 240Q135 80 135 68Q135 26 162 26Q197 26 230 60T283 144Q285 150 288 151T303 153H307Q322 153 322 145Q322 142 319 133Q314 117 301 95T267 48T216 6T155 -11Q125 -11 98 4T59 56Q57 64 57 83V101L92 241Q127 382 128 383Q128 385 77 385H26Z"></path><path id="MJX-330-TEX-N-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"></path><path id="MJX-330-TEX-N-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"></path><path id="MJX-330-TEX-I-1D706" d="M166 673Q166 685 183 694H202Q292 691 316 644Q322 629 373 486T474 207T524 67Q531 47 537 34T546 15T551 6T555 2T556 -2T550 -11H482Q457 3 450 18T399 152L354 277L340 262Q327 246 293 207T236 141Q211 112 174 69Q123 9 111 -1T83 -12Q47 -12 47 20Q47 37 61 52T199 187Q229 216 266 252T321 306L338 322Q338 323 288 462T234 612Q214 657 183 657Q166 657 166 673Z"></path><path id="MJX-330-TEX-N-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"></path><path id="MJX-330-TEX-N-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"></path><path id="MJX-330-TEX-I-210E" d="M137 683Q138 683 209 688T282 694Q294 694 294 685Q294 674 258 534Q220 386 220 383Q220 381 227 388Q288 442 357 442Q411 442 444 415T478 336Q478 285 440 178T402 50Q403 36 407 31T422 26Q450 26 474 56T513 138Q516 149 519 151T535 153Q555 153 555 145Q555 144 551 130Q535 71 500 33Q466 -10 419 -10H414Q367 -10 346 17T325 74Q325 90 361 192T398 345Q398 404 354 404H349Q266 404 205 306L198 293L164 158Q132 28 127 16Q114 -11 83 -11Q69 -11 59 -2T48 16Q48 30 121 320L195 616Q195 629 188 632T149 637H128Q122 643 122 645T124 664Q129 683 137 683Z"></path><path id="MJX-330-TEX-N-5B" d="M118 -250V750H255V710H158V-210H255V-250H118Z"></path><path id="MJX-330-TEX-I-1D465" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"></path><path id="MJX-330-TEX-N-5D" d="M22 710V750H159V-250H22V-210H119V710H22Z"></path><path id="MJX-330-TEX-N-2B" d="M56 237T56 250T70 270H369V420L370 570Q380 583 389 583Q402 583 409 568V270H707Q722 262 722 250T707 230H409V-68Q401 -82 391 -82H389H387Q375 -82 369 -68V230H70Q56 237 56 250Z"></path><path id="MJX-330-TEX-I-1D463" d="M173 380Q173 405 154 405Q130 405 104 376T61 287Q60 286 59 284T58 281T56 279T53 278T49 278T41 278H27Q21 284 21 287Q21 294 29 316T53 368T97 419T160 441Q202 441 225 417T249 361Q249 344 246 335Q246 329 231 291T200 202T182 113Q182 86 187 69Q200 26 250 26Q287 26 319 60T369 139T398 222T409 277Q409 300 401 317T383 343T365 361T357 383Q357 405 376 424T417 443Q436 443 451 425T467 367Q467 340 455 284T418 159T347 40T241 -11Q177 -11 139 22Q102 54 102 117Q102 148 110 181T151 298Q173 362 173 380Z"></path><path id="MJX-330-TEX-N-7B" d="M434 -231Q434 -244 428 -250H410Q281 -250 230 -184Q225 -177 222 -172T217 -161T213 -148T211 -133T210 -111T209 -84T209 -47T209 0Q209 21 209 53Q208 142 204 153Q203 154 203 155Q189 191 153 211T82 231Q71 231 68 234T65 250T68 266T82 269Q116 269 152 289T203 345Q208 356 208 377T209 529V579Q209 634 215 656T244 698Q270 724 324 740Q361 748 377 749Q379 749 390 749T408 750H428Q434 744 434 732Q434 719 431 716Q429 713 415 713Q362 710 332 689T296 647Q291 634 291 499V417Q291 370 288 353T271 314Q240 271 184 255L170 250L184 245Q202 239 220 230T262 196T290 137Q291 131 291 1Q291 -134 296 -147Q306 -174 339 -192T415 -213Q429 -213 431 -216Q434 -219 434 -231Z"></path><path id="MJX-330-TEX-I-1D453" d="M118 -162Q120 -162 124 -164T135 -167T147 -168Q160 -168 171 -155T187 -126Q197 -99 221 27T267 267T289 382V385H242Q195 385 192 387Q188 390 188 397L195 425Q197 430 203 430T250 431Q298 431 298 432Q298 434 307 482T319 540Q356 705 465 705Q502 703 526 683T550 630Q550 594 529 578T487 561Q443 561 443 603Q443 622 454 636T478 657L487 662Q471 668 457 668Q445 668 434 658T419 630Q412 601 403 552T387 469T380 433Q380 431 435 431Q480 431 487 430T498 424Q499 420 496 407T491 391Q489 386 482 386T428 385H372L349 263Q301 15 282 -47Q255 -132 212 -173Q175 -205 139 -205Q107 -205 81 -186T55 -132Q55 -95 76 -78T118 -61Q162 -61 162 -103Q162 -122 151 -136T127 -157L118 -162Z"></path><path id="MJX-330-TEX-I-1D464" d="M580 385Q580 406 599 424T641 443Q659 443 674 425T690 368Q690 339 671 253Q656 197 644 161T609 80T554 12T482 -11Q438 -11 404 5T355 48Q354 47 352 44Q311 -11 252 -11Q226 -11 202 -5T155 14T118 53T104 116Q104 170 138 262T173 379Q173 380 173 381Q173 390 173 393T169 400T158 404H154Q131 404 112 385T82 344T65 302T57 280Q55 278 41 278H27Q21 284 21 287Q21 293 29 315T52 366T96 418T161 441Q204 441 227 416T250 358Q250 340 217 250T184 111Q184 65 205 46T258 26Q301 26 334 87L339 96V119Q339 122 339 128T340 136T341 143T342 152T345 165T348 182T354 206T362 238T373 281Q402 395 406 404Q419 431 449 431Q468 431 475 421T483 402Q483 389 454 274T422 142Q420 131 420 107V100Q420 85 423 71T442 42T487 26Q558 26 600 148Q609 171 620 213T632 273Q632 306 619 325T593 357T580 385Z"></path><path id="MJX-330-TEX-N-7D" d="M65 731Q65 745 68 747T88 750Q171 750 216 725T279 670Q288 649 289 635T291 501Q292 362 293 357Q306 312 345 291T417 269Q428 269 431 266T434 250T431 234T417 231Q380 231 345 210T298 157Q293 143 292 121T291 -28V-79Q291 -134 285 -156T256 -198Q202 -250 89 -250Q71 -250 68 -247T65 -230Q65 -224 65 -223T66 -218T69 -214T77 -213Q91 -213 108 -210T146 -200T183 -177T207 -139Q208 -134 209 3L210 139Q223 196 280 230Q315 247 330 250Q305 257 280 270Q225 304 212 352L210 362L209 498Q208 635 207 640Q195 680 154 696T77 713Q68 713 67 716T65 731Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mtable"><g data-mml-node="mtr" transform="translate(0,1300)"><g data-mml-node="mtd"><g data-mml-node="mi"><use data-c="1D466" xlink:href="#MJX-330-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(490,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(879,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(1240,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(1851.2,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(2851.4,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(3434.4,0)"><use data-c="1D466" xlink:href="#MJX-330-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(3924.4,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(4313.4,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(4896.7,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(5896.9,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(6396.9,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g></g><g data-mml-node="mtd" transform="translate(6785.9,0)"><g data-mml-node="mi"></g><g data-mml-node="mo" transform="translate(277.8,0)"><use data-c="3D" xlink:href="#MJX-330-TEX-N-3D"></use></g><g data-mml-node="mi" transform="translate(1333.6,0)"><use data-c="210E" xlink:href="#MJX-330-TEX-I-210E"></use></g><g data-mml-node="mrow" transform="translate(2076.2,0)"><g data-mml-node="mo"><use data-c="5B" xlink:href="#MJX-330-TEX-N-5B"></use></g><g data-mml-node="mi" transform="translate(278,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(850,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(1239,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(1600,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(2211.2,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(3211.4,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(3794.4,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(4366.4,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(4755.4,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(5338.7,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(6338.9,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(6838.9,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(7227.9,0)"><use data-c="5D" xlink:href="#MJX-330-TEX-N-5D"></use></g></g><g data-mml-node="mo" transform="translate(9804.3,0)"><use data-c="2B" xlink:href="#MJX-330-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(10804.6,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(11289.6,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(11678.6,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(12039.6,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(12650.8,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(13651,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(14234,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(14719,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(15108,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(15691.2,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(16691.4,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(17191.4,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g></g></g><g data-mml-node="mtr" transform="translate(0,0)"><g data-mml-node="mtd" transform="translate(6785.9,0)"></g><g data-mml-node="mtd" transform="translate(6785.9,0)"><g data-mml-node="mi"></g><g data-mml-node="mo" transform="translate(277.8,0)"><use data-c="3D" xlink:href="#MJX-330-TEX-N-3D"></use></g><g data-mml-node="mi" transform="translate(1333.6,0)"><use data-c="210E" xlink:href="#MJX-330-TEX-I-210E"></use></g><g data-mml-node="mrow" transform="translate(2076.2,0)"><g data-mml-node="mo"><use data-c="7B" xlink:href="#MJX-330-TEX-N-7B"></use></g><g data-mml-node="mo" transform="translate(500,0)"><use data-c="5B" xlink:href="#MJX-330-TEX-N-5B"></use></g><g data-mml-node="mi" transform="translate(778,0)"><use data-c="1D453" xlink:href="#MJX-330-TEX-I-1D453"></use></g><g data-mml-node="mi" transform="translate(1328,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(1900,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(2289,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(2872.2,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(3872.4,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(4372.4,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(4983.7,0)"><use data-c="2B" xlink:href="#MJX-330-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(5983.9,0)"><use data-c="1D464" xlink:href="#MJX-330-TEX-I-1D464"></use></g><g data-mml-node="mo" transform="translate(6699.9,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(7088.9,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(7672.1,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(8672.3,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(9172.3,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(9561.3,0)"><use data-c="5D" xlink:href="#MJX-330-TEX-N-5D"></use></g><g data-mml-node="mo" transform="translate(10061.6,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(11061.8,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(11644.8,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(12216.8,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(12605.8,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(13189,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(14189.2,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(14689.2,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(15078.2,0)"><use data-c="7D" xlink:href="#MJX-330-TEX-N-7D"></use></g></g><g data-mml-node="mo" transform="translate(17876.7,0)"><use data-c="2B" xlink:href="#MJX-330-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(18876.9,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(19361.9,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(19750.9,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(20111.9,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(20723.1,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(21723.3,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(22306.3,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(22791.3,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(23180.3,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(23763.6,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(24763.8,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(25263.8,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g></g></g><g data-mml-node="mtr" transform="translate(0,-1300)"><g data-mml-node="mtd" transform="translate(6785.9,0)"></g><g data-mml-node="mtd" transform="translate(6785.9,0)"><g data-mml-node="mi"></g><g data-mml-node="mo" transform="translate(277.8,0)"><use data-c="3D" xlink:href="#MJX-330-TEX-N-3D"></use></g><g data-mml-node="mi" transform="translate(1333.6,0)"><use data-c="210E" xlink:href="#MJX-330-TEX-I-210E"></use></g><g data-mml-node="mrow" transform="translate(2076.2,0)"><g data-mml-node="mo"><use data-c="5B" xlink:href="#MJX-330-TEX-N-5B"></use></g><g data-mml-node="mi" transform="translate(278,0)"><use data-c="1D453" xlink:href="#MJX-330-TEX-I-1D453"></use></g><g data-mml-node="mi" transform="translate(828,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(1400,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(1789,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(2372.2,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(3372.4,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(3872.4,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(4483.7,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(5483.9,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(6066.9,0)"><use data-c="1D465" xlink:href="#MJX-330-TEX-I-1D465"></use></g><g data-mml-node="mo" transform="translate(6638.9,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(7027.9,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(7611.1,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(8611.3,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(9111.3,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(9722.6,0)"><use data-c="2B" xlink:href="#MJX-330-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(10722.8,0)"><use data-c="1D464" xlink:href="#MJX-330-TEX-I-1D464"></use></g><g data-mml-node="mo" transform="translate(11438.8,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(11827.8,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(12411,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(13411.2,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(13911.2,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(14300.2,0)"><use data-c="5D" xlink:href="#MJX-330-TEX-N-5D"></use></g></g><g data-mml-node="mo" transform="translate(16876.7,0)"><use data-c="2B" xlink:href="#MJX-330-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(17876.9,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(18361.9,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(18750.9,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(19111.9,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(19723.1,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(20723.3,0)"><use data-c="1D706" xlink:href="#MJX-330-TEX-I-1D706"></use></g><g data-mml-node="mi" transform="translate(21306.3,0)"><use data-c="1D463" xlink:href="#MJX-330-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(21791.3,0)"><use data-c="28" xlink:href="#MJX-330-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(22180.3,0)"><use data-c="1D461" xlink:href="#MJX-330-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(22763.6,0)"><use data-c="2212" xlink:href="#MJX-330-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(23763.8,0)"><use data-c="31" xlink:href="#MJX-330-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(24263.8,0)"><use data-c="29" xlink:href="#MJX-330-TEX-N-29"></use></g></g></g></g></g></g></svg></mjx-container></div></div>
   <p>我们惊讶地发现，当<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="5.58ex" height="2.059ex" role="img" focusable="false" viewBox="0 -705 2466.6 910" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.464ex;"><defs><path id="MJX-290-TEX-I-1D706" d="M166 673Q166 685 183 694H202Q292 691 316 644Q322 629 373 486T474 207T524 67Q531 47 537 34T546 15T551 6T555 2T556 -2T550 -11H482Q457 3 450 18T399 152L354 277L340 262Q327 246 293 207T236 141Q211 112 174 69Q123 9 111 -1T83 -12Q47 -12 47 20Q47 37 61 52T199 187Q229 216 266 252T321 306L338 322Q338 323 288 462T234 612Q214 657 183 657Q166 657 166 673Z"></path><path id="MJX-290-TEX-N-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"></path><path id="MJX-290-TEX-I-1D453" d="M118 -162Q120 -162 124 -164T135 -167T147 -168Q160 -168 171 -155T187 -126Q197 -99 221 27T267 267T289 382V385H242Q195 385 192 387Q188 390 188 397L195 425Q197 430 203 430T250 431Q298 431 298 432Q298 434 307 482T319 540Q356 705 465 705Q502 703 526 683T550 630Q550 594 529 578T487 561Q443 561 443 603Q443 622 454 636T478 657L487 662Q471 668 457 668Q445 668 434 658T419 630Q412 601 403 552T387 469T380 433Q380 431 435 431Q480 431 487 430T498 424Q499 420 496 407T491 391Q489 386 482 386T428 385H372L349 263Q301 15 282 -47Q255 -132 212 -173Q175 -205 139 -205Q107 -205 81 -186T55 -132Q55 -95 76 -78T118 -61Q162 -61 162 -103Q162 -122 151 -136T127 -157L118 -162Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D706" xlink:href="#MJX-290-TEX-I-1D706"></use></g><g data-mml-node="mo" transform="translate(860.8,0)"><use data-c="3D" xlink:href="#MJX-290-TEX-N-3D"></use></g><g data-mml-node="mi" transform="translate(1916.6,0)"><use data-c="1D453" xlink:href="#MJX-290-TEX-I-1D453"></use></g></g></g></svg></mjx-container><script type="math/tex">\lambda=f</script>时我们成功消除了<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="1.294ex" height="1.025ex" role="img" focusable="false" viewBox="0 -442 572 453" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.025ex;"><defs><path id="MJX-328-TEX-I-1D465" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D465" xlink:href="#MJX-328-TEX-I-1D465"></use></g></g></g></svg></mjx-container><script type="math/tex">x</script>项的系数，并得到<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="45.713ex" height="2.262ex" role="img" focusable="false" viewBox="0 -750 20205.2 1000" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.566ex;"><defs><path id="MJX-329-TEX-I-1D466" d="M21 287Q21 301 36 335T84 406T158 442Q199 442 224 419T250 355Q248 336 247 334Q247 331 231 288T198 191T182 105Q182 62 196 45T238 27Q261 27 281 38T312 61T339 94Q339 95 344 114T358 173T377 247Q415 397 419 404Q432 431 462 431Q475 431 483 424T494 412T496 403Q496 390 447 193T391 -23Q363 -106 294 -155T156 -205Q111 -205 77 -183T43 -117Q43 -95 50 -80T69 -58T89 -48T106 -45Q150 -45 150 -87Q150 -107 138 -122T115 -142T102 -147L99 -148Q101 -153 118 -160T152 -167H160Q177 -167 186 -165Q219 -156 247 -127T290 -65T313 -9T321 21L315 17Q309 13 296 6T270 -6Q250 -11 231 -11Q185 -11 150 11T104 82Q103 89 103 113Q103 170 138 262T173 379Q173 380 173 381Q173 390 173 393T169 400T158 404H154Q131 404 112 385T82 344T65 302T57 280Q55 278 41 278H27Q21 284 21 287Z"></path><path id="MJX-329-TEX-N-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"></path><path id="MJX-329-TEX-I-1D461" d="M26 385Q19 392 19 395Q19 399 22 411T27 425Q29 430 36 430T87 431H140L159 511Q162 522 166 540T173 566T179 586T187 603T197 615T211 624T229 626Q247 625 254 615T261 596Q261 589 252 549T232 470L222 433Q222 431 272 431H323Q330 424 330 420Q330 398 317 385H210L174 240Q135 80 135 68Q135 26 162 26Q197 26 230 60T283 144Q285 150 288 151T303 153H307Q322 153 322 145Q322 142 319 133Q314 117 301 95T267 48T216 6T155 -11Q125 -11 98 4T59 56Q57 64 57 83V101L92 241Q127 382 128 383Q128 385 77 385H26Z"></path><path id="MJX-329-TEX-N-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"></path><path id="MJX-329-TEX-N-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"></path><path id="MJX-329-TEX-I-1D453" d="M118 -162Q120 -162 124 -164T135 -167T147 -168Q160 -168 171 -155T187 -126Q197 -99 221 27T267 267T289 382V385H242Q195 385 192 387Q188 390 188 397L195 425Q197 430 203 430T250 431Q298 431 298 432Q298 434 307 482T319 540Q356 705 465 705Q502 703 526 683T550 630Q550 594 529 578T487 561Q443 561 443 603Q443 622 454 636T478 657L487 662Q471 668 457 668Q445 668 434 658T419 630Q412 601 403 552T387 469T380 433Q380 431 435 431Q480 431 487 430T498 424Q499 420 496 407T491 391Q489 386 482 386T428 385H372L349 263Q301 15 282 -47Q255 -132 212 -173Q175 -205 139 -205Q107 -205 81 -186T55 -132Q55 -95 76 -78T118 -61Q162 -61 162 -103Q162 -122 151 -136T127 -157L118 -162Z"></path><path id="MJX-329-TEX-N-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"></path><path id="MJX-329-TEX-N-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"></path><path id="MJX-329-TEX-I-210E" d="M137 683Q138 683 209 688T282 694Q294 694 294 685Q294 674 258 534Q220 386 220 383Q220 381 227 388Q288 442 357 442Q411 442 444 415T478 336Q478 285 440 178T402 50Q403 36 407 31T422 26Q450 26 474 56T513 138Q516 149 519 151T535 153Q555 153 555 145Q555 144 551 130Q535 71 500 33Q466 -10 419 -10H414Q367 -10 346 17T325 74Q325 90 361 192T398 345Q398 404 354 404H349Q266 404 205 306L198 293L164 158Q132 28 127 16Q114 -11 83 -11Q69 -11 59 -2T48 16Q48 30 121 320L195 616Q195 629 188 632T149 637H128Q122 643 122 645T124 664Q129 683 137 683Z"></path><path id="MJX-329-TEX-I-1D464" d="M580 385Q580 406 599 424T641 443Q659 443 674 425T690 368Q690 339 671 253Q656 197 644 161T609 80T554 12T482 -11Q438 -11 404 5T355 48Q354 47 352 44Q311 -11 252 -11Q226 -11 202 -5T155 14T118 53T104 116Q104 170 138 262T173 379Q173 380 173 381Q173 390 173 393T169 400T158 404H154Q131 404 112 385T82 344T65 302T57 280Q55 278 41 278H27Q21 284 21 287Q21 293 29 315T52 366T96 418T161 441Q204 441 227 416T250 358Q250 340 217 250T184 111Q184 65 205 46T258 26Q301 26 334 87L339 96V119Q339 122 339 128T340 136T341 143T342 152T345 165T348 182T354 206T362 238T373 281Q402 395 406 404Q419 431 449 431Q468 431 475 421T483 402Q483 389 454 274T422 142Q420 131 420 107V100Q420 85 423 71T442 42T487 26Q558 26 600 148Q609 171 620 213T632 273Q632 306 619 325T593 357T580 385Z"></path><path id="MJX-329-TEX-N-2B" d="M56 237T56 250T70 270H369V420L370 570Q380 583 389 583Q402 583 409 568V270H707Q722 262 722 250T707 230H409V-68Q401 -82 391 -82H389H387Q375 -82 369 -68V230H70Q56 237 56 250Z"></path><path id="MJX-329-TEX-I-1D463" d="M173 380Q173 405 154 405Q130 405 104 376T61 287Q60 286 59 284T58 281T56 279T53 278T49 278T41 278H27Q21 284 21 287Q21 294 29 316T53 368T97 419T160 441Q202 441 225 417T249 361Q249 344 246 335Q246 329 231 291T200 202T182 113Q182 86 187 69Q200 26 250 26Q287 26 319 60T369 139T398 222T409 277Q409 300 401 317T383 343T365 361T357 383Q357 405 376 424T417 443Q436 443 451 425T467 367Q467 340 455 284T418 159T347 40T241 -11Q177 -11 139 22Q102 54 102 117Q102 148 110 181T151 298Q173 362 173 380Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="mi"><use data-c="1D466" xlink:href="#MJX-329-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(490,0)"><use data-c="28" xlink:href="#MJX-329-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(879,0)"><use data-c="1D461" xlink:href="#MJX-329-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(1240,0)"><use data-c="29" xlink:href="#MJX-329-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(1851.2,0)"><use data-c="2212" xlink:href="#MJX-329-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(2851.4,0)"><use data-c="1D453" xlink:href="#MJX-329-TEX-I-1D453"></use></g><g data-mml-node="mi" transform="translate(3401.4,0)"><use data-c="1D466" xlink:href="#MJX-329-TEX-I-1D466"></use></g><g data-mml-node="mo" transform="translate(3891.4,0)"><use data-c="28" xlink:href="#MJX-329-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(4280.4,0)"><use data-c="1D461" xlink:href="#MJX-329-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(4863.7,0)"><use data-c="2212" xlink:href="#MJX-329-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(5863.9,0)"><use data-c="31" xlink:href="#MJX-329-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(6363.9,0)"><use data-c="29" xlink:href="#MJX-329-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(7030.7,0)"><use data-c="3D" xlink:href="#MJX-329-TEX-N-3D"></use></g><g data-mml-node="mi" transform="translate(8086.4,0)"><use data-c="210E" xlink:href="#MJX-329-TEX-I-210E"></use></g><g data-mml-node="mi" transform="translate(8662.4,0)"><use data-c="1D464" xlink:href="#MJX-329-TEX-I-1D464"></use></g><g data-mml-node="mo" transform="translate(9378.4,0)"><use data-c="28" xlink:href="#MJX-329-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(9767.4,0)"><use data-c="1D461" xlink:href="#MJX-329-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(10350.7,0)"><use data-c="2212" xlink:href="#MJX-329-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(11350.9,0)"><use data-c="31" xlink:href="#MJX-329-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(11850.9,0)"><use data-c="29" xlink:href="#MJX-329-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(12462.1,0)"><use data-c="2B" xlink:href="#MJX-329-TEX-N-2B"></use></g><g data-mml-node="mi" transform="translate(13462.3,0)"><use data-c="1D463" xlink:href="#MJX-329-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(13947.3,0)"><use data-c="28" xlink:href="#MJX-329-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(14336.3,0)"><use data-c="1D461" xlink:href="#MJX-329-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(14697.3,0)"><use data-c="29" xlink:href="#MJX-329-TEX-N-29"></use></g><g data-mml-node="mo" transform="translate(15308.6,0)"><use data-c="2212" xlink:href="#MJX-329-TEX-N-2212"></use></g><g data-mml-node="mi" transform="translate(16308.8,0)"><use data-c="1D453" xlink:href="#MJX-329-TEX-I-1D453"></use></g><g data-mml-node="mi" transform="translate(16858.8,0)"><use data-c="1D463" xlink:href="#MJX-329-TEX-I-1D463"></use></g><g data-mml-node="mo" transform="translate(17343.8,0)"><use data-c="28" xlink:href="#MJX-329-TEX-N-28"></use></g><g data-mml-node="mi" transform="translate(17732.8,0)"><use data-c="1D461" xlink:href="#MJX-329-TEX-I-1D461"></use></g><g data-mml-node="mo" transform="translate(18316,0)"><use data-c="2212" xlink:href="#MJX-329-TEX-N-2212"></use></g><g data-mml-node="mn" transform="translate(19316.2,0)"><use data-c="31" xlink:href="#MJX-329-TEX-N-31"></use></g><g data-mml-node="mo" transform="translate(19816.2,0)"><use data-c="29" xlink:href="#MJX-329-TEX-N-29"></use></g></g></g></svg></mjx-container><script type="math/tex">y(t)-fy(t-1)=hw(t-1)+v(t)-fv(t-1)</script>。</p>
   <p>因此，新的方差将会变成：<mjx-container class="MathJax" jax="SVG" style="position: relative;"><svg xmlns="http://www.w3.org/2000/svg" width="18.289ex" height="2.351ex" role="img" focusable="false" viewBox="0 -833.9 8083.7 1038.9" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" style="vertical-align: -0.464ex;"><defs><path id="MJX-326-TEX-I-1D445" d="M230 637Q203 637 198 638T193 649Q193 676 204 682Q206 683 378 683Q550 682 564 680Q620 672 658 652T712 606T733 563T739 529Q739 484 710 445T643 385T576 351T538 338L545 333Q612 295 612 223Q612 212 607 162T602 80V71Q602 53 603 43T614 25T640 16Q668 16 686 38T712 85Q717 99 720 102T735 105Q755 105 755 93Q755 75 731 36Q693 -21 641 -21H632Q571 -21 531 4T487 82Q487 109 502 166T517 239Q517 290 474 313Q459 320 449 321T378 323H309L277 193Q244 61 244 59Q244 55 245 54T252 50T269 48T302 46H333Q339 38 339 37T336 19Q332 6 326 0H311Q275 2 180 2Q146 2 117 2T71 2T50 1Q33 1 33 10Q33 12 36 24Q41 43 46 45Q50 46 61 46H67Q94 46 127 49Q141 52 146 61Q149 65 218 339T287 628Q287 635 230 637ZM630 554Q630 586 609 608T523 636Q521 636 500 636T462 637H440Q393 637 386 627Q385 624 352 494T319 361Q319 360 388 360Q466 361 492 367Q556 377 592 426Q608 449 619 486T630 554Z"></path><path id="MJX-326-TEX-N-32" d="M109 429Q82 429 66 447T50 491Q50 562 103 614T235 666Q326 666 387 610T449 465Q449 422 429 383T381 315T301 241Q265 210 201 149L142 93L218 92Q375 92 385 97Q392 99 409 186V189H449V186Q448 183 436 95T421 3V0H50V19V31Q50 38 56 46T86 81Q115 113 136 137Q145 147 170 174T204 211T233 244T261 278T284 308T305 340T320 369T333 401T340 431T343 464Q343 527 309 573T212 619Q179 619 154 602T119 569T109 550Q109 549 114 549Q132 549 151 535T170 489Q170 464 154 447T109 429Z"></path><path id="MJX-326-TEX-N-2B" d="M56 237T56 250T70 270H369V420L370 570Q380 583 389 583Q402 583 409 568V270H707Q722 262 722 250T707 230H409V-68Q401 -82 391 -82H389H387Q375 -82 369 -68V230H70Q56 237 56 250Z"></path><path id="MJX-326-TEX-I-210E" d="M137 683Q138 683 209 688T282 694Q294 694 294 685Q294 674 258 534Q220 386 220 383Q220 381 227 388Q288 442 357 442Q411 442 444 415T478 336Q478 285 440 178T402 50Q403 36 407 31T422 26Q450 26 474 56T513 138Q516 149 519 151T535 153Q555 153 555 145Q555 144 551 130Q535 71 500 33Q466 -10 419 -10H414Q367 -10 346 17T325 74Q325 90 361 192T398 345Q398 404 354 404H349Q266 404 205 306L198 293L164 158Q132 28 127 16Q114 -11 83 -11Q69 -11 59 -2T48 16Q48 30 121 320L195 616Q195 629 188 632T149 637H128Q122 643 122 645T124 664Q129 683 137 683Z"></path><path id="MJX-326-TEX-N-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"></path><path id="MJX-326-TEX-I-1D453" d="M118 -162Q120 -162 124 -164T135 -167T147 -168Q160 -168 171 -155T187 -126Q197 -99 221 27T267 267T289 382V385H242Q195 385 192 387Q188 390 188 397L195 425Q197 430 203 430T250 431Q298 431 298 432Q298 434 307 482T319 540Q356 705 465 705Q502 703 526 683T550 630Q550 594 529 578T487 561Q443 561 443 603Q443 622 454 636T478 657L487 662Q471 668 457 668Q445 668 434 658T419 630Q412 601 403 552T387 469T380 433Q380 431 435 431Q480 431 487 430T498 424Q499 420 496 407T491 391Q489 386 482 386T428 385H372L349 263Q301 15 282 -47Q255 -132 212 -173Q175 -205 139 -205Q107 -205 81 -186T55 -132Q55 -95 76 -78T118 -61Q162 -61 162 -103Q162 -122 151 -136T127 -157L118 -162Z"></path></defs><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="scale(1,-1)"><g data-mml-node="math"><g data-mml-node="msub"><g data-mml-node="mi"><use data-c="1D445" xlink:href="#MJX-326-TEX-I-1D445"></use></g><g data-mml-node="mn" transform="translate(792,-150) scale(0.707)"><use data-c="32" xlink:href="#MJX-326-TEX-N-32"></use></g></g><g data-mml-node="mo" transform="translate(1417.8,0)"><use data-c="2B" xlink:href="#MJX-326-TEX-N-2B"></use></g><g data-mml-node="msup" transform="translate(2418,0)"><g data-mml-node="mi"><use data-c="210E" xlink:href="#MJX-326-TEX-I-210E"></use></g><g data-mml-node="mn" transform="translate(609,363) scale(0.707)"><use data-c="32" xlink:href="#MJX-326-TEX-N-32"></use></g></g><g data-mml-node="msub" transform="translate(3430.6,0)"><g data-mml-node="mi"><use data-c="1D445" xlink:href="#MJX-326-TEX-I-1D445"></use></g><g data-mml-node="mn" transform="translate(792,-150) scale(0.707)"><use data-c="31" xlink:href="#MJX-326-TEX-N-31"></use></g></g><g data-mml-node="mo" transform="translate(4848.3,0)"><use data-c="2B" xlink:href="#MJX-326-TEX-N-2B"></use></g><g data-mml-node="msup" transform="translate(5848.5,0)"><g data-mml-node="mi"><use data-c="1D453" xlink:href="#MJX-326-TEX-I-1D453"></use></g><g data-mml-node="mn" transform="translate(636,363) scale(0.707)"><use data-c="32" xlink:href="#MJX-326-TEX-N-32"></use></g></g><g data-mml-node="msub" transform="translate(6888.1,0)"><g data-mml-node="mi"><use data-c="1D445" xlink:href="#MJX-326-TEX-I-1D445"></use></g><g data-mml-node="mn" transform="translate(792,-150) scale(0.707)"><use data-c="32" xlink:href="#MJX-326-TEX-N-32"></use></g></g></g></g></svg></mjx-container><script type="math/tex">R_2+h^2R_1+f^2R_2</script></p>
   </details>
   
