---
layout: blog_post
title: Bandit问题和UCB算法
---

最近的研究需要探索一些exploration-exploitation tradeoff，想找一些理论上的东西，于是开始看Tor Lattimore和Csaba Szepesvári合著的[Bandit Algorithms](https://tor-lattimore.com/downloads/book/book.pdf)。这是一本写得很深入和全面的书，应该是把bandit问题的方方面面都讲到了。

Bandit问题是一个基本的、经典的关于exploration-exploitation tradeoff的问题。这个问题的设定一般是假定有$$k$$个选项(action)可选，每次选取一个选项$$a$$后可以得到一个该选项对应的回报$$r$$。对于每个选项$$a$$，其会产生的回报$$r$$有随机性，每个$$a$$的回报的分布可能也都不一样。如果允许选择$$n$$次，那么这n次选择的总回报为

$$
\sum_{t=1}^n r_t = \sum_{t=1}^n r(a_t)
$$

这里$$a_t$$为在第$$t$$轮所选择的选项，$$r_t = r(a_t)$$为选择$$a_t$$后所得到的回报，我们有$$r_t \sim p_{a_t}(r)$$。给定一个bandit问题，我们能控制的是如何选择$$a_t$$的策略。在第$$t$$轮选择之前，我们能观察到的是之前$$t-1$$轮的所有选择和对应的回报的历史序列$$h_{t-1} = (a_1, r_1, a_2, r_2, ..., a_{t-1}, r_{t-1})$$，我们的策略$$\pi$$则是一个将历史序列$$h_{t-1}$$映射到第$$t$$轮的选择$$a_t$$的函数，一般而言

$$
\pi(a_t|h_{t-1}) = \pi(a_t|a_1, r_1, ..., a_{t-1}, r_{t-1})
$$

是一个$$a_t$$的概率分布，注意当概率全部集中在一个特定选择上时，这个概率分布也可以表示确定性的策略。

Bandit问题的目标是找到一个策略$$\pi$$最大化总的回报。由于每一个选项的回报的不确定性，我们通常力求找到一个策略能够最大化总回报的期望，也即

$$
\mathbb{E}_{a_t \sim \pi(a_t|h_{t-1}), r_t \sim p_{a_t}(r)}\left[\sum_{t=1}^n r_t\right] = \mathbb{E}_{a_t\sim \pi}\left[\sum_{t=1}^n \mu_{a_t}\right]
$$

这里$$\mu_a = \mathbb{E}_{r\sim p_a(r)}[r]$$是选择$$a$$选项后所得回报的期望。如定义$$\mu^* = \max_{a} \mu_a$$为最优回报，那么在bandit问题中最常用的目标函数regret定义为

$$
R_n(\pi) = \mathbb{E}\left[\sum_{t=1}^n (\mu^* - r_t)\right] = n\mu^* - \mathbb{E}\left[\sum_{t=1}^n r_t\right]
$$

Bandit问题的目标是找到策略$$\pi$$来最大化总收益，也就等于最小化regret。一般我们使用最小化regret的这个目标，因为$$n\mu^*$$这一项本身有一点normalization的作用，能让很多分析变得更简洁一些。我们还可以定义平均regret

$$
R_n(\pi) / n = \mu^* - \frac{1}{n}\mathbb{E}\left[\sum_{t=1}^n r_t\right]
$$

在理想情况下，如果我们知道所有选项的预期收益$$\mu_a$$，那么最优的策略就是每次都选择最优选项$$a^* = \arg \max_a \mu_a$$，在这种情况下$$r_t = \mu^*$$，从而regret为0。但实际情况下，每一个选项的回报的概率分布并不一定为我们所知，我们只能通过观察推测可能的回报预期，另一方面回报具有不确定性，因而我们也不一定能准确地推测出那一个选项为最优。在给定可以做的选择的次数$$n$$之后，我们就需要去分配一定的选择次数去尝试每个选项，来估计每个选项的回报大概有多少，然后再尽量多的选择回报多的那些选项，以最大化总收益。具体在explore和exploit之间怎么平衡，就是各种bandit策略要研究的问题。

一般而言，我们的目标是希望regret尽量的小，平均regret当$$n\rightarrow 0$$时最好也能收敛到0，而更好的策略则会更快的收敛到0。

要从理论上分析bandit问题，就需要一些统计工具。

