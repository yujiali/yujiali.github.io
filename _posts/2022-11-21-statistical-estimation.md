---
layout: blog_post
title: 统计估计的一些结论
---

在机器学习里常常会需要估计模型的参数，或者更广泛的，从数据中估计某些变量的值。需要多少数据，才能把这些参数估计到什么样的精确程度，是机器学习理论里面最基础的问题之一。这篇博文简单回顾一下一些比较经典的结论。

首先，几个基本的tail-probability不等式，对于任意$$\epsilon > 0$$：

* Markov不等式：对于任意非负$$X$$，$$p(X \ge \epsilon) \le \frac{\mathbb{E}[X]}{\epsilon}$$。
* Chebyshev不等式：$$p(\lvert X - \mathbb{E}[X]\rvert \ge \epsilon) \le \frac{\mathbb{V}[X]}{\epsilon^2}$$。

之所以叫tail-probability，是因为这些不等式刻画的是概率分布在$$\epsilon$$范围之外的样子。这两个不等式成立的条件仅需要期望$$\mathbb{E}[X]$$以及方差$$\mathbb{V}[X]$$存在，不需要任何其他条件，是适用范围最广的概率不等式。另一方面，因为它们的普适性，这两个不等式给出的bound也尝尝比较宽松，要得到更精确的结果则需要引入一些假设，得到更紧的bound。

---

证明：

$$
p(X \ge \epsilon) = \int_{\epsilon}^{\infty} p(x) dx = \frac{1}{\epsilon} \int_{\epsilon}^{\infty} \epsilon p(x) dx \le \frac{1}{\epsilon} \int_{\epsilon}^{\infty} x p(x) dx \le \frac{1}{\epsilon} \int_0^\infty x p(x)dx = \frac{\mathbb{E}[X]}{\epsilon}
$$

此即Markov不等式，注意这里我偷懒用$$p$$表示了概率函数和概率密度函数，但从上下文应能看出适用的情况。

对于Chebyshev不等式，我们有

$$
p(\lvert X - \mathbb{E}[X]\rvert \le \epsilon) = p((X - \mathbb{E}[X])^2 \le \epsilon^2)
$$

套用Markov不等式，得到

$$
p((X - \mathbb{E}[X])^2 \le \epsilon^2) \le \frac{\mathbb{E}[(X - \mathbb{E}[X])^2]}{\epsilon^2} = \frac{\mathbb{V}[X]}{\epsilon^2}
$$

---

用这两个不等式已经可以得到一些有用的结果。例如，假定我们要估计某一个参数$$\mu$$，我们有对$$\mu$$的$$n$$个i.i.d.的观测$$X_1, ..., X_n$$，那么我们可以从这$$n$$个观测中计算一个$$\mu$$的估计

$$
\hat{\mu} = \frac{1}{n}\sum_{i=1}^n X_i
$$

那么我们有

$$
\mathbb{E}[\hat{\mu}] = \frac{1}{n}\sum_{i=1}^n \mathbb{E}[X_i] = \frac{1}{n} n\mu = \mu
$$

因而$$\hat{\mu}$$是一个unbiased estimator，同时

$$
\mathbb{V}[\hat{\mu}] = \frac{1}{n^2} \sum_{i=1}^n \mathbb{V}[X_i] = \frac{\sigma^2}{n}
$$

其中变量$$X_i$$的方差$$\mathbb{V}[X_i] = \sigma^2$$。带入Chebyshev不等式，可得

$$
p(\lvert \hat{\mu} - \mu \rvert \ge \epsilon) \le \frac{\mathbb{V}[\hat{\mu}]}{\epsilon^2} = \frac{\sigma^2}{n\epsilon^2}
$$

这个结果说明，估计量$$\hat{\mu}$$到真正的$$\mu$$的误差大于$$\epsilon$$的概率最多为$$\frac{\sigma^2}{n\epsilon^2}$$，这个上界和$$\sigma^2$$成正比，和$$n$$成反比。因此，$$X$$的方差越小，$$\hat{\mu}$$越容易将$$\mu$$估计准确，得到的观测$$n$$越多，也越容易估计的更准确。不过Chebyshev不等式给出的上界$$\frac{\sigma^2}{n\epsilon^2}$$还是比较松的，引入其他的假设之后这个上界可以有显著的改进。

例如，中心极限定理(Central Limit Theorem, CLT)告诉我们当$$n\rightarrow \infty$$时，$$\frac{\hat{\mu} - \mu}{\sigma/\sqrt{n}}$$收敛于一个标准正态分布，因此

