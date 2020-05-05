---
layout: post
title: 主成分分析の気持ち
tags: [math, statistics]
---

主成分分析が何を解きたいかということを考えると自分のなかで一番しっくりくる説明を書いてみました。

<div class="box">

平均が$\boldsymbol{0}$となる$p$次元のデータ$\{\boldsymbol{x}_{i}\}_{i=1}^N \subset \mathbb{R}^p$が与えられたときに、元のデータをなるべく損なわないような正規直交系(長さが1で互いに直交するようなベクトルの組)$\{\boldsymbol{u}_i\}_{i=1}^d\subset \mathbb{R}^p$ を見つけてくる。
</div>

$p$次元ベクトルは1次独立なベクトルが$p$個あれば、それらの線型結合によって表現することができるので、ここでは $d < p$ となる状況を考えています。つまり$p$次元のデータを$d$ 個の直交系を使うことにより「圧縮」して表現してやろうというわけです。

ここで、「元のデータをなるべく損なわない」の定義は何なのかという疑問が生じますが、ここでは次のような定義を採用します。

<div class="box">

$\{\boldsymbol{u}_{i}\}_{i=1}^d$で張られる空間にデータ $\{\boldsymbol{x}_{i}\}_{i=1}^N$ を直交射影したときの2乗距離の平均が最小になるようにとる。

</div>

「損なわれなさ」に2乗距離を採用することに数学的な必然性はありません。ただ、最小2乗法などを考えるとわかるようにこうすると後の計算が楽になります。

いま、ベクトル$\boldsymbol{x}\in\mathbb{R}^p$を

$$
\{\boldsymbol{u}_i\}_{i=1}^d
$$ 

で張られる空間に直交射影したベクトルを考えます。

これは $\boldsymbol{U}\boldsymbol{U}^\top\boldsymbol{x}$ と表されます。


なぜなら、直交系で張られる空間に対する射影であることから射影ベクトルは

$$
\sum_{i=1}^d (\boldsymbol{u}_{i}^\top \boldsymbol{x}_{i}) \boldsymbol{u}_{i}
$$ 

とかけるからです。

ここで 

$$
\boldsymbol{U} = [\boldsymbol{u}_1, \ldots, \boldsymbol{u}_{d}]\in \mathbb{R}^{p\times d}
$$ 

と置いています。

これより、主成分分析は次のような問題を解くことになります。

$$
\begin{align}
&\text{minimize}\,\,\frac{1}{N}\sum_{i=1}^N \|\boldsymbol{x}_i - \boldsymbol{U}\boldsymbol{U}^\top\boldsymbol{x}_i\|^2\\

& \text{s.t.}\quad \boldsymbol{U}^\top \boldsymbol{U} = \boldsymbol{I}_d
\end{align}
$$

よく主成分分析を説明するときに、データの散らばりが最大になるように分散共分散行列の固有値の大きなものから固有ベクトルを取っていけばよいというような説明がなされますが、これは主成分分析の気持ちとはややずれていると思います。2乗距離が最小になるような直交系をみつけてくるというような説明のほうがしっくりきます。
