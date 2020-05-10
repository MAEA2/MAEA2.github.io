---
layout: post
title: 集中不等式まとめ
tags: [math]
---

* index
{:toc}

自分用に纏めます。証明がパラレルに進むのが楽しい。

[この本](https://mitpress.mit.edu/books/foundations-machine-learning)に載ってる内容を写経して和訳してるだけ。

写経しながら証明を理解する。

## Hoeffdingの補題

<div class="theorem">
<div class='box-title'>Theorem</div>
$X$を $\mathbb{E}[X]=0$ かつ$a\leq X\leq b$となる確率変数とする。

このとき任意の正数$t$に対して

$$
\mathbb{E}[e^{tX}]\leq e^{\frac{t^2(b-a)^2}{8}}
$$

</div>
<div class='proof'>
<div class='box-title'>Proof</div>

関数 $f(x)=e^{tx}$ の凸性から

$$
e^{tx}\leq \frac{b-x}{b-a}e^{ta}+\frac{x-a}{b-a}e^{tb}
$$

が成立する。$\mathbb{E}[X]=0$に注意して両辺の期待値をとると

$$
\mathbb{E}[e^{tX}]\leq \frac{b}{b-a}e^{ta}+\frac{-a}{b-a}e^{tb}=e^{\phi(t)}
$$

ただし

<div class="scroll">

$$
\begin{align*}
\phi(t)&=\log\left(\frac{b}{b-a}e^{ta}+\frac{-a}{b-a}e^{tb}\right)\\
&=\log\left(e^{ta}\left(\frac{b}{b-a}+\frac{-a}{b-a}e^{t(b-a)}\right)\right)\\
&=ta +\log\left(\frac{b}{b-a}+\frac{-a}{b-a}e^{t(b-a)}\right)
\end{align*}
$$

$$
\begin{align*}
\phi^\prime(t)&=a-\frac{ae^{t(b-a)}}{\frac{b}{b-a}+\frac{-a}{b-a}e^{t(b-a)}}\\
&=a-\frac{a}{\frac{b}{b-a}e^{-t(b-a)}-\frac{a}{b-a}}\\
\phi^{\prime\prime}(t)&=\frac{-abe^{-t(b-a)}}{\left\{\frac{b}{b-a}e^{-t(b-a)}-\frac{a}{b-a}\right\}^2}\\
&=\frac{\alpha(1-\alpha)e^{-t(b-a)}(b-a)^2}{[(1-\alpha)e^{-t(b-a)}+\alpha]^2}
\end{align*}
$$

</div>

ただし

$$
\alpha=-\frac{a}{b-a}
$$

と置いた。

$\phi(0)=\phi^\prime(0)=0$であり、

$$
u=\frac{\alpha}{(1-\alpha)e^{-t(b-a)}+\alpha}
$$

と置くと

$$
\phi^{\prime\prime}(t)=u(1-u)(b-a)^2
$$

とかける。

ここで $0\leq u \leq 1$ であるから、

$$
u(1-u)\leq \frac{1}{4}
$$

である。

以上より $\phi(t)$ にTaylorの定理を適用すればある $\theta\in[0,1]$ が存在して

<div class="scroll">

$$
\phi(t)=\phi(0)+t\phi^\prime(0)+\frac{t^2}{2}\phi^{\prime\prime}(\theta)\leq t^2\frac{(b-a)^2}{8}
$$

</div>

</div>

## Hoeffdingの不等式

<div class="theorem">
<div class='box-title'>Theorem</div>
$X_1,X_2,\ldots,X_m$を独立な確率変数で、各$X_i$は$[a_i,b_i]$に値を取るとする。

このとき任意の正数 $\varepsilon$ に対して

$$
\mathrm{Pr}[S_m-\mathbb{E}[S_m]\geq \varepsilon]\geq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m(b_i-a_i)^2}\right)\\
\mathrm{Pr}[S_m-\mathbb{E}[S_m]\leq -\varepsilon]\leq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m(b_i-a_i)^2}\right)
$$


が成立する。

ただし

$$
S_m=\sum_{i=1}^m X_i
$$

である。

</div>

<div class='proof'>
<div class='box-title'>Proof</div>