$$
\begin{align*}
p\left(\left\vert \frac{\hat{\mu} - \mu}{\sigma/\sqrt{n}} \right\vert \ge \epsilon\right) &\approx 2 \int_{\epsilon}^\infty \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{x^2}{2}\right) dx \\
&\le 2 \int_\epsilon^\infty \frac{x}{\epsilon} \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{x^2}{2}\right) dx \\
&= \sqrt{\frac{2}{\pi\epsilon^2}} \int_\epsilon^\infty x\exp\left(-\frac{x^2}{2}\right)dx \\
&= \sqrt{\frac{2}{\pi\epsilon^2}} \int_\epsilon^\infty \exp\left(-\frac{x^2}{2}\right) d(x^2 / 2) \\
&= \sqrt{\frac{2}{\pi\epsilon^2}} \exp\left(-\frac{\epsilon^2}{2}\right)
\end{align*}
$$

所以，当$$n\rightarrow \infty$$，我们有

$$
p(\left\vert \hat{\mu} - \mu\right\vert \ge \epsilon) = p\left(\left\vert \frac{\hat{\mu} - \mu}{\sigma/\sqrt{n}} \right\vert \ge \frac{\epsilon\sqrt{n}}{\sigma}\right) \le \sqrt{\frac{2\sigma^2}{\pi n\epsilon^2}} \exp\left(-\frac{n\epsilon^2}{2\sigma^2}\right)
$$

这个上界比由Chebyshev不等式得到的$$\frac{\sigma^2}{n\epsilon^2}$$要好得多，因为这里的误差随$$n$$指数收敛到0（并且还有一个额外的$$1/\sqrt{n}$$收敛项）。值得注意的是，这个估计的上界在$$n$$很大时显著的比Chebyshev不等式得到的上界要好，但当$$n$$较小时却并不一定，因为$$n$$小时指数项接近于常数1，从而误差项接近于$$\sqrt{\frac{2\sigma^2}{n\epsilon^2}}$$，这是不如Chebyshev不等式得到的上界的。

为了让这个上界严格成立，我们可以引入一个subgaussian的性质，定义如果一个随机变量$$X$$满足

$$
\forall \lambda\in\mathbb{R}, \qquad \mathbb{E}[\exp(\lambda X)] \le \exp\left(\frac{1}{2}\lambda^2\sigma^2\right)
$$

则我们称$$X$$的分布为$$\sigma$$-subgaussian。一个特例是$$N(0, \sigma^2)$$的正态分布，我们有

$$
\begin{align*}
\mathbb{E}[\exp(\lambda X)] &= \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{x^2}{\sigma^2}\right) \cdot \exp(\lambda x) dx \\
&= \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x - \lambda \sigma^2)^2}{2\sigma^2} + \frac{1}{2}\lambda^2\sigma^2\right) dx \\
&= \exp\left(\frac{1}{2}\lambda^2 \sigma^2\right)
\end{align*}
$$

另一个特例是如果$$X$$有界，即$$\vert X \vert\le B$$，并且$$\mathbb{E}[X] = 0$$那么$$X$$的分布为$$B$$-subgaussian。（TODO：证明）

subgaussian分布有一些比较好的性质，比如
* 若$$X$$为$$\sigma$$-subgaussian，则对任何$$c\in\mathbb{R}$$，$$cX$$为$$\vert c\vert\sigma$$-subgaussian。
* 若$$X_1$$和$$X_2$$分别为$$\sigma_1$$和$$\sigma_2$$-subgaussian，则$$X_1 + X_2$$为$$\sqrt{\sigma_1^2 + \sigma_2^2}$$-subgaussian。
* 若$$X$$为$$\sigma$$-subgaussian，则$$\mathbb{E}[X] = 0$$，且$$\mathbb{V}[X]\le \sigma^2$$。

---

前两个性质很容易由定义得到，第三个性质可以证明如下。由指数函数的泰勒级数形式，得到

$$
\exp(\lambda X) = 1 + \lambda X + \frac{(\lambda X)^2}{2!} + ...
$$

从而根据$$\sigma$$-subgaussian的定义，有

$$
\mathbb{E}[\exp(\lambda X)] = \mathbb{E}\left[1 + \lambda X + \frac{(\lambda X)^2}{2!} + ...\right] \le \exp\left(\frac{1}{2}\lambda^2\sigma^2\right)
$$

因此

$$
\lambda \mathbb{E}[X] \le \exp\left(\frac{1}{2}\lambda^2\sigma^2\right) - 1 - \frac{\lambda^2 \mathbb{E}[X^2]}{2!} - ...
$$

取$$\lambda > 0$$，得

$$
\mathbb{E}[X] \le \frac{\exp(\lambda^2\sigma^2/2) - 1}{\lambda} - \frac{\lambda \mathbb{E}[X^2]}{2!} - ...
$$

