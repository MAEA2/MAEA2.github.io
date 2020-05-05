---
layout: post
title: 行列式の性質
tags: [math]
---

線形代数の復習として理解しておくべき行列式の性質についてまとめておきました．随時更新されていく予定です．

## 行列式の性質

### 定義
$A=\{a_{ij}\}\in\mathbb{R}^{n\times n}$の行列式$\det(A)$は

$$
\det(A):=\sum_{\sigma\in S}\prod_{i=1}^n \mathrm{sgn}(\sigma)a_{i\sigma(i)}
$$

ただし$S$は$(1,2,\ldots,n)$の置換列全体の集合．$\mathrm{sgn}(\sigma)$は$\sigma$が偶置換のときは$1$，奇置換のときは$-1$となる．

以下キャピタルは行列を表す．

### 行の公式

$$
\det(\bm{a}_1,\ldots,r\bm{a}_i,\ldots,\bm{a}_n)
=r\det(\bm{a}_1,\ldots,\bm{a}_i,\ldots,\bm{a}_n)
$$

$$
\det(\bm{a}_1,\ldots,\bm{a}_i,\ldots,r\bm{a}_i,\ldots,\bm{a}_n)=0
$$

### 列の公式

$$
A=\begin{pmatrix}
\bm{a}_1\\
\bm{a}_2\\
\vdots\\
\bm{a}_n
\end{pmatrix}
$$ とする．

$$
\det\begin{pmatrix}
\bm{a}_1\\
\vdots\\
r\bm{a}_i\\
\vdots\\
\bm{a}_n
\end{pmatrix}=r\det\begin{pmatrix}
\bm{a}_1\\
\vdots\\
\bm{a}_i\\
\vdots\\
\bm{a}_n
\end{pmatrix}
$$

$$
\det\begin{pmatrix}
\bm{a}_1\\
\vdots\\
\bm{a}_i\\
\vdots\\
r\bm{a}_i\\
\vdots\\
\bm{a}_n
\end{pmatrix}=0
$$

### 余因子展開
$A=\{a_{ij}\}$ とする．

$$
\begin{align*}
\det(A)&=\sum_{j=1}^n(-1)^{i+j}a_{ij}\det A[i,j]
\quad(i=1,2,\ldots,n)\\
&=\sum_{i=1}^n(-1)^{i+j}a_{ij}\det A[i,j]
\quad(j=1,2,\ldots,n)
\end{align*}
$$

ただし$A[i,j]$ は$A$より$i$行と$j$列を除いた行列．

$(-1)^{i+j}\det A[i,j]$ を $A$ の余因子といい，$\tilde{A}_{ij}$とかく．また

$$
\tilde{A}=\{\tilde{A}_{ji}\}
$$

を余因子行列という．成分が転置されているので注意する．
### 余因子行列の性質

$i$行で余因子展開を行うと

$$
\det(A)=\sum_{j=1}^na_{ij}\tilde{A}_{ij}
$$

$A[i,1],A[i,2],\ldots,A[i,n]$ はすべて $A$ の $i$ 行が除かれているので

 $$
 \tilde{A}_{i1},\tilde{A}_{i2},\ldots,\tilde{A}_{in}
 $$ は $A$ の $i$ 行の成分を含まない．いま行列 $A$ の $i$ 行目を $k$ 行目に書き換えた行列の行列式を考えると，これは行列式の性質より0となる．この行列式を余因子展開することで次の関係式が得られる．

$$
\sum_{j=1}^na_{kj}\tilde{A}_{ij}=0
$$

がわかる．
上の式で $k=i$ の場合は余因子展開を行っていることになるから，

$$
\sum_{j=1}^na_{kj}\tilde{A}_{ij}=\det(A)\delta_{ki}
$$

列についても同様に考えることで

$$
\sum_{i=1}^na_{ik}\tilde{A}_{ij}=\det(A)\delta_{kj}
$$

これより
$$
\begin{align*}
\tilde{A}^\top A=\det(A)E
\end{align*}
$$
### 逆行列公式
$A$が正則であるとき

$$
A^{-1}=\frac{\tilde{A}}{\det A}
$$


### ブロック行列の行列式
$$
\det
\begin{pmatrix}
A&C\\
O&B
\end{pmatrix}=\det
\begin{pmatrix}
A&O\\
C&B
\end{pmatrix}=\det(A)\det(B)
$$

### 積の行列式

$$
\det(AB)=\det(A)\det(B)
$$

### 固有値との関係

$$
\det(A)=\prod_{\lambda\in\mathsf{Spec}(A)}\lambda
$$


ただし $\mathsf{Spec}(A)$は$A$の重複も含めた$n$個の固有値の集合．
