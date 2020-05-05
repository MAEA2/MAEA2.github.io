---
layout: post
title: 次元定理の証明とその応用
tag: [math]
---
次元定理は線形代数の講義でほぼ必ず扱われますが，今回はその面白い応用を見つけたのでメモしておきます．

## 次元定理

<div class="box">
線形空間$V$の線形部分空間$S,T$に対して

$$
\dim (S\cap T)=\dim(S)+\dim(T)-\dim(S+T)
$$

が成立する．
</div>
### 証明
$S\cap T$の基底を $\{a_1,\ldots,a_k\}$ とする．この基底を拡大して$S$の基底 $\{a_1,\ldots,a_k,b_1,\ldots,b_l\}$ , $T$の基底 $\{a_1,\ldots,a_k,c_1,\ldots,c_m\}$ を作る． $\{a_1,\ldots,a_k,b_1,\ldots,b_l,c_1,\ldots,c_m\}$ が $S+T$ の基底であることを示す． これが $S+T$ を張ることは明らかなので，線形独立性を示せばよい．$\{a_1,\ldots,a_k,b_1,\ldots,b_l,c_1,\ldots,c_m\}$ の線形方程式

$$
\sum_{i=1}^k \alpha_ia_i+\sum_{i=1}^l \beta_ib_i+\sum_{i=1}^m \gamma_ic_i=0
$$

を考える．

$$
d=\sum_{i=1}^k \alpha_ia_i+\sum_{i=1}^l \beta_ib_i=-\sum_{i=1}^m \gamma_ic_i
$$

とおくと，$d$は$S$の基底の線形結合である．$c_1,\ldots,c_m$は$S$に含まれない元であるので，$d$は$S$に含まれないベクトルたちの線形結合でもある．$d=0$となる．$\{a_1,\ldots,a_k,b_1,\ldots,b_l\}$ は $S$ の基底なので
$\alpha_1=\cdots=\alpha_k=\beta_1=\cdots=\beta_l=0$．$\{c_1,\ldots,c_m\}$ は基底の一部であり線形独立なので，$\gamma_1=\cdots=\gamma_m=0$．よって　$\{a_1,\ldots,a_k,b_1,\ldots,b_l,c_1,\ldots,c_m\}$ の線形方程式は自明な解のみをもち，これらは線形独立．

## 次元定理の応用
以下の定理では次元定理が証明で肝心な役割を果たします．証明は順次気が向いたら書きます．

### $\mathrm{Ker}$ と $\mathrm{Im}$ の関係

<div class="box">

$A$ を $\mathbb{R}^n$ から $\mathbb{R}^m$への線形写像とする．

$$
\dim\mathrm{Ker}(A)+\dim\mathrm{Im}(A)=n
$$
が成立する．

</div>
#### 証明

次元定理の式で$S=\mathrm{Ker}(A),T=\mathbb{R}^n/\mathrm{Ker}(A)\cup\\{0\\}$ と置くと，これは $\mathbb{R}^n$ の線型部分空間となっている．
$\dim(S\cap T)=0,\dim(S+T)=n$．$\mathbb{R}^n=S+T$より $\dim(\mathrm{Im}(A))=\dim(A\mathbb{R}^n)=\dim(A(S+T))=\dim(AS+AT)=\dim(AT)$($\because$ $S$は零空間)．ここで $A$ の定義域を $T$ に制限した写像 $A^\prime : T \to\mathbb{R}^m$を考えると， $\mathrm{Ker}(A^\prime)=\{0\}$．よって$A^\prime$は単射であり，$\dim(\mathrm{Im}A^\prime)=\mathrm{dim}(T)$．$\mathrm{dim(\mathrm{Im} A)}=\mathrm{dim(\mathrm{Im} A^\prime)}$  であるから示された．

### 単調定理

<div class="box">

$n$ 次エルミート行列 $A,B$に対して， $A$ の固有値を $\alpha_1\leq\alpha_2\leq\ldots\leq\alpha_n$ ，$B$ の固有値を $\beta_1\leq\beta_2\leq\ldots\leq\beta_n$ ， $C:=A+B$ の固有値を $\gamma_1\leq\gamma_2\leq\ldots\leq\gamma_n$とする．

$$
\begin{align}
&\alpha_i+\beta_1\leq\gamma_i\leq \alpha_i+\gamma_n\,(i=1,2,\ldots,n)\\
&\gamma_i\geq\alpha_j+\beta_{i-j+1}\,(i\geq j)\\
&\gamma_i\leq\alpha_j+\beta_{i-j+n}\,(i\leq j)
\end{align}
$$

</div>

### 分離定理

<div class="box">

$$
A=\begin{bmatrix}
B&C\\
C^\ast&D
\end{bmatrix}
$$

を$A$が$n$次正方行列で固有値　$\alpha_1\leq\alpha_2\leq\ldots\leq\alpha_n$，$B$が$m$次正方行列で固有値　$\beta_1\leq\beta_2\leq\ldots\leq\beta_n$ ，をもつとき

$$
\begin{align}
\alpha_k\leq\beta_k\leq\alpha_{k+n-m}\,(k=1,2,\ldots,m)\\
\end{align}
$$

</div>

### クーランフィッシャーの定理(ミニマックス原理)

<div class="box">
$n$次エルミート行列$A$の固有値を $\alpha_1\leq\ldots\leq\alpha_n$ とする．

$$
\begin{align}
\alpha_k=\min_{S^k}\max\{\bm{x}^\ast A \bm{x} \mid \bm{x}\in S^k,|\bm{x}|=1\}\\
\alpha_k=\max_{S^k}\min\{\bm{y}^\ast A \bm{y} \mid \bm{y}\in S^k,|\bm{y}|=1\}
\end{align}
$$

ここで$S^k$は$\mathbb{C}^n$の任意の線形部分空間を表す．

</div>


## 参考

* [現代線形代数―分解定理を中心として― ](http://www.kyoritsu-pub.co.jp/bookdetail/9784320018815)
