---
layout: post
title: 正定値行列には平方根行列が存在することの証明
tags: [math]
---

きっかけは以下のツイートです。問題が解決したので、ここに書きます。

正定値な行列なんて対称行列しかないんやから、一般の場合なんか考えても意味ないやろ！って方はブラウザバックでお願いします。こういう細かいことが気になっちゃうという人はお進み下さい。

数学の世界では、このようなことはもっと鮮やかに解決されていると思うのでもちろん車輪の再発明となっております。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">A: 正定値 なら A^(1/2)っていつも存在するんでしたっけ？</p>&mdash; まえあつ (@MAEA_2) <a href="https://twitter.com/MAEA_2/status/997637484925206528?ref_src=twsrc%5Etfw">2018年5月19日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

# 正定値行列

正定値行列の定義です。

<div class="box">

$A\in\mathbb{R}^{n\times n}$ が正定値行列であるとは

すべての $\boldsymbol{x}\in\mathbb{R}^{n},\boldsymbol{x}\neq \boldsymbol{0}$ に対して $\boldsymbol{x}^\top A \boldsymbol{x} >0$ が成立するということ

</div>

ちなみに、$\boldsymbol{x}^\top A \boldsymbol{x} >0$ ではなくて $\boldsymbol{x}^\top A \boldsymbol{x} \geq 0$ が常に成立する場合は半生定値行列というのでした。

このとき $A^{1/2}$ すなわち $X^2＝A$ となるような正方行列$X$は存在するかと言うのが問題です。

# 正定値行列と固有値の関係

次の補題が成り立ちます。

<div class="box">

$A$ : 正定値行列　ならば　$A$ のすべての固有値の実部は正である。

</div>

<div class='proof'>

[証明]

$A$ のある固有値 $\lambda=\mu+i\nu\,(\mu,\nu\in\mathbb{R})$ と対応する固有ベクトルの1つを $\boldsymbol{z}=\boldsymbol{x}+i\boldsymbol{y}\,(\boldsymbol{x},\boldsymbol{y}\in\mathbb{R}^n)$ とします。※実部と虚部をそれぞれ分けて書いています。

証明の目標は　$\mu > 0$ を示すことです。

固有値、固有ベクトルの定義から


<div class='scroll'>
$$
\begin{align}
&(A-\lambda I_n)\boldsymbol{z}=\boldsymbol{0}\\
\iff&(A-(\mu+i\nu)I_n)(\boldsymbol{x}+i\boldsymbol{y})=\boldsymbol{0}\\
\iff&\begin{cases}
(A-\mu I_n)\boldsymbol{x}+\nu y=\boldsymbol{0}\\
(A-\nu I_n)\boldsymbol{y}-\nu\boldsymbol{x}=\boldsymbol{0}
\end{cases}\\
\end{align}
$$
</div>


最後の2つの式それぞれに右から$\boldsymbol{x}^\top,\boldsymbol{y}^\top$を掛けて足すと

<div class='scroll'>
$$
\boldsymbol{x}^\top(A-\mu I_n)\boldsymbol{x}+\boldsymbol{y}^\top(A-\nu I_n)\boldsymbol{y}=
-\nu(\boldsymbol{x}^\top\boldsymbol{y}-\boldsymbol{y}^\top\boldsymbol{x})=0
$$
</div>

が成り立つので、これを $\mu$ について解くと

<div class='scroll'>
$$
\mu = \frac{\boldsymbol{x}^\top A \boldsymbol{x}+\boldsymbol{y}^\top A \boldsymbol{y}}{\boldsymbol{x}^\top \boldsymbol{x}+\boldsymbol{y}^\top\boldsymbol{y}}
$$
</div>

左辺は $A$ の正定値性と固有ベクトルが零ベクトルでないこととから正となります。

</div>

# 正定値行列の平方根

次のような形の行列 $J_n(\lambda)$ (ジョルダン細胞) を定義しておきます。


<div class="scroll">

$$

J_{n}(\lambda )={\begin{pmatrix}\lambda &1&&&0\\&\lambda &1&&\\&&\ddots &\ddots &\\&&&\lambda &1\\0&&&&\lambda \\\end{pmatrix}}

$$

</div>


