---
layout: page
title: 存疑
permalink: /ques/
toc: true
body_class: page
description: 君子终日乾乾夕惕若厉无咎
---
---
<figure style="text-align: center; margin: 20px 0;">
    <img src="/assets/img/qianli.jpg" alt="千里江山图" style="max-width: 100%; height: auto; border-radius: 2px;">
    <figcaption style="
        font-family: 'KaiTi', 'STKaiti', '楷体', serif; 
        font-size: 0.85rem; 
        color: #555; 
        margin-top: 8px;
    ">
        《千里江山图》卷 [北宋] 王希孟作
    </figcaption>
</figure>

---

<br>
* TOC
{:toc}

---

<br>

#### 2026.03.08

如何控制$\tilde{\rho}$的二阶导数  

归纳证明Krylov估计，Xie L J, Zhang X C. Ergodicity of stochastic differential equations with jumps and singular coefficients. Ann Inst
Henri Poincar´e Probab Stat, 2020, 56: 175–229


# 执行摘要

本文研究具有反射边界条件的随机微分方程（SDE）的系数光滑近似问题。假设域$D$满足一定几何条件——存在一个内部点$x_0\in D$和边界子集$H\subset\partial D$使得对$\partial D\setminus H$上的任意点$x$都有$\langle x-x_0,n(x)\rangle\le0$，并且存在$g\in C^2_b(\bar D)$使得$\langle\nabla g(x),n(x)\rangle\ge1$在$H$上成立。在此条件下，对有界Lipschitz且满足一致椭圆条件的系数$b_t,\sigma_t$，反射SDE

\[dX_t=b_t(X_t)dt+\sigma_t(X_t)dW_t+n(X_t)dl_t\]

具有全局唯一的解$(X_t,l_t)$【21†L882-L884】。对系数进行空间光滑化得到$b^n_t,\sigma^n_t$，相应的反射SDE解记作$X^n_t$，则可以证明当$n\to\infty$时，$X^n_t$在路径空间上收敛到原SDE的解$X_t$【18†L790-L794】。由此对任意紧支撑的$C^\infty$函数$f$，过渡半群满足$P^n_{s,t}f(x)=\mathbb{E}[f(X^n_t)\mid X^n_s=x]\to \mathbb{E}[f(X_t)\mid X_s=x]=P_{s,t}f(x)$。主要论证包括：利用Skorokhod问题构造反射SDE解的存在唯一性（参见Lions–Sznitman, Saisho, Słomiński等工作），建立系数近似下解的紧性与稳定性（鞅问题和Skorokhod映射连续性），以及利用生成元一致性或鞅表征导出半群收敛。下文将详细阐明假设、关键引理与证明思路，并给出必要的估计和论证。

## 问题陈述与假设

我们考虑欧几里得空间$\mathbb{R}^d$中有界域$D$及其边界$\partial D$。给定点$x_0\in D$及边界上的子集$H\subset\partial D$，假设对$\partial D\setminus H$上任意$x$都有
\[
\langle x - x_0,\, n(x)\rangle \le 0,
\]
其中$n(x)$为$\partial D$上的单位*内*法向量（指向域内部）。此外，假设存在函数$g\in C^2_b(\bar D)$使得
\[
\langle \nabla g(x),\, n(x)\rangle \ge 1\quad\text{在 }H\text{上成立},
\]
即$g$沿边界$H$方向的法向导数不小于1。这组几何/可行性条件是Skorokhod问题的常用假设，保证了反射映射的唯一性和存在性【16†L25-L33】【21†L882-L884】。系数假设为：漂移$b_t(x)$、扩散$\sigma_t(x)$是对$t\in[0,T]$的进程，空间上满足Lipschitz连续、有界，并且$\sigma_t\sigma_t^*$一致椭圆（即$\sigma_t\sigma_t^*\ge\lambda I>0$）。由此经典结果保证**反射SDE**有全局唯一解（**强解**）$(X_t,l_t)$，其中$l_t$为累积的边界局部时间【21†L882-L884】。我们取初始时刻$s$及初始位置$x\in D$固定。对上述$b_t,\sigma_t$作空间卷积光滑近似，得光滑系数序列$b^n_t,\sigma^n_t$，仍然满足相似的Lipschitz和椭圆性质（保留有界性与下界$\lambda$）。设$X^n_t$为对应系数下的反射SDE解，对应的跃迁半群$P^n_{s,t}f(x)=\mathbb{E}[f(X^n_t)\mid X^n_s=x]$。目标是证明：对于任意紧支撑的$C^\infty$函数$f$（且支持在$D$的内部），当$n\to\infty$时有
\[
P^n_{s,t}f(x)\to P_{s,t}f(x)
\]
对所有$x\in D$成立。该结论归结为证明路径层面$X^n_t\to X_t$，从而对有界连续函数$f$，$\mathbb{E}[f(X^n_t)]\to\mathbb{E}[f(X_t)]$。 

