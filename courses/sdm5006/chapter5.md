<p align='center'><font size=8><b>模型参考自适应控制</b></font><br><br>Model Refered Adaptive Control (MRAC)</p>

# 梯度下降和自适应控制

在这之前，首先让我们回顾一下什么是梯度下降。

对于某个函数$L(x)$，如果我们希望得到它的最小值，例如，当函数为$L(x)=\frac12x^2$时，观察可以发现，倘若某点在$x=0$左侧时，需要往正方向走一步才可能到最小值点；某点在其右侧时候，需要往负方向走一步，才可能到最小值点。

让我们来计算$L(x)$函数的梯度$\nabla L(x)=\frac{dL(x)}{dx}=x$。

如果我们选择一个很小的参数$\gamma$（在机器学习中，通常把它称为“学习率”，用$\eta$表示）让某个动点的函数值“逼近”该函数的最低点，可以发现：

**略。**（没空写qwq）

值得一提的是，有的函数可能不具有全局最小值，也可能有多个全局最小值，在设计这样的函数的时候需要有所注意。

因此，我们可以通过设计某种具有这样性质的函数，来对待优化的问题进行求解。

## MIT自适应控制律

如果控制目标和目标的误差绝对值趋近于0，将会是一个很好的结果。很显然，我们可以用上文提到的函数来作为其性能指标函数：

$L(e(t))=\frac{1}{2}e(t)^2$，其中$e(t)=y_m(t)-y_p(t)$表示参考模型的输出（$y_m(t)$）与实际系统的输出（$y_p(t)$）的误差。

类似于机器学习的梯度更新公式，参数*随着时间*的更新过程便可以被写为：
$$
\Theta\leftarrow\Theta-\gamma\frac{\partial J}{\partial \Theta}\cdot dt=\Theta-\gamma e\cdot\frac{\partial e}{\partial \Theta}
$$
显然，为了得到$\frac{\partial e}{\partial \Theta}$，我们需要找到误差和我们设计的参数之间的关联。接下来，让我们以这样的一个例子，来探索MIT自适应控制律的秘密。

* 设计一个简单的MIT自适应控制系统

![MIT-adaptive-sys](imgs/c5-MIT-adaptive-sys.svg)

Step 1：初始化$\theta(t)|_{t=0}$。

Step 2：根据性能函数$J(\Theta(t))=\frac12e(t)^2$，对参数进行梯度更新。

由上面的式子可以知道，我们只要求得$\frac{\partial e}{\partial \theta}$就可以对参数进行更新了。
我们假设传递函数 $ G(s) $
在时域下为 $ G(p) $。我们可以计算得到：
$$
\begin{aligned}
e(t)&=y_m(t)&-&y_p(t)\\&=y_r(t)k_0G(p,t)&-&y_r(t)\theta(t)\cdot k_pG(p,t)\\
\frac{\partial e(t)}{\partial \theta(t)}&=-y_r(t)k_pG(p,t)
\end{aligned}
$$
这样我们就能够完成更新了！

当然，就本题而言，聪明的你或许还发现了：
$$
\begin{aligned}
&y_rk_mG(p)&=y_m\\
%&y_r\theta k_pG(p)&=y_p\\
\rightarrow&-y_r(t)k_p\cdot G(p,t)&=-y_r(t)k_p\cdot\frac{y_m}{y_rk_m}
\\&&=-\frac{k_py_m}{k_m}
\end{aligned}
$$
我们甚至不需要把抽象的s域下的传递函数转回时域，实在是太方便了！因此，参数的更新公式可以被改写为：
$$
\begin{aligned}
\Theta\leftarrow\Theta-\gamma\frac{\partial J}{\partial \Theta}\cdot dt&=\Theta-\gamma e\cdot\frac{\partial e}{\partial \Theta}\cdot dt\\
&=\Theta+\gamma e\cdot\frac{k_py_m}{k_m}\cdot dt
\end{aligned}
$$
由于$k_p,~k_m$是常数，因此我们可以把$\gamma\frac{k_p}{k_m}$看成是一个整体的步长$\gamma$。也许这一步让你感到困惑，可以试着假设$\frac{k_p}{k_m}=10$，因此$\gamma\cdot\frac{k_p}{k_m}=10\gamma$，相当于调整因子乘上了$\frac{k_p}{k_m}$的系数，进行了一次缩放。以这个例子来说，就相当于原本设置为0.001的步长变成了0.01，我们将被缩放后的部分看作一个整体以简化程序的撰写。因此，参数的更新公式将会变为：
$$
\Theta\leftarrow\Theta+\gamma e\cdot y_m\cdot dt
$$

**延伸**：

