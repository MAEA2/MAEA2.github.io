---
layout: post
title: Uplift Modelingについて
tags: [machine-leanring]
---

個人の覚書としてまとめた。

# Uplift Modelingとは

## ひとことで

なんらかの介入を行ったときに、目的の変数にどれだけの影響があるかをデータから予測する手法をUplift Modelingという。

## Upliftとはなにか

「なんらかの介入を行ったときに、目的の変数にどれだけの影響があるか」をUplift という。これは数式で書くと次のようになる。

## Upliftの定義

まず必要な変数を定義する。

$$
\begin{align*}
&Y\in\{0,1\} : \text{目的の変数(例は Upliftの例 を参照)}\\
&A\in\{0,1\} : \text{処置変数(介入を行った: 1, 介入を行わなかった: 0)}
\end{align*}
$$

Upliftとは介入を行った場合と行わなかった場合とで条件づけたときに、目的の変数が$Y=1$を取る確率の差である。

つまり、$\mathrm{Uplift}$は

$$
\mathrm{Uplift} := \mathbb{P}[Y=1|A=1] - \mathbb{P}[Y=1|A=0]
$$

で定義される。Upliftが正の値をとるとき、その介入は目的の変数に対して正の効果を持っていると考えられる。


## Upliftの例

- 商品広告をユーザーに表示するかどうかで($A=1$:表示した, $A=0$:表示していない)、ユーザーが商品を買うかどうか($Y=1$: 購入, $Y=1$: 非購入)。
- ある患者に新薬を投与したかどうかで($A=1$: 投与した, $A=0$: 投与しない)に、病気から回復するかどうか($Y=1$:回復した, $Y=0$:回復しなかった)

## Uplift Modelingとは

Uplift ModelingとはUpliftをデータから予測しようとする手法のことである。

## Uplift ModelingとA/Bテストとの違い

介入の効果を調べる類似手法として、A/Bテストがある。A/Bテストは介入を行った集団(A)と介入を行わなかった集団(B)を用意することで、介入の集団への平均的な効果を測る手法である。
Upliftは集団に対する介入の効果ではなく、個人への介入の効果を指している。A/Bテストで知りたいような集団への介入効果は**average treatment effect**と呼ばれ、
Upliftのような個人への介入効果は**individual treatment effect**と呼ばれている。

## Uplift Modelingで何をしたいか。

個人ごとのUpliftを知ることができれば、個人ごとに介入を行うかどうかを決定するのに役立つ。
商品の広告を例にとると、Upliftが正であるユーザーに広告を表示するのが良いと考えられる。逆にUpliftが負のユーザーに対しては広告は購買確率を下げることになるので、広告を表示しないほうが良いと考えられる。

## Uplift Modelingの指標

Uplift Modelingの指標としてはAUUC(area under the uplift curve)が用いられる事が多い。

### Average Uplift

次で定義される量。ユーザー全体に介入を行った/行わないを介入確率に従って決めた場合のUpliftの期待値

$$
\text{Average Uplift} := \mathbb{E}_{\text{ユーザー}}[\text{ユーザーのuplift}\times\text{ユーザーへの介入確率}]
$$

### AUUCの定義


# 参考文献
- [Uplift modeling for clinical trial data](http://people.cs.pitt.edu/~milos/icml_clinicaldata_2012/Papers/Oral_Jaroszewitz_ICML_Clinical_2012.pdf)

