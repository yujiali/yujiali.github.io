---
layout: blog_post
title: 运动和力学
---

运动是我们可以直接观测到的物理现象，一个物体从一个地方移动到另一个地方，运动的快慢，都是可以观测的。而力则不同，力是一个挺抽象的概念。中学课本里，我们学过“力是物体间的相互作用”，但这个定义本身是很含糊的，相互作用这个词可以有很多模糊的解读，这样的定义仔细想一下其实并不能算是一个很有用的定义。所以力到底是什么呢？

历史上，伽利略的一个重大贡献是惯性原理：如果一个物体没有受到任何其他物体和环境的影响，那么它将会保持它的运动状态，一直持续下去。如果物体之前静止，那么它会保持静止，如果物体在朝一个方向以一定速度运动，那么它会继续保持那个方向和速度运动。

牛顿进一步提出，如果要改变物体的运动状态，则需要对它施加一定的影响，比如直接推它一把。这就是要对物体施加一个“力”的作用。牛顿提出了三条定律：

1. 如果一个物体没有受到任何其他物体和环境的影响，那么它将会保持它的运动状态，一直持续下去。（即伽利略惯性原理）
2. 物体动量随时间的变化率与其受到的力成正比。
3. 作用力与反作用力大小相等方向相反。

物理上，动量（momentum）定义为质量（mass）和速度（velocity）的乘积

$$
p = mv
$$

牛顿的第二定律说

$$
F = \frac{dp}{dt} = \frac{d}{dt}(mv)
$$

在低速（速度远小于光速）情况下，质量视为恒定，可得

$$
F = \frac{d}{dt}(mv) = m \frac{dv}{dt} = ma
$$

这个定律将力的作用和力的效果联系了起来，成为了动力学里面最根本的一条规律。一个物体的质量本质上衡量了它的运动状态被改变的难易程度。牛顿第二定律总结抽象了这样一个事实：同样大小的力，用在质量小的物体上它的运动状态很容易就被改变（很容易将其加速），用在质量大的物体上运动状态就没那么容易改变（较难将其加到同样的速度）。

说回实际的观测，物体的速度

$$
v = \frac{ds}{dt}
$$

是可以通过对位移$$s$$和时间$$t$$的测量得出的，对于物体的质量，人们知道质量和重量有一个直接的正比关系。但是对于力$$F$$本身，其实并没有很好的测量办法。因此牛顿第二定律某种意义上也可以被认为是力的一种定义方式。我们可以从物体的运动规律，比如它的轨迹，反推出它所受到的力是什么形式。

历史上牛顿就是这样推导出引力定律的。当时对于天体的运动，开普勒等人已经做出了不少研究，开普勒尤其提出了行星运动的三定律：

1. 行星运动轨迹是一个椭圆，太阳在椭圆的一个焦点上。
2. 从太阳到行星的连线在相同的时间内扫过相同的面积。
3. 行星运行周期的平方与椭圆半长轴的三次方成正比。

开普勒的定律都是从行星的观测数据总结提炼出来的。牛顿在此基础上进了一大步，他从行星的椭圆形轨迹反推出引力的形式必须为平方反比，亦即

$$
F \propto \frac{m}{r^2}
$$

再设想引力同样作用于太阳，可知