由
$$
\begin{aligned}
\Theta(t+1)%&=\Theta(t)-\gamma e(t)\cdot\frac{\partial e(t)}{\partial \Theta(t)}\cdot dt\\
&=\Theta(t)+\gamma e(t)\cdot{y_m(t)}\cdot dt
\end{aligned}
$$
可以得知：
$$
\begin{aligned}
\Theta(t)&=\int^t \gamma e(\tau)y_m(\tau)\cdot d\tau\\
&=\Theta(t_0)+\int^t_{t_0} \gamma e(\tau)y_m(\tau)\cdot d\tau\\
\end{aligned}
$$



# 李雅普诺夫定理和自适应控制

和上文一样，如果我们把误差定义为一个与状态参数线性相关的参数，如$e(t)=cx(t)$

## 系统误差和状态观测方程的建立

让我们回顾这个系统。可以知道：
$$
e(t)=y_m(t)-y_p(t)=(k_m-k_c(t)k_p)G(p)y_r(t)
$$
我们令$k(t)=k_m-k_c(t)k_p$，可以得到：
$$
e(t)=k(t)G(p)y_r(t)
$$
我们的观测对象是误差函数。因此，我们将$k(t)y_r(t)$构造成输入u，建立系统的状态方程和观测方程：
$$
\begin{aligned}
\dot x(t) &= Ax(t)+Bu(t)\\
y(t)&=Cx(t)+Du(t)
\end{aligned}
$$
其中，$u(t)=k(t)y_r(t),~e(t)=y(t)$。它们都是**一维**的。

## 构建李雅普诺夫函数

本节内容开始前，我们强烈建议您准备好充足的草稿纸和笔。本节内容涉及的数学知识较为丰富，因此我们强烈推荐您一边阅览，一边进行推导。

> 定理：对于$\dot{x}=Ax$的系统，若其是一个稳定的系统，那么存在正定矩阵$P,~Q$，使得：$A^TP+PA=-Q$。

对于满足该定理的一个系统，我们可以构造一个李雅普诺夫函数。至于为什么会构建它作为李雅普诺夫函数，笔者功力不够，只能说前人智慧无穷了。这个李雅普诺夫函数是：
$$
V(t)=\gamma'x^T(t)Px(t)+k^2(t),~\gamma'>0
$$
如果我们能保证其对于时间的导数始终小于0，那么它将会收敛。我们来试一试对它进行求导，查找满足条件。
$$
\dot V(t)=\gamma'(\dot x^T(t)Px(t)+x^T(t)P\dot x(t))+2k(t)\dot k(t)
$$
将$\dot x(t) = Ax(t)+Bu(t)$带入$\dot x^T(t)Px(t)+x^T(t)P\dot x(t)$:
$$
\begin{aligned}
\dot V(t)&=\gamma'(\dot x^T(t)Px(t)+x^T(t)P\dot x(t))+2k(t)\dot k(t)\\
&=\gamma'\left[(Ax(t)+Bu(t))^T\cdot Px(t)+x^T(t)PA\cdot (x(t)+Bu(t))\right]+2k(t)\dot k(t)
\end{aligned}
$$
将我们构造的$u(t)=k(t)y_r(t)$带入可得：
$$
\begin{aligned}
\dot V(t)
&=\gamma'\left[(Ax(t)+Bu(t))^T\cdot Px(t)+x^T(t)P\cdot (Ax(t)+Bu(t))\right]+2k(t)\dot k(t)\\
&=\gamma'[x(t)^TAPx(t)+u^T(t)B^TPx(t)+x^T(t)PAx(t)+x^T(t)PBu(t)]+2k(t)\dot k(t)\\
&=\gamma'[x(t)^TAPx(t)+x^T(t)PAx(t)]+\gamma'[u^T(t)B^TPx(t)+x^T(t)PBu(t)]+2k(t)\dot k(t)\\
\end{aligned}
$$
这实在是太长了。力争以后更新。

最终，这个李雅普诺夫函数对时间的导函数为：
$$
\begin{aligned}
\dot V(t)
&=-\gamma'x^T(t)Qx(t)+2\gamma'\cdot x^T(t)PB\cdot k(t)y_r(t)+2\dot k(t)k(t)\\
&=-\gamma'x^T(t)Qx(t)+2k(t)[\gamma'x^T(t)PB\cdot y_r(t)+\dot k(t)]
\end{aligned}
$$
刚刚，我们证明了第一项的值$-\gamma'x^T(t)Qx(t)$是恒负的。如果我们这个计算结果全局为负，聪明的你或许发现了，有一个一定可行的解——让后面一项的计算结果为零。这样的话，该李雅普诺夫函数的导数将会全局小于0，该函数可以达到收敛。因此，欲使后面的一项计算结果为0，很显然：
$$
\begin{aligned}
\gamma'x^T(t)PB\cdot y_r(t)+\dot k(t)=0\\\rightarrow
\dot k(t)=-\gamma'y_r(t)\cdot x^T(t)PB
\end{aligned}
$$
当然，也可被写作$\dot k(t)=-\gamma'y_r(t)\cdot B^TPx(t)$。因此，当$\dot k(t)=-\gamma'y_r(t)b^TPx(t)$时，$\dot{V}(t)<0$。