当$$\lambda \rightarrow 0$$，右边的高次项变为0，第一项可由L'Hôpital's rule（洛必达法则）得到

$$
\mathbb{E}[X] \le \lim_{\lambda\rightarrow 0} \frac{\exp(\lambda^2\sigma^2/2) - 1}{\lambda} = \lim_{\lambda\rightarrow 0} \lambda\sigma^2 \exp(\lambda^2\sigma^2/2) = 0
$$

取$$\lambda < 0$$并且$$\lambda \rightarrow 0$$，可类似的得到$$\mathbb{E}[X]\ge 0$$。结合起来，得到$$\mathbb{E}[X] = 0$$。

同样利用泰勒级数形式，以及上面得到的$$\mathbb{E}[X] = 0$$，我们有

$$
\frac{\lambda^2}{2}\mathbb{E}[X^2] \le \exp\left(\frac{1}{2}\lambda^2\sigma^2\right) - 1 - \frac{\lambda^3\mathbb{E}[X^3]}{3!} - ...
$$

从而

$$
\mathbb{E}[X^2] \le \frac{2}{\lambda^2} \left[\exp\left(\frac{1}{2}\lambda^2\sigma^2\right) - 1\right] - \frac{2\lambda}{3!}\mathbb{E}[X^3] - ...
$$

当$$\lambda \rightarrow 0$$，右边的高次项同样变为0，第一项可再一次由L'Hôpital's rule得到，

$$
\mathbb{E}[X^2] \le \lim_{\lambda\rightarrow 0}\frac{2}{\lambda^2} \left[\exp\left(\frac{1}{2}\lambda^2\sigma^2\right) - 1\right] = \lim_{\lambda\rightarrow 0}\frac{\lambda\sigma^2\exp\left(\frac{1}{2}\lambda^2\sigma^2\right)}{\lambda} = \sigma^2
$$

因此$$\mathbb{V}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2 = \mathbb{E}[X^2]\le \sigma^2$$。

---

由这些性质可以推导出$$\sigma$$-subgaussian分布的tail-probability，

$$
p(X \ge \epsilon) = p(\exp(\lambda X) \ge \exp(\lambda \epsilon)) \le \frac{\mathbb{E}[\exp(\lambda X)]}{\exp(\lambda \epsilon)} \le \exp\left(\frac{1}{2}\lambda^2\sigma^2 - \lambda \epsilon\right)
$$

上式对于任何$$\lambda > 0$$成立，其中用到了Markov不等式。选取$$\lambda = \frac{\epsilon}{\sigma^2}$$得

$$
p(X \ge \epsilon) \le \exp\left(-\frac{\epsilon^2}{2\sigma^2}\right)
$$

因为$$-X=(-1)\cdot X$$也是$$\sigma$$-subgaussian，从而

$$
p(-X \ge \epsilon) \le \exp\left(-\frac{\epsilon^2}{2\sigma^2}\right)
$$

我们有

$$
p(\vert X - \mathbb{E}[X]\vert \ge \epsilon) = p(\vert X\vert \ge \epsilon) = p(X \ge \epsilon) + p(-X \ge \epsilon) \le 2 \exp\left(-\frac{\epsilon^2}{2\sigma^2}\right)
$$


进而可以推出，在前面讨论过的参数估计的设定下，如果$$X_i - \mu$$为$$\sigma$$-subgaussian分布（例如当$$X_i\sim N(\mu, \sigma^2)$$），那么

$$
\hat{\mu} - \mu = \frac{1}{n}\sum_{i=1}^n (X_i - \mu)
$$

则为$$\frac{1}{n}\sqrt{n\sigma^2} = \frac{\sigma}{\sqrt{n}}$$-subgaussian。这个误差量的上界可以确定为

$$
p(\vert \hat{\mu} - \mu\vert \ge \epsilon) \le 2 \exp\left(-\frac{n\epsilon^2}{2\sigma^2}\right)
$$

这个上界另一个常见的写法是，以至多$$\delta = 2 \exp\left(-\frac{n\epsilon^2}{2\sigma^2}\right)$$的概率，$$\vert \hat{\mu} - \mu\vert \ge\epsilon$$。反过来，以至少$$1-\delta$$的概率，$$\hat{\mu}$$应落在$$(\mu - \epsilon, \mu + \epsilon)$$的区间内。将$$\epsilon$$用$$\delta$$表示，可得这个区间为

$$
\left(\mu - \sqrt{\frac{2\sigma^2\log(2/\delta)}{n}}, \mu + \sqrt{\frac{2\sigma^2\log(2/\delta)}{n}}\right)
$$