## 反射SDE的存在性与唯一性

在上述条件下，反射SDE
\[
X_t = x + \int_s^t b_r(X_r)dr + \int_s^t \sigma_r(X_r)dW_r + \int_s^t n(X_r)\,dl_r
\]
称为Skorokhod问题的解。其中$(X_t,l_t)$满足：$X_t\in\bar D$，$l_t$为增加过程，仅在$X_t\in\partial D$时增长，并且积分方程和边界条件$\int_0^T\mathbf{1}_{\{X_r\notin\partial D\}}dl_r=0$成立。经典理论（见Lions–Sznitman (1984)【2†L33-L41】、Saisho (1987)【12†L207-L215】、Słomiński (1993)【21†L882-L884】）表明：如果域$D$满足上述“可行性”条件（一般化的星型/凸性条件(A),(B)）且$b,\sigma$空间Lipschitz，则反射SDE有且仅有一个强解【21†L882-L884】。特别，Słomiński 定理5指出：在条件(A),(B)下，如果$b,\sigma$ Lipschitz且有界，则反射SDE存在唯一强解$(X_t,l_t)$【21†L882-L884】。这里的条件(A),(B)实质上对应题设的几何假设，保证Skorokhod映射的良好性质；Liouville-Sznitman (1984)也是类似的结论，但要求域可近似为光滑凸域【2†L33-L41】。因此我们可以使用这一存在唯一性结果，断言半群$P_{s,t}$定义良好。

## 系数近似与解的稳定性

接下来考虑系数近似过程。设$b^n,\sigma^n$为$b,\sigma$的空间光滑序列，且一致Lipschitz和一致椭圆常数不变。对相同的初始数据和同一个布朗运动，我们得到近似SDE解$(X^n_t,l^n_t)$。要证明$X^n\to X$，可以采用以下思路：

- **紧性**：由于$b^n,\sigma^n$有界且Lipschitz，一致满足线性增长条件，由标准估计可知$X^n_t$具有统一的矩界限（如：$E[\sup_{s\le t}|X^n_t|^p]<C$）。利用Aldous紧性判据或Meyer–Zheng紧性判据，可证明$\{X^n\}$在Skorokhod空间中是紧的。Słomiński 在定理4(i)中也指出：在系数序列统一条件下，$(X^n,K^n)$（包括局部时间）是弱紧的【18†L790-L794】。

- **Skorokhod映射的连续性**：实质上$X^n$和$X$满足$X^n=Y^n+K^n,\,X=Y+K$，其中$Y^n_s = x + \int_s^\cdot b^n_r(X^n_r)dr + \int_s^\cdot \sigma^n_r(X^n_r)dW_r$，$Y$类似。因为$b^n\to b,\ \sigma^n\to\sigma$一致收敛，以及$X^n$紧致，可以利用稳定性定理（Słomiński 定理4(i)【18†L790-L794】）或Skorokhod问题的Lipschitz特性推断，若$Y^n\to Y$（易得）则任何极限点$(\widetilde X,\widetilde K)$满足反射SDE的解的定义，从而是$X$的解。更具体地，由于强解唯一，引理保证$X^n\to X$（在弱收敛甚至概率收敛意义下）【18†L790-L794】【21†L882-L884】。

- **估计与鞅问题**：可借助Itô引理和停时技术给出收敛速度估计。例如令$\Delta_t=X^n_t-X_t$，应用Itô公式估计$|\Delta_t|^2$，结合$b^n-b$和$\sigma^n-\sigma$的小量以及局部时间项的处理，可推出$E[\sup_{s\le t}|\Delta_t|^2]\to0$。Słomiński 的定理3及其推论给出了类似的估计，即$E\sup|\Delta_t|^2\le C\{E\sup|b^n-b|^2+E\sup|\sigma^n-\sigma|^2\}$ (忽略技术性细节)【15†L66-L74】。这些估计辅以Gronwall引理可正式证明收敛。

综上，借助上述紧性和Skorokhod图像性质，可以得到：$X^n\to X$，局部时间$l^n\to l$（在路径空间弱收敛或概率意义）【18†L790-L794】【21†L882-L884】。这里关键利用了(UT)条件下的随机积分极限定理和反射问题的解唯一性。若需要，也可应用Martingale问题方法：近似过程满足由生成元$L^n_t$定义的鞅问题，极限点必满足原始生成元$L_t$对应的鞅问题，凭唯一性也可得收敛。

## 半群收敛证明