$$
F \propto \frac{m'}{r^2}
$$

也需要成立，因此

$$
F \propto \frac{mm'}{r^2}
$$

选取合适的质量、距离及力的单位，可使上式变为等式，得到

$$
F = G \frac{mm'}{r^2}
$$

这就是我们熟悉的牛顿引力定律的形式。

引力定律的强大之处在于它的普适性。牛顿从天体运动的数据中总结出引力定律，但这个定律却被发现能适用于任何的物体！如果能测得物体的质量和物体间的距离，那么他们在引力作用下的力以及运动形式就可以用数学方法完整的描述出来，不用再一个一个的做观测了。从牛顿力学三定律也可以推导出一整套解释物体运动的理论，引申出很多重要的物理概念包括能量、动量、角动量以及相应的守恒定律等等。这套体系不仅可以完美解释开普勒的行星运动定律，还可以用在小到沙粒，大至天体的各种物体的运动。这给了我们一个可以用于认识和预测物体运动的强大工具。很难想象牛顿和康熙皇帝是生活在同一时期的人，在那个年代，牛顿的引力和力学理论之精确简直近乎神迹。牛顿力学是如此的成功，以至于几百年后到了二十世纪才第一次遇到问题，得到相对论和量子力学的修正。

***

接下来，我们就看一看如何从行星运动的椭圆轨迹推导出引力的距离平方反比形式。我们从椭圆的极坐标表示形式（至于为什么这表示一个椭圆，可以看我的另一篇文章[TODO]）

$$
r = \frac{p}{1 + \epsilon \cos \theta}
$$

出发，尝试推导出行星的加速度$$a \propto \frac{1}{r^2}$$与距离的平方成反比，因此根据牛顿第二定律$$F = ma \propto \frac{m}{r^2}$$。

为了让推导过程稍容易一些，我们引入旋转研究中很重要的力矩的概念。首先让我们明确，牛顿定律中的力、速度、加速度、位移等都是向量，我们用粗体表示向量，则牛顿第二定律的形式为

$$
\boldsymbol{F} = m\boldsymbol{a} = m \frac{d\boldsymbol{v}}{dt} = m\frac{d^2\boldsymbol{r}}{dt^2}
$$

选取太阳所在的椭圆焦点为原点，一个力$$\boldsymbol{F}$$的力矩为其垂直于$$\boldsymbol{r}$$的分量$$F_{\bot}$$与距离$$r$$的乘积。在二维平面中，可以将$$\boldsymbol{r}$$和$$\boldsymbol{F}$$表示为

$$
\boldsymbol{r} = (x, y), \qquad \boldsymbol{F} = (F_x, F_y)
$$

则可得力矩（torque）为

$$
\tau = x F_y - y F_x
$$

引入新的运算符$$\times$$来表示这个运算，可定义$$\tau = \boldsymbol{r} \times \boldsymbol{F}$$。这个新的运算符被称为cross product / vector product，中文译作叉积、外积（与内积相对应）或向量积（与内积得到标量相对应）。容易验证$$\times$$满足普通乘法的结合律和分配律，但不满足交换律（$$\boldsymbol{r} \times \boldsymbol{F} = -\boldsymbol{F} \times \boldsymbol{r}$$）。并且对于任意向量$$\boldsymbol{x}$$，$$\boldsymbol{x} \times \boldsymbol{x} = \boldsymbol{0}$$，从而易得对任意平行向量$$\boldsymbol{x}, \boldsymbol{x}'$$有$$\boldsymbol{x} \times \boldsymbol{x}' = \boldsymbol{0}$$。

我们在牛顿第二定律的两边都乘上$$\boldsymbol{r}$$，可得

$$
\boldsymbol{r} \times \boldsymbol{F} = m \boldsymbol{r} \times \frac{d\boldsymbol{v}}{dt}
$$

对于引力来说，引力的方向始终在$$\boldsymbol{r}$$的沿线上，并且与$$\boldsymbol{r}$$的方向相反，因而易得$$\boldsymbol{r} \times \boldsymbol{F} = \boldsymbol{0}$$。

因此

$$
\boldsymbol{r} \times \frac{d\boldsymbol{v}}{dt} = \boldsymbol{0}.
$$

从而

$$
\frac{d}{dt}(\boldsymbol{r} \times \boldsymbol{v}) = \frac{d\boldsymbol{r}}{dt} \times \boldsymbol{v} + \boldsymbol{r} \times \frac{d\boldsymbol{v}}{dt} = \boldsymbol{v} \times \boldsymbol{v} + \boldsymbol{r} \times \frac{d\boldsymbol{v}}{dt} = \boldsymbol{r} \times \frac{d\boldsymbol{v}}{dt} = \boldsymbol{0}.
$$

可得$$\boldsymbol{r} \times \boldsymbol{v}$$在运动过程中需保持恒定为一个常量。

将$$\boldsymbol{v}$$分解为平行和垂直于$$\boldsymbol{r}$$的两个分量之和，得

$$
\boldsymbol{r} \times (\boldsymbol{v}_\parallel + \boldsymbol{v}_\bot) = \boldsymbol{r} \times \boldsymbol{v}_\bot = r \cdot v_\bot
$$

在垂直方向上

$$
v_\bot = r\frac{d\theta}{dt} = r\theta'
$$

因此在行星运动的过程中

$$
r\cdot r\theta' = r^2 \theta' = C \equiv \text{constant}
$$

接下来，我们回到运动轨迹的椭圆表达式，两边对时间求导，得到

$$
r' = \frac{\epsilon p\sin\theta}{(1 + \epsilon \cos\theta)^2}\theta' = \frac{\epsilon r^2 \sin\theta}{p} \theta' = \frac{\epsilon C}{p}\sin\theta
$$

再求导，得到

$$
r'' = \frac{\epsilon C}{p}\cos \theta \theta' = \frac{\epsilon C}{p}\left(\frac{p}{r} - 1\right)\frac{1}{\epsilon} \frac{C}{r^2} = \frac{C^2}{r^3} - \frac{C^2}{pr^2}
$$

最后，让我们来看旋转中物体的加速度，我们有$$\boldsymbol{r} = r \cdot \hat{\boldsymbol{r}}$$，其中$$r$$是位移的大小，亦即距离，$$\hat{\boldsymbol{r}}$$为$$\boldsymbol{r}$$方向的单位向量，因此

$$
\frac{d\boldsymbol{r}}{dt} = \frac{d}{dt}(r \hat{\boldsymbol{r}}) = r' \hat{\boldsymbol{r}} + r \hat{\boldsymbol{r}}'
$$

这里$$\hat{\boldsymbol{r}}'$$为$$\boldsymbol{r}$$方向变化的速度，通过几何关系可知$$\hat{\boldsymbol{r}}' = \theta' \hat{\boldsymbol{r}}_\bot$$，$$\hat{\boldsymbol{r}}_\bot$$为垂直于$$\boldsymbol{r}$$方向的单位向量。再求一次导数，得到

$$
\begin{align*}
\frac{d^2\boldsymbol{r}}{dt^2} = \frac{d}{dt}(r' \hat{\boldsymbol{r}} + r \theta' \hat{\boldsymbol{r}}_\bot) &= r'' \hat{\boldsymbol{r}} + r' \hat{\boldsymbol{r}}' + r'\theta'\hat{\boldsymbol{r}}_\bot + r\theta'' \hat{\boldsymbol{r}}_\bot + r\theta'\hat{\boldsymbol{r}}_\bot' \\
&= r'' \hat{\boldsymbol{r}} + (r'\theta' + r'\theta' + r\theta'')\hat{\boldsymbol{r}}_\bot + r\theta'\hat{\boldsymbol{r}}_\bot'
\end{align*}
$$

再次利用守恒律$$r^2\theta' = C$$，在其两边求导，得到

$$
2rr'\theta' + r^2\theta' = 0
$$

从而上式中第二项为0。对于第三项，$$\hat{\boldsymbol{r}}_\bot'$$为$$\boldsymbol{r}$$垂直方向的变化率，再由几何关系可以得到$$\hat{\boldsymbol{r}}_\bot' = -\theta' \hat{\boldsymbol{r}}$$，带入回上面的加速度表达式，得到

$$
\frac{d^2\boldsymbol{r}}{dt^2} = \left[r'' - r(\theta')^2\right] \hat{\boldsymbol{r}}.
$$

将上面得到的$$r''$$表达式以及$$r^2\theta' = C$$带入，可得

$$
\frac{d^2\boldsymbol{r}}{dt^2} = \left[\frac{C^2}{r^3} - \frac{C^2}{pr^2} - r\left(\frac{C}{r^2}\right)^2\right] \hat{\boldsymbol{r}} = -\frac{C^2}{pr^2}\hat{\boldsymbol{r}}.
$$

这里的负号表示加速度的方向和$$\boldsymbol{r}$$相反，是朝向原点的方向。

最后，带入牛顿第二定律，可得引力的平方反比形式为

$$
\boldsymbol{F} = m\frac{d^2\boldsymbol{r}}{dt^2} = -m \frac{C^2}{pr^2}\hat{\boldsymbol{r}}.
$$

以上就是从物体运动的轨迹反推其所受到的作用力的一个（或许是史上第一个？）例子，牛顿当年的推导大致就是这样。

这个推导过程中涉及到了新的物理概念“力矩”，并且我们看到$$\boldsymbol{r}\times \boldsymbol{v}$$是一个守恒量。再转动的研究中，我们把$$m \boldsymbol{r} \times \boldsymbol{v}$$称为“角动量”，如果总的力矩为0，那么角动量将保持不变，此即角动量守恒定律。

类似的推导方法还可以用来推导其他运动轨迹所需要的作用力形式，例如$$F \propto r, F\propto \frac{1}{r^3}$$（参考[这里](https://web.math.utk.edu/~freire/m231f07/m231f07NewtonKeplerConverse.pdf)），感兴趣的读者可以自己去延伸一下。