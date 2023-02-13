---
created: 2023-01-04
type: Literature Note Template
tag:
---

> [!success] 要点
> - 信息熵表示随机变量的"惊讶程度"，与发生概率成反比，满足定义的函数只有对数函数
> - KL 散度表示两随机变量分布的近似程度，恒大于 0，当且仅当分布相同等于 0 ，但不是一种距离，不满足对称性
> - 互信息是一种特殊的 KL 散度（ $p(\mathbf{x}, \mathbf{y})$ 和 $p (\mathbf{x}) p (\mathbf{y})$ ），用来衡量两随机变量独立程度

^dca775


## 1. 随机变量的信息
如果我们想衡量一个随机变量 $x$，当我们观测到其实际值的时候所包含的信息 $h(x)$，需要满足三点[^1]：
1. $h(x)>0$, 人为规定的结果
2. __如果某随机变量发生概率越低，它却发生了，这时候包含的信息越多；反之一个不太可能的事情没有发生，实际包含的信息越少__, 所以 $h(x)$ 是 $p(x)$ 的单调递减函数，即 $$
h(x)=f(p(x))
$$ 其中 $f$ 单调递减
3. 对于不相关随机变量 $x,y$，两事件同时发生带来的信息应该等于各自信息量之和，所以有 $h(x, y)=h(x)+h(y)$，即$$
\begin{aligned}
& h(x, y)=f(p(x, y))=f(p(x) p(y)) \\
& h(x)+h(y)=f(p(x))+f(p(y))
\end{aligned}
$$

综合以上三点，可以证明[^2]
$$
\left\{\begin{array}{l}
f(a \cdot b)=f(a)+f(b) \\
f(a) \downarrow a \in(0,+\infty) \\
f(a)>0
\end{array}\right.
$$
满足上式的 $f(x)$ 只有对数函数，所以定义一个随机变量的的信息为
$$
h(x)=-\log _2 p(x)
$$
信息熵（entropy of the random variable）指的是随机变量包含信息的期望
$$
\mathrm{H}[x]=E(h(x))-\sum_x p(x) \log _2 p(x)=-\int p(\mathbf{x}) \ln p(\mathbf{x}) \mathrm{d} \mathbf{x}
$$

^a3f7eb

> [!tip] 注意
> $p(x)$ 可以等于 0，此时定义 $p(x) \ln p(x)=0$

## 2. 条件熵
条件熵描述了在已知第二个随机变量 $x$ 已知条件下 $y$ 所带来的信息

$$
\mathrm{H}[\mathbf{y} \mid \mathbf{x}]=\int p(y \mid x) \ln p(y \mid x) d y \int p(x) d x=-\iint p(\mathbf{y}, \mathbf{x}) \ln p(\mathbf{y} \mid \mathbf{x}) \mathrm{d} \mathbf{y} \mathrm{d} \mathbf{x}
$$

可以证明

$$
\mathrm{H}[\mathbf{x}, \mathbf{y}]=\mathrm{H}[\mathbf{y} \mid \mathbf{x}]+\mathrm{H}[\mathbf{x}]
$$

## 3. 相对熵和互信息
考虑某个隐含的分布 $p(\mathbf{x})$，我们用分布 $q(\mathbf{x})$ 来近似，两个分布的 KL 散度（相对熵）定义为 
$$
\begin{aligned}
\mathrm{KL}(p \| q) & =-\int p(\mathbf{x}) \ln q(\mathbf{x}) \mathrm{d} \mathbf{x}-\left(-\int p(\mathbf{x}) \ln p(\mathbf{x}) \mathrm{d} \mathbf{x}\right) \\
 & =\int p(\mathbf{x}) \ln p(\mathbf{x}) \mathrm{d} \mathbf{x}-\int p(\mathbf{x}) \ln q(\mathbf{x}) \mathrm{d} \mathbf{x} \\
& =\int p(\mathbf{x}) \ln \left\{\frac{p(\mathbf{x})}{q(\mathbf{x})}\right\} \mathrm{d} \mathbf{x} .
\end{aligned}
$$
可以证明[^3]，**KL 散度大于等于 0 当且仅当 $p(\mathbf{x})=q(\mathbf{x})$ 成立**，

这样一看 KL 散度类似一个距离，实际并不是，因为不满足对称性，只是用来衡量两种分布的近似程度

### 相对熵与极大似然估计
假设 $q(\mathbf{x} \mid \boldsymbol{\theta})$ 是一个参数为 $\boldsymbol{\theta}$ 的近似分布，$p (\mathbf{x})$ 是隐含的实际分布，上式其实是两个期望的差值，而期望可以近似为样本的平均值，所以两个分布的 KL 散度为
$$\mathrm{KL}(p \| q) \simeq \frac{1}{n} \sum_{n=1}^N\left\{-\ln q\left(\mathbf{x}_n \mid \boldsymbol{\theta}\right)+\ln p\left(\mathbf{x}_n\right)\right\}$$
其中 $p\left(\mathbf{x}_n\right)$ 是参数无关的，RHS 就是似然函数，所以**最小化 KL 散度等价于最大化似然函数**

## 4. 互信息
考虑两个随机变量 $\mathbf{x}$ 和 $\mathbf{y}$ ，如果两者独立，则说明 $p(\mathbf{x}, \mathbf{y})=p(\mathbf{x}) p(\mathbf{y})$，如果计算等号两边的 KL 散度，就可以计算这两个随机变量的独立性程度，则有
$$
\begin{aligned}
\mathrm{I}[\mathbf{x}, \mathbf{y}] & \equiv \mathrm{KL}(p(\mathbf{x}, \mathbf{y}) \| p(\mathbf{x}) p(\mathbf{y})) \\
& =-\iint p(\mathbf{x}, \mathbf{y}) \ln \left(\frac{p(\mathbf{x}) p(\mathbf{y})}{p(\mathbf{x}, \mathbf{y})}\right) \mathrm{d} \mathbf{x} \mathrm{d} \mathbf{y}
\end{aligned}
$$
为了计算方便，一般计算为
$$
\mathrm{I}[\mathbf{x}, \mathbf{y}]=\mathrm{H}[\mathbf{x}]-\mathrm{H}[\mathbf{x} \mid \mathbf{y}]=\mathrm{H}[\mathbf{y}]-\mathrm{H}[\mathbf{y} \mid \mathbf{x}] \text {. }
$$
所以互信息也可以理解为已知 $\mathbf{y}$ 的条件下，$\mathbf{x}$ 带来的信息减少程度，也就是**信息增益（Information gain）**（$\mathbf{y}$ 和 $\mathbf{x}$ 独立时已知一方对另一方信息减少程度为 0）

## 参考文献

[^1]:  [[Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf#page=68]]
[^2]: https://math.stackexchange.com/questions/598413/fxy-fxfy-proof
[^3]: [[Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf#page=76]]