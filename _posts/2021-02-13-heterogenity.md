---
layout: post
title: 個別因果効果の推定について
tags: [statistics]
---

* index
{:toc}

# 個別因果効果とは

ある処置を施したとき、各対象にどのような影響を与えるかを知りたいとする。これを**個別因果効果**という。個別因果効果が知りたい場面として、例えば薬の治験が考えられる。一般に薬を投与される患者によって、薬の副作用は異なると考えられる。**平均因果効果**では興味のある集団に対する処置の影響を測るものだが、**個別因果効果**は各対象に対する処置の影響を測るものである。

# 個別因果効果の定義

いま、ある共変量$X_i$を持った対象についての処置の効果を考える。処置変数を$W_i$, 処置を受けたときと受けなかったときのアウトカムをそれぞれ$Y_i(1), Y_i(0)$とすると、条件付き平均因果効果$\tau(x)$は

$$
\tau(x)=\mathbb{E}[Y_i(1)-Y_i(0)|X_i=x]
$$

で定義される[^cate]。

[^cate]: ここでは同じ共変量を持つ対象同士については処置に対して同じ影響を受けるという前提に立っている。

# 個別因果効果の推定方法

## セミパラメトリックモデリング

$\tau(x)$に関して以下の式が成り立つと考える。

$$
\begin{align}
& Y_i(w)=f(X_i)+w\cdot\tau(X_i)+\epsilon_i(w)\\
& \tau(x)={\beta}^\top{\psi}(x)\,,{\psi}:\mathcal{X}\to\mathbb{R}^k, {\beta}\in\mathbb{R}^k\\
& e(x):=\mathbb{P}[W_i=1|X_i]
\end{align}
$$

[Robinson(1998)](https://www.jstor.org/stable/1912705?seq=1)より、これは

$$
\begin{align}
& Y_i(W_i)-m(X_i)=(W_i-e(X_i))\psi(X_i)^\top\beta+\epsilon_i\\
& m(x)=\mathbb{E}[Y_i|X_i=x] = f(X_i)+e(X_i)\cdot\psi(X_i)^\top\beta
\end{align}
$$

と書き換えられて、これをOLSで推定した$\beta$の推定値を$\hat{\theta}^\ast$とすると、$O(1/\sqrt{n})$のオーダーで$\beta$との一致性を持ち、漸近正規となる。

実際には、$m(x), e(x)$がわからないので、プラグイン推定量を用いることになるが、その際の最適性の条件については[Nie and Wager(2017)](https://arxiv.org/abs/1712.04912) で議論されているR-Lossを用いた二段階推定を行えば良い。

# 参考文献

- [Causal Inference(スタンフォード大学の講義資料, stats361)](https://web.stanford.edu/~swager/stats361.pdf)
- [Robinson(1998)](https://www.jstor.org/stable/1912705?seq=1)
- [Nie and Wager(2017)](https://arxiv.org/abs/1712.04912)

