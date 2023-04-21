---
title: 'Josh''s Notes: 最优阵列处理（Part 1.3 —— 均匀加权线阵）'
mathjax: true
comments: true
copyright: true
toc:
  enable: true
  number: true
  wrap: true
  expand_all: true
  max_depth: 4
tags:
  - 阵列信号处理
  - 均匀加权线阵
categories:
  - - Josh 的学习笔记
    - 最优阵列处理
    - 阵列和空域滤波器
abbrlink: aa32ec76
date: 2023-04-20 19:34:47
---

# 均匀加权线阵的频率-波数响应函数

&emsp;&emsp;现在把注意力集中到均匀加权的情况，即

$$\begin{equation}
  w_n = \frac{1}{N}, \, n = 0,1,\cdots,N-1
\end{equation}$$

$$\begin{equation}
  \vec{w} = \frac{1}{N} \vec{1}
\end{equation}$$

其中 $\vec{1}$ 是 $N \times 1$ 维的单位矢量，则在 $\psi$ 空间的频率-波数函数可以写成（利用等比级数的求和公式）

$$\begin{equation}
  \begin{aligned}
    \vec{\varUpsilon}_\psi(\psi) &= \frac{1}{N} \sum_{n=0}^{N-1}  e^{j \left(n - \frac{N-1}{2}\right)\psi} \\
    &= \frac{1}{N} e^{-j \left(\frac{N-1}{2}\right)\psi} \sum_{n=0}^{N-1} e^{j n \psi} \\
    &= \frac{1}{N} e^{-j \left(\frac{N-1}{2}\right)\psi} \left[ \frac{1-e^{jN\psi}}{1-e^{j\psi}} \right]
  \end{aligned}
\end{equation}$$

或（利用欧拉公式）

$$\begin{equation}
  \vec{\varUpsilon}_\psi(\psi) = \frac{1}{N} \frac{\sin\left( N \frac{\psi}{2} \right)}{\sin\frac{\psi}{2}}
\end{equation}$$

<!-- more -->

观察到，

- 当 $N$ 是奇数时，$\vec{\varUpsilon}_\psi(\psi)$ 是周期函数，周期为 $2\pi$；
- 当 $N$ 为偶数时，波瓣在 $\pm 2 \pi$、$\pm 6 \pi$ 处的值为负值，周期为 $4 \pi$；
- 对任意的 $N$，$\left|\vec{\varUpsilon}_\psi(\psi)\right|$ 的周期为 $2 \pi$。