## 基于该李雅普诺夫函数的自适应控制律

> 卡尔曼-雅库波维奇引理：对于下面的系统，
$$
\begin{aligned}
\dot x(t)=&Ax(t)+bv(t)\\
e(t)=&cx(t)
\end{aligned}
$$
>
>
> 如果其是完全能控能观的，那么在满足：
$$
A^TP+PA+-Q,~b^TP=c
$$
> 时，其对应的传递函数$G(s)=c(sI-A)^{-1}b$将会是严格的正实数的函数（SPR function）。

* 自适应增益定律

当$k_p$变化缓慢或者为常数的时候，由于上文中，我们定义了$k(t)=k_m-k_c(t)k_p$（注意，$k_m,~k_p$在求导时是常数），因此自适应增益$k_c$对时间的导函数满足：
$$
\begin{aligned}
k_c(t)=\frac{-k(t)+k_m}{k_p}
\\\dot k_c(t)=-\frac{\dot k(t)}{k_p}=-\frac{\gamma'}{k_p}y_r(t)B^TPx(t)=-\gamma y_r(t)B^TPx(t)
\end{aligned}
$$
方便起见，我们将$\frac{\gamma'}{k_p}$写作$\gamma$。

带入$B^TP=c,~cx(t)=e(t)$:
$$
\begin{aligned}
\dot k_c(t)=-y_r(t)e(t)\\
k_c(t)\leftarrow k_c(t)-\dot k_c(t)dt=k_c(t)+y_r(t)e(t)\cdot dt
\end{aligned}
$$


最终，李雅普诺夫自适应控制律可以被表示为：
$$
k_c(t)=k_c(t_0)+\gamma\int_{t_0}^t e(t)y_r(t)dt
$$


# 波波夫超稳定性和自适应控制

## 波波夫超稳定性

对于一个反馈系统，若其正向为线性传递，反馈为非线性传递（如下图），其中$u(t)$为输入信号，$v(t)$为反馈信号，$y(t)$为输出信号



那么当满足：
$$
\int_0^t y^T(\tau)v\tau d\tau \geq -\gamma_0^2,\gamma_0\in R
$$
时，该系统称为波波夫超稳定系统。（$\gamma_0\in R$指$\gamma_0$是实数。）

> 该定理也可以被写作：
$$
\int_0^t u^T(\tau) y(\tau)d\tau\leq \delta \cdot \sup_{0\leq\tau\leq t}||x(\tau)||
$$
> 在此基础上，在任意时刻，如果满足：
$$
||x(t)||\leq K(||x(0)||+\delta)
$$
> 那么该系统超稳定。

* 渐进超稳定

对于有界的输入，在满足波波夫超稳定性的前提下，如果其同时满足：
$$
\lim_{t\rightarrow\infty}x(t)=0
$$
则该系统也是渐进超稳定（asymptotically hyperstable）的。

## 系统被动性

如果一个系统的输入和输出满足：
$$
\left<y,u\right>=y^Tu\geq0
$$
那么这个系统是**被动的**。输入严格被动性（Input Strictly Passive, ISP）

$$
\left<y,u\right>=y^Tu\geq\epsilon u^2,\epsilon>0
$$

* 输出严格被动性（Output Strictly Passive, ISP）
$$
\left<y,u\right>=y^Tu\geq\epsilon y^2,\epsilon>0
$$

## 正实性

* 正实函数：对于任意复数$s=\sigma+j\omega$，当$\sigma\geq0$时，如果$Re[f(s)]\geq0$，那么这样的函数称为==正实函数==。
* 严格正实函数：对于任意复数$s=\sigma+j\omega$，当$\sigma\geq-\lambda~(\lambda>0)$时，如果$Re[f(s)]\geq0$，那么这样的函数称为==严格正实函数==。

## 正实传递函数

一个实传递函数（传递函数中的系数均为实数）是正实的**当且仅当**：

 1. 传递函数在右半平面没有极点；

 2. 如果传递函数在虚轴或无穷远处有极点，这些极点必须是**简单极点**；

    > 简单极点：极点的阶数是1。

 3. 传递函数的实部在虚轴上是非负的，即当$s=j\omega$时，$Re[G(j\omega)]\geq0$。


> 严格正实传递函数：满足上述（1）和（3）条件，（2）变更为传递函数在徐州没有极点或零点。



## 正实有理传递函数矩阵

正实传递函数的矩阵拓展形式。

一个有理传递函数矩阵是正实传递函数矩阵，当且仅当满足以下三个条件：

1. 当 s是实数时，G(s)的**所有元素**都是实数。

2. G(s) 的每个元素在开右半复平面（$Re(s)>0$）没有极点。如果在虚轴（$s=j\omega$ ）有极点，则这些极点必须是**简单极点**，并且对应的残差矩阵是**半正定 Hermite**矩阵。

3. 对于所有$ Re(s)>0$，只要$s $不是$ G(s)$的某个元素的极点，则以下矩阵：
$$
G(s)+G^∗(s)
$$
 是**非负定 Hermite 矩阵**。

> 严格正实有理传递函数矩阵：在满足上述三个条件下，需要额外满足：
>
> 4. $G(s)$的所有几点均在左半平面
> 5. 对于任意$\omega$， $G(j\omega)+G^*j\omega$是正定Hermite矩阵。

## 超稳定定理和自适应控制

对于系统：
$$
\begin{aligned}
\dot x(t) &= Ax(t)+Bu(t)\\
y(t)&=Cx(t)+Du(t)
\end{aligned}
$$

* *定理一*：当且仅当线性开环传递函数部分$G(s)=D+C(sI-A)^{-1}B$是**正实**的情况下，系统具有**超稳定性**；
* *定理二*：当且仅当线性开环传递函数部分$G(s)=D+C(sI-A)^{-1}B$是**严格正实**的情况下，系统具有**渐进超稳定性**。

==控制参数$ b_0 $的更新法则==：现在我们希望得到一个$b_0(t)$，从而让系统误差收敛。可能我们很难想象到可以这样进行设计，但是确实有人这样设计了一个$b_0(t)$的更新法则，它将满足波波夫超稳定：
$$
\begin{aligned}
b_0(t)=\int_0^t\Psi_1(V,\tau)d\tau+\Psi_2(V,t)+b_0(0)\\
\Psi_1(V,\tau)=\frac{k_1}{b_p}V(t)u(t)\\
\Psi_2(V,\tau)=k_2V(t)u(t)
\end{aligned}
$$

> 其中，$ k_1 $是一个常数。
>
> $\Psi_2$提供了四种选择（见课件[Chapter5-part2](../../lectures/Chapter5-ModelBasedAC/SDM5006-SIAC-Chapter5-模型参考自适应控制-Part2.pdf)的第8大页（第15小页）。这里，我们将其取作**$ \Psi_2=k_2V(t)u(t) $**，其中$ k_2 $为常数。

如何证明它呢？参考课件吧。太好了，又水了一节。



# 自适应稳定控制


## 控制系统

对于某个单输入单输出（SISO）的系统：
$$
\begin{aligned}
\dot x_p(t)&=A_px_p(t)+b_pu(t)\\
y_p(t)&=h^Tx_p(t)
\end{aligned}
$$
我们假想$A_p,~b_p$是恒定的或者缓慢变化（可以近似是为恒定或者某个时间段内恒定）的。

我们之前学过的知识告诉我们，这个系统的传递函数将会是：
$$
G_p(s)=h^T(sI-A_p)^{-1}b_p
$$
接下来，我们的参考模型被选为：
$$
\begin{aligned}
\dot x_m(t)&=A_mx_m(t)+b_mu(t)\\
y_m(t)&=h^Tx_m(t)
\end{aligned}
$$
同样，它的传递函数将会是：
$$
G_m(s)=h^T(sI-A_m)^{-1}b_m
$$
它是一个**严格正实函数**==todo：why==

同样，我们的目标是，让模型误差和系统误差趋近于0：
$$
\begin{aligned}
e(t)&=y_m(t)-y_p(t)\\
\lim_{t\rightarrow\infty} e(t)&=0
\end{aligned}
$$
在接下来的讲述中，我们只考虑$G(s)=\frac{N(s)}{D(s)}$在$D(s)$比$N(s)$阶数大1的时候的场景（例如$G(s)=\frac{s+1}{(s^2+3s+2)}$）。假设$D(s)$有n项未知系数，则$N(s)$有n-1项未知系数。

## 控制器结构

* $F_1(s)$：控制信号$u(s)$，包含n-1个可调参数
* $F_2(s)$：输出$y_p(s)$，包含n个可调参数
* $k_c$：反馈增益

## 控制参数设计

可变参数的设计为：
$$
\begin{aligned}
\theta(t)=\left[k_c, c_f^T,d_0,d_f^T\right]^T~\in~\R^{2n\times1}\\
\phi(t)=\left[y_r(t),v_1^T(t),y_p(t),v_2^T(t)\right]^T~\in~\R^{2n\times1}\\
u(t)=\theta^T(t)\phi(t)
\end{aligned}
$$




# 增益调度的自适应控制

其实就是把非线性部分线性化了，然后在控制器后接上一个反函数。因为时间有限，肯请参考课件。
