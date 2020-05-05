---
layout : post
title : 正方行列の固有値の実部が1未満$\Longleftrightarrow$行列の冪の極限は零行列
tags: [math]
---

ジョルダン標準形を用いて示します。
ジョルダンブロック $J(\lambda,k)\in\mathbb{R}^{k\times k}$ とは

$$
\begin{align}
J(\lambda,k)=\begin{pmatrix}
\lambda&1&0&\cdots&0&0\\
0&\lambda&1&0&\cdots&0\\
&&\ddots&&&\\
0&0&0&\cdots&\lambda&1\\
0&0&0&\cdots&0&\lambda
\end{pmatrix}
\end{align}
$$

という形の行列です。
ジョルダンブロックの冪について$n \geq k$のときジョルダンブロックの冪は次の式で表せます。

$$
\begin{align}
(J(\lambda,k))^n=\begin{pmatrix}
\lambda^n&\binom{n}{1}\lambda^{n-1}&\binom{n}{2}\lambda^{n-2}&\cdots&\binom{n}{k-2}\lambda^{n-k+2}&\binom{n}{k-1}\lambda^{n-k+1}\\
0&\lambda^n&\binom{n}{1}\lambda^{n-1}&\binom{n}{2}\lambda^{n-2}&\cdots&\binom{n}{k-2}\lambda^{n-k+2}\\
&&\ddots&&&\\
0&0&\cdots&\cdots&\lambda^n&\binom{n}{1}\lambda^{n-1}\\
0&0&0&\cdots&\cdots&\lambda^n
\end{pmatrix}
\end{align}
$$

### 証明

帰納法と二項係数に関する関係式

$$
\begin{align}
\binom{n+1}{k}=\binom{n}{k}+\binom{n}{k-1}
\end{align}
$$

から示すことができます。
全ての行列はジョルダンブロックの直和で表すことができるので(ジョルダン標準形を持つ)ので正方行列$A$の固有値の実部が全て1未満ならばジョルダンブロックの冪が収束して

$$
\textsf{Spec}(A)<1\iff\displaystyle\lim_{n\to\infty}A^n=O
$$

が成り立ちます。逆は逆にたどると示せます。