当 $N = 11$  时， $\vec{\varUpsilon}_\psi(\psi)$ 和 $\psi$ 的关系在[图 1-3-1](#fig.1-3-1) 中给出。[图 1-3-2](#fig.1-3-2) 给出了 $\left|\vec{\varUpsilon}_\psi(\psi)\right|$，单位为 dB, 其中

$$\begin{equation}
  \vec{\varUpsilon}_\mathrm{dB}(\psi) = 10 \log_{10} \left|\vec{\varUpsilon}_\psi(\psi)\right|^2
\end{equation}$$

<a id="fig.1-3-1"></a>

![图 1-3-1 $\vec{\varUpsilon}(\psi): \psi = \frac{2\pi}{\lambda} d \cos\theta, N=11$](https://josh-blog-1257563604.cos.ap-beijing.myqcloud.com/img/2023-04-20-josh-oap-part-1-3/2023-04-20-josh-oap-part-1-3-010-FrequencyWavenumberResponseFunction.svg){width=700px}

<a id="fig.1-3-2"></a>

![图 1-3-2 用 dB 表示 $\left|\vec{\varUpsilon}(\psi)\right|$](https://josh-blog-1257563604.cos.ap-beijing.myqcloud.com/img/2023-04-20-josh-oap-part-1-3/2023-04-20-josh-oap-part-1-3-020-FrequencyWavenumberResponseFunctionInDB.svg){width=700px}

若不指定 $\vec{w}$ 的类型, 则 $\vec{\varUpsilon}_\psi(\psi)$ 是复数，所以相位也应该画出来。但是，均匀加权线阵具有对称性，因此得到的频率-波数响应是实函数。

&emsp;&emsp;也可以用 $k_z$ 来表示频率-波数响应

$$\begin{equation}
  \vec{\varUpsilon}(\omega:k_z) = \frac{1}{N} \frac{\sin\left( N k_z \frac{d}{2} \right)}{\sin \left(k_z\frac{d}{2}\right)}
\end{equation}$$

这里 $\vec{\varUpsilon}(\omega:k_z)$ 是周期函数，周期为 $2\pi/d$。

&emsp;&emsp;注意，响应函数仅依赖于波数分量 $k_z$, 是 $k_z$ 的周期函数，间隔为 $2\pi/d$，这是线性阵列的一维特性导致的，所以该阵列仅能分析在 $k_z$ 方向上投影的波数分量。

# 均匀加权线阵的波束方向图

&emsp;&emsp;均匀加权线阵的波束方向图的波束方向图为

$$\begin{align}
  &\theta 空间: && B_\theta(\theta) = \frac{1}{N} \frac{\sin\left(\frac{N}{2} \cdot \frac{2\pi}{\lambda} \cos \theta \cdot d \right)}{\sin \left( \frac{1}{2} \cdot \frac{2\pi}{\lambda} \cos\theta \cdot d\right)}, \quad 0 \leqslant \theta \leqslant \pi \\

  &u 空间: && B_u(u) = \frac{1}{N} \frac{\sin\left(\frac{N \pi d}{\lambda} u \right)}{\sin \left( \frac{N d}{\lambda} u\right)}, \quad -1 \leqslant u \leqslant 1 \label{BeamPatternOfUWLAInDirectionCosineDomain} \\

  &\psi 空间:  &&B_\psi(\psi) = \frac{1}{N} \frac{\sin\left(N\frac{\psi}{2}\right)}{\sin \left( \frac{\psi}{2} \right)}, \quad -\frac{2\pi d}{\lambda} \leqslant \psi \leqslant \frac{2\pi d}{\lambda}
\end{align}$$

其中定义域分别为 $0 \leqslant \theta \leqslant \pi$、$-1 \leqslant u \leqslant 1$ 和 $-\displaystyle\frac{2\pi d}{\lambda} \leqslant \psi \leqslant \frac{2\pi d}{\lambda}$，称为**{% label primary @可视区域（visible region） %}**。

&emsp;&emsp;函数 $B_u(u)$ 和 $B_\psi(\psi)$ 有时称为**{% label primary @阵列因子（Array Factor） %}**。当我们研究非全向性阵元时，将发现这个量的重要性。

&emsp;&emsp;[图 1-3-3](#fig.1-3-3) 给出了 $B_\theta(\theta)$ 的极坐标形式，单位为 dB。如果在三维空间画出波束方向图，在[图 1-3-3](#fig.1-3-3) 中的图将对应沿着任意方位角 $\theta$ 切割得到的方向图。[图 1-3-4](#fig.1-3-4) 给出了波束方向图的幅度和不同变量之间的关系。

<a id="fig.1-3-3"></a>

![图 1-3-3 在极坐标系中画出 $B_\theta(\theta)$](https://josh-blog-1257563604.cos.ap-beijing.myqcloud.com/img/2023-04-20-josh-oap-part-1-3/2023-04-20-josh-oap-part-1-3-030-PloarPlotOfBeamPatternInAngleSpace.svg){width=600px}

<a id="fig.1-3-4"></a>

![图 1-3-4 $d = \lambda/2, N=10$，线阵的 $\left|\vec{\varUpsilon}_\psi(\psi)\right|$](https://josh-blog-1257563604.cos.ap-beijing.myqcloud.com/img/2023-04-20-josh-oap-part-1-3/2023-04-20-josh-oap-part-1-3-040-AbsOfWFRFForALinearArray.svg){width=700px}

&emsp;&emsp;尽管这是一个简单的例子，但可以用来展示线性阵列的一些重要特征。第一组重要特
征描述了波束方向图的参数。

# 波束方向图的参数

1. 3dB 带宽（半功率波束宽度，half-power beamwidth，HPBW）
2. 到第一零点的距离（这个距离的两倍称为 $BW_{NN}$）
3. 到第一旁瓣的距离
4. 第一旁瓣的高度
5. 其余零点的位置
6. 旁瓣衰减的速率
7. 栅瓣（Grating lobes）

## 3 dB 带宽

为了说明前两个参数，考虑在[图 1-3-5](#fig.1-3-5) 中给出的原点附近的波束方向图。

<a id="fig.1-3-5"></a>

![图 1-3-5 波束方向图的主波束](https://josh-blog-1257563604.cos.ap-beijing.myqcloud.com/img/2023-04-20-josh-oap-part-1-3/2023-04-20-josh-oap-part-1-3-050-MainLobeOfBeamPattern.svg){width=700px}

&emsp;&emsp;3dB 波束宽度是波束宽度的一个度量。定义为对应 $\left| B_u(u) \right|^2 = 0.5$ 或 $\left| B_u(u) \right| = 1/\sqrt{2}$ 的点。可以通过使式 $\eqref{BeamPatternOfUWLAInDirectionCosineDomain}$ 中的 $B_u(u)$ 的值等于 $1/\sqrt{2}$ 来确定出在 $u$ 空间的半功率点。当 $N$ 增加时，计算这个值，我们发现，对于 $N\geqslant 10$, 通过解下面的方程可以得到一个很好的近似值：

$$\begin{equation}
  \frac{\pi N d}{\lambda} u = 1.4
\end{equation}$$

则

$$\begin{equation}
  \frac{\Delta u_1}{2} = 1.4 \frac{\lambda}{\pi N d}
\end{equation}$$

或

$$\begin{equation} \label{DefinitionOfHPBW}
 \Delta u_1 = 0.891 \frac{\lambda}{N d}
\end{equation}$$

我们把这个间隔称为**{% label primary @半功率波束宽度（half-power beamwidth，HPBW） %}**。当 $N$ 增加时，式 $\eqref{DefinitionOfHPBW}$ 中的系数稍稍减小。对于 $N > 30$，$0.886 \lambda/Nd$ 是一个更好的近似表达式。

&emsp;&emsp;[表 1-3-1](#table.1-3-1) 中列出了不同空间内 HPBW 的表达式。

<a id="table.1-3-1"></a>

|空间| 任意 $d$ | $d=\lambda/2$ |
| :--: | :------: | :------: |
| $u$ | $0.891 \frac{\lambda}{Nd}$ | $1.782 \frac{1}{N}$ |
| $\bar{\theta}$[^] | $2\sin^{-1} \left( 0.446 \frac{\lambda}{Nd} \right)$ | $2\sin^{-1} \left( 0.891 \frac{1}{N} \right)$ |
| 较小的 $\bar{\theta}$ | $\simeq 0.891 \frac{\lambda}{Nd}$ radians <br> $\simeq 51.05 \frac{\lambda}{Nd}$ degrees | $\simeq 1.782 \frac{1}{N}$ radians <br> $\simeq 102.1 \frac{1}{N}$ degrees |
| $\psi$ | $0.891 \frac{2\pi}{N}$ | $0.891 \frac{2\pi}{N}$ |
| $k_z$ | $0.891 \frac{2\pi}{dN}$ | $1.782 \frac{2\pi}{\lambda N}$ |

## 到第一零点的距离

&emsp;&emsp;方向图的零点出现在当 $B_u(u)$ 的分子为零而分母不为零时，即

$$\begin{equation}
  \sin \left( \frac{\pi N d}{\lambda} u \right) = 0
\end{equation}$$

成立的条件为

$$\begin{equation}
  \frac{\pi N d}{\lambda} u = m\pi, \quad m = 1,2,\cdots
\end{equation}$$

则出现零点需要满足下面的两个条件：

$$\begin{equation}
  u = m \frac{\lambda}{Nd}, \quad m = 1,2,\cdots
\end{equation}$$

且

$$\begin{equation}
  u \ne m \frac{\lambda}{d}, \quad m = 1,2,\cdots
\end{equation}$$

则第一个零点的位置为 $\lambda/Nd$, 且

$$\begin{equation}
  \Delta u_2 = 2 \frac{\lambda}{Nd}
\end{equation}$$

我们把 $\Delta u_2$ 称为零点-零点波束宽度（null-to-null beamwidth），并表示为 $BW_{NN}$ 。 $BW_{NN}$ 的一半是到第一零点的距离 ($0.5 BW_{NN}$) 。这个量衡量了阵列分辨两个不同平面波的能力，也称为{% label primary @瑞利限（Rayleigh resolution limit） %}。如果第二个波束方向图的峰值在第一个波束方向图的第一零点之外（间隔 $\geqslant \Delta u_2 / 2$ ）, 则我们认为这两个平面波是可以分辨的。在后面，我们将研究一个阵列的分辨能力的统计性度量。

&emsp;&emsp;注意到线阵在方位角方向（$\varphi$）没有分辨能力，因为该阵列在 $x$ 和 $y$ 方向上没有扩展。我们将在后面详细讨论分辨率的问题。

&emsp;&emsp;[表 1-3-1](#table.1-3-1)中列出了在各个不同空间表示出的 $BW_{NN}$。

<a id="table.1-3-2"></a>

|空间| 任意 $d$ | $d=\lambda/2$ |
| :--: | :------: | :------: |
| $u$ | $2 \frac{\lambda}{Nd}$ | $\frac{4}{N}$ |
| $\bar{\theta}$[^] | $2\sin^{-1} \left( \frac{\lambda}{Nd} \right)$ | $2\sin^{-1} \left( \frac{2}{N} \right)$ |
| 较小的 $\bar{\theta}$ | $\simeq 2 \frac{\lambda}{Nd}$ radians | $\simeq \frac{4}{N}$ radians |
| $\psi$ | $ \frac{4\pi}{N}$ | $\frac{4\pi}{N}$ |
| $k_z$ | $\frac{4\pi}{dN}$ | $\frac{8\pi}{\lambda N}$ |