---
layout : post
title: 確率変数の収束
tags: [math]
---

確率論の個人的な復習メモ。
よくあるやつ。イメージが湧く感じに書き留めておきたい。

## 確率空間
全事象$\Omega$,$\sigma$-加法族$\mathcal{F}$,確率測度$P$の三つ組$(\Omega,\mathcal{F},P)$を確率空間という。
測度の定義とか$\sigma$-加法族の定義とかは省略。

## 確率変数

$\Omega$上の実数値可測関数を(実)確率変数という。

可測関数の定義は省略。

$(\Omega,\mathcal{F},P)$の確率変数の列$\left(X_{n}\right)_{n=1,2,\ldots}$と確率変数$X$を考える。

$X_n$が$X$に収束する("近づく")のにいくつかバリエーションがある。

## チェビシェフの不等式

<div class="box">

$X$を非負値確率変数とする。$A\in\mathcal{F}$として$\psi:\mathbb{R}\to\mathbb{R}$を非負値関数とする。

確率変数$X$と可測集合$A$に対して

$$
P(A)\leq \frac{E[\psi(X)]}{\inf \left\{\psi(X(\omega))\,\big\vert\, \omega\in A \right\}}
$$

</div>

[証明]

$1_A:\Omega\to\{ 0,1 \}$を$A$に関する指示関数とする。

$$
1_A\leq \frac{\psi(X)}{\inf \left\{\psi(X(\omega))\,\big\vert\, \omega\in A \right\}}
$$

が成り立つので、両辺の期待値をとると

$$
E[1_A]\leq \frac{E[\psi(X)]}{\inf \left\{\psi(X(\omega))\,\big\vert\, \omega\in A \right\}}
$$

ここで$E[1_A]=P(A)$より、定理が示された。

## 概収束

$$
P\left(\left\{\omega\in\Omega\,\Big\vert\,\lim_{n\to\infty}X_n(\omega)=X(\omega)\right\}\right)=1
$$

が成立するとき、$X_n$は$X$に概収束するといい、$X_n\longrightarrow X\,(a.s.)$あるいは$X_n\stackrel{a.s.}{\longrightarrow}X$と書く。

つまり$X_n(\omega)$の収束先が$X(\omega)$であるという事象が起きる確率が1となるということ。

$$
\lim_{n\to\infty}P\left(\left\{\omega\in\Omega\,\vert\,X_n(\omega)=X(\omega)\right\}\right)=1
$$

ではないことに注意する。


## 確率収束
任意の正の数$\varepsilon$に対して

$$
\lim_{n\to\infty}P\left(\left\{\omega\in\Omega\,\Big\vert\,\left|X_n(\omega)-X(\omega)\right|>\varepsilon\right\}\right)=0
$$

となるとき$X_n$は$X$に確率収束するといい、$X_n\stackrel{p}{\longrightarrow}X$と書く。

つまり任意の微小な正の数$\varepsilon$について$X_n(\omega)$と$X(\omega)$の差が$\varepsilon$より大きくなるという事象が起きる確率は0ということ。言い換えると、確率1で$X_n(\omega)$と$X(\omega)$の差は$\varepsilon$以下になるということ。

## $p$次平均収束

$p\geq 1$とする。

$$
\lim_{n\to\infty} E\left[|X_n-X|^p\right]=0
$$

であるとき$X_n$は$X$に$p$-次平均収束するという。

こいつはわかりやすい。

## 法則収束(分布収束)

任意の有界な実数値関数$f:\mathbb{R}\to\mathbb{R}$に対して

$$
\lim_{n\to\infty} E[f(X_n)]=E[f(X)]
$$

が成立するとき、$X_n$は$X$に分布収束するといい、$X_n\stackrel{d}{\longrightarrow}X$と書く。ここで$f(X_n)$とか$f(X)$は$\Omega$上の可測関数になっており、これ自身が確率変数。
定義から分かるように、法則収束では$X_n$と$X$が同じ確率空間上になくてもよい。


## 収束同士の関係

<div class="box">

$X_n$が$X$に概収束するならば$X_n$は$X$に確率収束する。

</div>

[証明]

$\varepsilon$を任意の正数とする。

$$
A_n=\bigcup_{m\geq n}\left\{|X_m-X|>\varepsilon\right\}
$$

という$\omega$の集合を定める。

$A_n$は

$$
A_{n}\supset A_{n+1} \supset \ldots
$$

を満たす。

ここで

$$
A_{\infty}=\bigcap_{n\geq 1} A_n
$$

という$\omega$の集合を考える。

すなわち、

$$
A_{\infty}=\lim_{n\to\infty} A_n
$$

と定める。

$$
\{|X_n-X|>\varepsilon\}\subset A_n
$$

が成り立つ。

$$
P(\{|X_n-X|>\varepsilon\}) \leq P(A_n)\to P(A_\infty)=0\,(n\to\infty)
$$

$P(A_\infty)$が$0$になるのは、$X_n\longrightarrow X\,(a.s.)$であることから。


<div class="box">

$X_n$が$X$に$p(\geq 1)$次平均収束ならば$X_n$は$X$に確率収束する。

</div>

[証明]

チェビシェフの不等式より,

$$
P(|X_n-X|> \varepsilon)\leq \frac{E[|X_n-X|^p]}{\varepsilon^p}=0\,(n\to\infty)
$$

## 参考文献

* [確率論 舟木直久](http://www.asakura.co.jp/books/isbn/978-4-254-11600-7/)
* [Convergence almost surely implies convergence in probability](https://en.wikipedia.org/wiki/Proofs_of_convergence_of_random_variables##propA1)