チェビシェフの不等式(https://maea2.github.io/convergence/)において

$$
\begin{align*}
& X=e^{t(S_m-\mathbb{E}[S_m])}\\
& A=\{\omega\in \Omega \,\vert\, S_m-\mathbb{E}[S_m]\geq \varepsilon \}
\end{align*}
$$

として適用することで


$$
\mathrm{Pr}[S_m-\mathbb{E}[S_m]\geq \varepsilon ]\leq e^{-t\varepsilon}E[e^{t(S_m-\mathbb{E}[S_m])}]
$$

が得られる。

左辺にHoeffdingの補題を適用することで

<div class="scroll">

$$
\begin{align*}
\mathrm{Pr}[S_m-\mathbb{E}[S_m]\geq \varepsilon ]&\leq e^{-t\varepsilon}E[e^{t(S_m-\mathbb{E}[S_m])}]\\
&=\prod_{i=1}^m e^{-t\varepsilon}\mathbb{E}\left[e^{t(X_i-\mathbb{E}[X_i])}\right]\, (\because \text{independence of } X_i)\\
&\leq \prod_{i=1}^m e^{-t\varepsilon}\mathbb{E}\left[e^{\frac{t(b_i-a_i)^2}{8}}\right]\,(\because \text{Hoeffding's lemma})\\
&= e^{-t\varepsilon}e^{-t^2\left(\sum_{i=1}^m\frac{(b_i-a_i)^2}{8}\right)}\\
&\leq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m(b_i-a_i)^2}\right)\,(\because \text{平方完成})
\end{align*}
$$

</div>

$\mathrm{Pr}[S_m-\mathbb{E}[S_m]\leq -\varepsilon]$ についての不等式は同様に示せる。

</div>

## Martingale Difference　Sequence

<div class="definition">
<div class='box-title'>definition</div>
Martingale Difference Sequenceというものを次のように定義する。

確率変数列$V_1,V_2,\ldots$が確率変数列$X_1,X_2,\ldots$に対してMartingale Difference Sequenceであるとは

$$
E[V_{i+1}\vert X_1,\ldots,X_i]=0
$$

がすべての$i$に対して成立することをいう。

</div>

## 条件付き期待値に対するHoeffdingの補題

<div class="theorem">
<div class='box-title'>Theorem</div>
確率変数 $V$ と $Z$ について $\mathbb{E}[V\vert Z]=0$かつある関数$f$と正の定数$c$について

$$
f(X)\leq V \leq f(Z)+c
$$

が成り立つとする。

このとき、すべての正の数$t$に対して

$$
\mathbb{E}[e^{sV}\vert Z ]\leq e^{\frac{t^2c^2}{8}}
$$


が成立する。

</div>

<div class='proof'>

[証明] Hoeffdingの補題で期待値をとる操作を条件付き期待値をとる操作に変えることでほとんど同様に証明できる。
$a$ を $f(Z)$ に $b$ を $f(Z)+c$ に置き換えて考える。

</div>

## Azumaの不等式

<div class="theorem">
<div class='box-title'>Theorem</div>
$V_1,V_2,\ldots$が確率変数列$X_1,X_2,\ldots$に対してMartingale Difference Sequenceであるとする。

$Z_i$を$X_1,\ldots,X_{i-1}$の関数とする。ある定数$c_i$が存在して

$$
Z_i\leq V_i \leq Z_i+c_i
$$

が成り立つとする。

このときすべての正の数$\varepsilon$と正の整数$m$に対して、次の不等式が成立する。

$$
\begin{align*}
&\mathrm{Pr}\left[\sum_{i=1}^m V_i \geq \varepsilon \right] \leq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m c_i^2} \right)\\
&\mathrm{Pr}\left[\sum_{i=1}^m V_i \leq -\varepsilon \right] \leq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m c_i^2} \right)
\end{align*}
$$

</div>

<div class='proof'>
<div class='box-title'>Proof</div>>
$S_k=\sum_{i=1}^k V_i$ と置く。

<div class="scroll">