正定値行列 $A$ をジョルダン標準形をつかって次のように変形します。

$$
A=P^{-1}JP
$$



ただし、$P$ は正則な行列で、 $J$ は

<div class="scroll">

$$
J=\begin{bmatrix}
J_{n_1}(\lambda_1) & &0  \\
&\ddots&\\
0&&J_{n_k}(\lambda_k)
\end{bmatrix}
$$

</div>

という形の行列です。ここで $\lambda_1,\ldots,\lambda_k$ は $A$の固有値です。

</div>

もし $J_{n_i}(\lambda_i)$ がすべて存在すれば、$A^{1/2}$ の平方根の1つとして[^1]:  $J^{1/2}_{n_i}(\lambda_i)$ は複数存在するはずなので、その組み合わせだけ、 $A$の平方根は存在するということになります。

$$
A^{1/2}:=P^{-1}\begin{bmatrix}
J_{n_1}^{1/2}(\lambda_1) & &0  \\
&\ddots&\\
0&&J_{n_k}^{1/2}(\lambda_k)
\end{bmatrix}P
$$

としてやれば、

<div class="scroll">

$$

(A^{1/2})^2=P^{-1}\begin{bmatrix}
J_{n_1}^{1/2}(\lambda_1) & &0  \\
&\ddots&\\
0&&J_{n_k}^{1/2}(\lambda_k)
\end{bmatrix}PP^{-1}\begin{bmatrix}
J_{n_1}^{1/2}(\lambda_1) & &0  \\
&\ddots&\\
0&&J_{n_k}^{1/2}(\lambda_k)
\end{bmatrix}P
=P^{-1}JP=A

$$

</div>

平方根行列になっていることがわかります。

これで問題は $A$のジョルダン標準形のジョルダンブロックに平方根行列が存在するかという問題まで変形できました。


# 正定値行列のジョルダン細胞の平方根行列

先程の補題より $A$ が正定値行列の場合は すべての固有値 $\lambda_i$ について $\mathrm{Re}(\lambda_i) > 0$　が成り立っている事がわかります。

これより $\mathrm{Re}(\lambda)>0$ となる $\lambda$ について

<div class="scroll">

$$

J_{n}(\lambda )={\begin{pmatrix}\lambda &1&&&0\\&\lambda &1&&\\&&\ddots &\ddots &\\&&&\lambda &1\\0&&&&\lambda \\\end{pmatrix}}

$$

</div>

が平方根行列を持てば良いことを示せば良いことがわかりました。

まず、$n$が小さな値のときにどうなるか考えてみましょう。

$n=1$のとき $J_1(\lambda)=\lambda^{1/2}$ とすれば良いです。[^2]: 複素数の範囲で考えると必ず平方根は存在します。


今回はとりあえず、ジョルダン細胞の平方根行列が少なくとも1つは存在することが言えれば良いので、とりあえず $J_n(\lambda)^{1/2}$ が存在するときに $J_{n+1}(\lambda)^{1/2}$ が構成できないか考えてみましょう。

行列のブロック同士の干渉しないパートを考えると次のような形

<div class="scroll">

$$
J_{n+1}(\lambda)^{1/2} = \begin{bmatrix}
J_n(\lambda)^{1/2}& \boldsymbol{b}_{n+1}\\
\boldsymbol{0} & \lambda^{1/2}
\end{bmatrix}
$$

</div>

で置いたときに $\boldsymbol{b}_{n+1}\in \mathbb{C}^{n}$ が求まれば良さげです。

2乗して$J_{n+1}(\lambda)$ になるという条件を満たさないといけないので、

<div class="scroll">

$$

\begin{align}

&\begin{bmatrix}
J_n(\lambda)^{1/2}& \boldsymbol{b}_{n+1}\\
\boldsymbol{0} & \lambda^{1/2}
\end{bmatrix}
\begin{bmatrix}
J_n(\lambda)^{1/2}& \boldsymbol{b}_{n+1}\\
\boldsymbol{0} & \lambda^{1/2}
\end{bmatrix}\\
=&\begin{bmatrix}
J_n(\lambda)& J_{n+1}^{1/2}\boldsymbol{b}_{n+1}+\lambda^{1/2}\boldsymbol{b}_{n+1}\\
\boldsymbol{0} & \lambda\\
\end{bmatrix}

