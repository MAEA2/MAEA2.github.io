---
layout: post
title: ラグランジュの未定乗数法
tags: [math]
---


## 動機
ラグランジュの未定定数法でよく下図のような絵を書いて，目的関数の勾配と等式制約の勾配がいい感じに比例するような点が停留点になっているんだ！というような幾何的イメージによった説明をよく見かけます．

![こんな感じの絵](https://upload.wikimedia.org/wikipedia/commons/b/bf/LagrangeMultipliers2D.svg)

僕はこの説明があまり好きではありません．これだと**等式制約がたくさんある場合**，さっきのイメージでは説明がつかなくなってしまいます．

そこで，この記事ではラグランジュの未定乗数法の幾何的なイメージではなく，式の意味を中心に説明したいと思います．

## 問題設定

 $f(\boldsymbol{x})$: $\mathbb{R}^n$上で定義された目的関数

 $g_i(\boldsymbol{x})=0\,(i=1,2,\ldots,m)$: 等式制約

 等式制約をみたすような$\boldsymbol{x}$で停留点をみつけたい．

## ラグランジュの未定乗数法

 ラグランジュの未定定数法では$f(\boldsymbol{x})$の代わりに

 $$
 F(\boldsymbol{x},\boldsymbol{\lambda})=f(\boldsymbol{x})-\sum_{i=1}^m\lambda_ig_i(\boldsymbol{x})
 $$

という関数を考えます．この関数の停留点をためしに求めてみましょう．微分すると$\eqref{1}$,$\eqref{2}$が出てきます．

$$
\begin{align}
&\nabla F(\boldsymbol{x})=\nabla f(\boldsymbol{x})-\sum_{i=1}^m\lambda_i\nabla g_i(\boldsymbol{x})=\boldsymbol{0}
\label{1}\\
&\frac{\partial F}{\partial \lambda_i}=-g_i(\boldsymbol{x})=0\,(i=1,2,\ldots,m)
\label{2}
\end{align}
$$

$\eqref{1}$は$\nabla f$が$\nabla g_i$の線形結合でかけるということを示しています．$\eqref{2}$は$\boldsymbol{x}$が等式制約を満たすということを示しています．
## これでいいのか

$\eqref{1}$で$\nabla f$が$\nabla g_i$の線形結合でかけることを要請しましたが，これを満たさないようなもので等式制約を満たす$\boldsymbol{x}$は無いのでしょうか？．制約集合(等式制約を満たす点)というのは$M$個の超曲面$g_i(\bm{x})=0\,(i=1,2,\ldots,m)$の共通部分です．実はラグランジュの未定定数法では次の条件を課しています．


* 制約集合上の点$\boldsymbol{x}_0$の制約集合近傍は$\boldsymbol{x}_0$を通る$m$個の接平面で近似できる．


この仮定があるので，$\nabla f$が$\nabla g_i$の張る空間に制限されることになります．
上の仮定が成り立つ条件としては以下の十分条件が知られています．


* $\nabla g_i(\bm{x})\,(i=1,2,\ldots,m)$が線形独立


## 参考

[ラグランジュの未定乗数法](https://ja.wikipedia.org/wiki/ラグランジュの未定乗数法)

[ラグランジュの未定乗数法について](http://fd.kuaero.kyoto-u.ac.jp/sites/default/files/Lagrange1.pdf)