$$
\begin{align*}
&\mathrm{Pr}[S_m \geq \varepsilon] \leq e^{-t\varepsilon}\mathbb{E}[e^{tS_m}]\\
&=e^{-t\varepsilon}\mathbb{E}[e^{tS_{m-1}}\mathbb{E}[e^{tV_m}|X_1,\ldots,X_{m-1}]]\,(\because \text{Martingale Difference Sequence})\\
&=e^{-t\varepsilon}\mathbb{E}[e^{tS_{m-1}}]e^{\frac{t^2c_m^2}{8}}\,(\because \text{Martingale Difference Sequenceに対するHoeffdingの補題})\\
&\leq e^{-t\varepsilon}e^{t^2\sum_{i=1}^m \frac{c_i^2}{8}}\,(\because \text{iteration of the previous process})\\
&\leq \exp\left(\frac{-2\varepsilon^2}{\sum_{i=1}^m c_i^2} \right)\,(\because \text{平方完成})
\end{align*}
$$

</div>
</div>

## McDiarmidの不等式

<div class="theorem">
<div class="box-title">Theorem</div>
$X_1,\ldots,X_m\in \mathcal{X}^m$を独立な確率変数の集まりとする。$f:\mathcal{X}^m\to \mathbb{R}$ が次の条件を満たすと仮定する。

$$
|f(x_1,\ldots,x_i,\ldots,x_m)-f(x_1,\ldots,x_i^\prime,\ldots,x_m) \leq c_i\, (i=1,2,\ldots,m \,,\, x_1,\ldots,x_m,x_i^\prime \in\mathcal{X})
$$

$f(S):=f(X_1,\ldots,X_m)$ (確率変数)と置く。このとき次の不等式が成立する。

$$
\begin{align}
&\mathrm{Pr}[f(S)-E[f(S)] \geq \varepsilon ] \leq \exp(\frac{-2\varepsilon^2}{\sum_{i=1}^m c_i^2})\\
&\mathrm{Pr}[f(S)-E[f(S)] \leq -\varepsilon ] \leq \exp(\frac{-2\varepsilon^2}{\sum_{i=1}^m c_i^2})
\end{align}
$$


</div>

<div class='proof'>

<div class='box-title'>Proof</div>>
$V=f(S)-E[f(S)]$ と置く。

$$
\begin{align}
& V_1=E[V|X_1]-E[V]\\
& V_k=E[V|X_1,\ldots,X_{k}]-E[V|X_1,\ldots,X_{k-1}]
\end{align}
$$

と置く。

ここで定義より

$$
V=\sum_{i=1}^m V_i
$$

が成立する。また$\mathbb{E}[V\vert X_1,\ldots,X_{k}]$は$X_1,\ldots,X_k$の関数であり、これに対して$X_1,\ldots,X_{k-1}$についての条件付き期待値をとることで

<div class="scroll">

$$
\mathbb{E}[\mathbb{E}[V\vert X_1,\ldots,X_k]\vert X_1,\ldots,X_{k-1}]=E[V\vert X_1,\ldots,X_{k-1}]
$$

</div>

がわかる。これより $\mathbb{E}[V_k|X_1,\ldots,X_{k-1}]=0$ がすべての $k$ で成立するので $V_k$ はmartingale differnce sequenceとなる。

また$V_k$の定義式に $V=f(S)-\mathbb{E}[f(S)]$ を代入すると $\mathbb{E}[f(S)]$ は定数であるから、ちょうど項が相殺して

$$
V_k=\mathbb{E}[f(S)|X_1,\ldots,X_k]-\mathbb{E}[f(S)|X_1,\ldots,X_{k-1}]
$$

とかける。

したがって、$V_k$に対する上限$W_k$と下限$U_k$が存在して

$$
\begin{align*}
&W_k=\sup_{x} E[f(S)|X_1,\ldots,X_{k-1},x]-E[f(S)|X_1,\ldots,X_{k-1}]\\
&U_k=\inf_{x} E[f(S)|X_1,\ldots,X_{k-1},x]-E[f(S)|X_1,\ldots,X_{k-1}]
\end{align*}
$$

ここで、定理の仮定より

$$
W_k-U_k \leq \leq c_k
$$

が成立するので、

$$
U_k\leq V_k \leq U_k+c_k
$$

が成立する。

$V=\sum_{k=1}^m V_k$に対してAzumaの不等式を適用することで定理を得る。

</div>

## 備考

論文を読んでいたらRademacher complexityが出てきて、Rademacher complexityに関する不等式を示すのにMcDiarmidsの不等式を使っていた。

## 参考文献(というか全部写しただけだが)

* [Foundations of Machine Learning](https://mitpress.mit.edu/books/foundations-machine-learning)
