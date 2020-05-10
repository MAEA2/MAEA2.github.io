---
layout : post
title: 有界な確率変数 は sub-gaussian
tags: [math,statistics]
---


<div class='theorem'>
<div class='box-title'>定理</div>
確率変数 $X$ が区間 $[a,b]$ で値を取るとする。このとき $X$ は パラメータ $\sigma=\frac{b-a}{2}$ で sub-gaussianになる。
</div>

<div class='proof'>
<div class='box-title'>証明</div>
$\psi(\lambda):=\log\mathbb{E}[e^{\lambda X}]$ と置くと。テイラーの定理より

$$
\psi(\lambda)　= \psi(0) + \psi^\prime(0)\lambda + \frac{\psi^{\prime\prime}(c)}{2}\lambda^2
$$

が成り立つ。ここで $\psi(0)=0, \psi^\prime(0)=\mathbb{E}[X]$ であるから、 $\sup_{\lambda\in\mathbb{R}}\psi^{\prime\prime}(\lambda)$ を評価すれば良い。

$$
\mathbb{E}_\lambda[f(X)]:=\frac{\mathbb{E}[f(X)e^{\lambda X}]}{\mathbb{E}[e^{\lambda X}]}
$$

と定めると、

$$
\psi^{\prime\prime}(\lambda)=\mathbb{E}_\lambda[(X-\mathbb{E}_\lambda[X])^2]
$$

と書ける。ここで $\lambda$ を固定して 実数 $t$ の二次関数 $\mathbb{E}_\lambda[(X-t)^2]$ を考える。

この関数は、$t=\mathbb{E}_\lambda[X]$ のときに最小になることがわかる。

したがって、

$$
\mathbb{E}_\lambda[(X-\mathbb{E}_\lambda[X])^2] \leq \mathbb{E}_\lambda\left[\left(X-\frac{b+a}{2}\right)^2\right]
\leq \frac{(b-a)^2}{4}
$$

これより $\mu=\mathbb{E}[X], \sigma=\frac{b-a}{2}$ と置くと

$$
\psi(\lambda) \leq  \mu\lambda + \frac{\sigma^2}{2}\lambda^2
$$

が すべての $\lambda\in\mathbb{R}$ で成立するので、$X$ はsub-gaussianとなる。

</div>

# 参考
次の本のExercise 2.4にあった問題。

- [High-Dimensional Statistics
A Non-Asymptotic Viewpoint](https://www.cambridge.org/core/books/highdimensional-statistics/8A91ECEEC38F46DAB53E9FF8757C7A4E)