对任意紧支撑的$C^\infty$函数$f$，有界且连续，可直接由概率收敛推出期望收敛：由于$X^n\to X$在分布意义上成立，对固定初始点$x$，由连续映射定理有$f(X^n_t)\to f(X_t)$依分布（因$f$连续且紧支撑，$f$有界）；再加上$f$有界，利用有界收敛定理得到$\mathbb{E}[f(X^n_t)]\to\mathbb{E}[f(X_t)]$。这正是半群收敛所需结论，即
\[
P^n_{s,t}f(x)=E_x[f(X^n_t)]\ \longrightarrow\ E_x[f(X_t)]=P_{s,t}f(x).
\]
注意紧支撑的假设确保$f$远离边界，局部时间项对$f(X_t)$的贡献为零，使得边界效应不影响上述推理。若进一步希望半群收敛的更强结果（如一致收敛），可以结合生成元一致收敛的理论（Trotter-Kato定理）加以处理，但对紧支撑光滑函数通常无需如此深入。因为$X^n\to X$在全局一致收敛后，半群在任意紧子集上一致收敛也是成立的。

下表总结了各关键步骤的假设与结论：  

| 步骤 | 主要假设 | 结论 | 参考文献 |
|:---|:---|:---|:---|
| 反射SDE存在唯一性 | 域$D$满足(A),(B)几何条件；$b,\sigma$有界Lipschitz，一致椭圆 | 存在唯一强解$(X,l)$，定义半群$P_{s,t}$【21†L882-L884】 | Słomiński (1993) Thm.5【21†L882-L884】 |
| 解的稳定性 | 同(上)，且近似系数$b^n\to b,\ \sigma^n\to\sigma$一致 | 解$(X^n,l^n)\to(X,l)$（紧性与Skorokhod映射连贯性）【18†L790-L794】 | Słomiński (1993) Thm.4(i)【18†L790-L794】 |
| 半群收敛 | $f\in C^\infty_c(D)$有界连续；$X^n\to X$ | $P^n_{s,t}f(x)=E[f(X^n_t)]\to E[f(X_t)]=P_{s,t}f(x)$ | 本文论证 |

```mermaid
flowchart LR
    A[域$D$满足(A),(B)几何条件] --> B[反射SDE存在唯一强解【21†L882-L884】]
    B --> C[构造系数近似$b^n,\sigma^n$]
    C --> D[解的稳定性: $(X^n,l^n)\to (X,l)$【18†L790-L794】]
    D --> E[半群收敛: $P^n_{s,t}f\to P_{s,t}f$]
```

## 边界行为与技术细节

- **边界条件的角色**：所给条件保证了域在$H$上“外凸”且在其余边界朝向点$x_0$“凹陷”或平滑，这些都是经典文献中的可行性假设【16†L25-L33】。函数$g$的存在可看作是确保在$H$上反射向内的辅助工具（类似障碍函数），对应于Saisho(1987)或Frankowska等人的可行性技术。在我们的论证中，这些假设确保了Skorokhod反射机制不会失败，从而使得局部时间$l_t$定义合理且与半群分析兼容。
- **一致椭圆性**：该条件保证了偏微分方程对应的Neumann问题解的正则性和稳定性，也使得随机动理学和偏微分方程之间的联系更直接。尽管本方案主要依赖概率方法，但一致椭圆使得诸如Kolmogorov前向方程存在光滑解，从而间接支持半群收敛的PDE论证。
- **函数空间**：我们对紧支撑$C^\infty$函数进行了证明，可通过密度和插值拓展到更一般的空间（如有界连续函数）。但由于边界反射，若$f$在边界附近不为零，则需要进一步考察局部时间项的贡献（在本情形$f$紧支撑远离边界，故问题得以规避）。
- **生成元方法**：可视为补充论证：令$L^n_t$和$L_t$分别为近似和原始过程的生成元（含Neumann边界条件）。可以证明在紧支撑函数上$L^n_t f\to L_t f$，进而由Stroock–Varadhan或Ethier–Kurtz理论推出相应的半群级收敛（参见【12†L207-L215】有关鞅问题的讨论）。

## 结论

综上所述，在给定的域几何条件(A),(B)和$b,\sigma$满足有界Lipschitz及一致椭圆的假设下，反射SDE存在唯一强解，并且该解对系数进行空间卷积近似时是稳定的。利用上述稳定性，我们证明了近似系数对应的马尔可夫半群在任意紧支撑光滑函数上收敛到原始半群。方法核心为Skorokhod问题和强解唯一性保证路径层面的收敛，从而导出半群收敛。未来的推广可考虑宽松的边界条件或更弱的系数假设，以及探讨收敛速率和在更大函数空间上的收敛性质。