={\begin{bmatrix}\lambda &1&&&0\\&\lambda &1&&\\&&\ddots &\ddots &\\&&&\lambda &1\\0&&&&\lambda \\\end{bmatrix}}

\end{align}

$$



</div>

が成り立っていないといけない。

一番右端の列同士を比較することで

$$
(J_n(\lambda)^{1/2}\boldsymbol+\lambda^{1/2} I_n){b}_{n+1}=\begin{bmatrix}
0\\
\vdots\\
0\\
1
\end{bmatrix}
$$

<div class="scroll">


を満たす $\boldsymbol{b}_{n+1}$ が求まれば良いです。

例えば$n+1=2$の場合でこの連立方程式を解いてみましょう。

書いてみると、

<div class="scroll">

$$
\begin{align}

\label{renritu}

\begin{bmatrix}
J_1(\lambda)^{1/2}& (J_1(\lambda)+\lambda^{1/2}I_1)\boldsymbol{b}_{2}\\
\boldsymbol{0} & \lambda^{1/2}

\end{bmatrix}=\begin{bmatrix}
0\\
1
\end{bmatrix}

\end{align}
$$

</div>


$n=1$ のとき $J_1^{1/2}=\lambda^{1/2}$ だったので、


$$
\begin{bmatrix}

\lambda^{1/2}& (J_1(\lambda)^{1/2}+\lambda^{1/2})b^{(2)}_1\\
\boldsymbol{0} & \lambda^{1/2}

\end{bmatrix}=\begin{bmatrix}
0\\
1
\end{bmatrix}
$$

となります。

ここで $\boldsymbol{b}_2=[b^{(2)}_1]$ と置きました。

これは、簡単に解けて$b^{(2)}_1=(2\lambda^{1/2})^{-1}$

です。ここで。$\mathrm{Re} \lambda > 0$ なので $\lambda$ は非零であるというのがポイントです。

</div>

これより、この形で求まる$J_2^{1/2}(\lambda)$ は上三角行列になっている事がわかります。
もし$J_n(\lambda)^{1/2}$ が上三角行列なら、$J_n(\lambda)^{1/2}+\lambda^{1/2} I_n$ も上三角行列であるから、上の連立方程式 $\eqref{renritu}$ は掃き出された形になっているので、下の成分から方程式を解いていけば容易に解けることがわかります。


これより $\boldsymbol{b}_{n+1}$ の存在が $n=1,2,\ldots$ で順次言えるので、固有値が非零の場合にジョルダン細胞には常に平方根行列が存在することが言えました。

これより、正定値行列には必ず平方根行列が存在すること言えます。


# 半正定値行列の場合　



零固有値がでてくるので、方程式が解けない可能性があり、このアプローチそのままでは難しそうです。

ちなみに、`Jordan`, `Positive definite` とかで調べると

- [Positive-semidefinite matrices and the Jordan totient function](http://inf.ucv.ro/~ami/index.php/ami/article/download/848/534)

が出てきたので、読んでみたいと思います。



# 参考文献

- [Does non-symmetric positive definite matrix have positive eigenvalues?](https://math.stackexchange.com/questions/83134/does-non-symmetric-positive-definite-matrix-have-positive-eigenvalues)

# 追記

正定値な場合ではなく、非特異な場合(行列が正則な場合)で一般に成り立つ証明となっているのではというご指摘がありました。どうもありがとうございます。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">これ正定値性いらなくないですかね（非特異な場合の証明になってるような）</p>&mdash; 歩衣子 (@poipoi2) <a href="https://twitter.com/poipoi2/status/1001337737281077249?ref_src=twsrc%5Etfw">2018年5月29日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

一般に行列の対数というものを考えると、すなわち

$$
e^Z:=\sum_{i=1}^\infty \frac{Z^n}{n!}
$$

としたときに$A=e^Z$となるような$Z$が存在するかどうかを考えると、

$A$が非特異な場合にはこれは存在するようです。

詳しいStatementについては、[Theory of Matrix Functions](https://epubs.siam.org/doi/pdf/10.1137/1.9780898717778.ch1)の Thereom 1.27を参照してください。
