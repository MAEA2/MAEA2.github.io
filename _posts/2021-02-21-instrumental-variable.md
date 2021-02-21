---
layout: post
title: 操作変数法について
tags: [github]
---

# 操作変数とはなにか

[Angrist, Graddy,
and Imbens [2000]](https://scholar.harvard.edu/imbens/publications/interpretation-instrumental-variables-estimators-simultaneous-equations-models-a)
にある魚の市場の例をもとに説明をする。

魚の価格と魚の需要の関係を調査したいというような問題を考える。ある日$i$の魚の価格を$W_i$、魚の需要を$Y_i$とする。価格と需要が独立であるとは考えにくいので( $Y_i \perp W_i$ ではない)、unconfoundnessはそのままでは成り立たない。

そこで、その日の天候$Z_i\in\mathbb{R}$を考える(漁日和かどうかを数値化したスコアみたいなものだと仮定する)。

嵐の日は魚を獲ることが難しくなるので、魚の価格は上がりやすく、逆に晴天の日は魚を獲りやすいので魚の価格は下がりやすいと考えられる。よって$W_i$と$Z_i$は相関していると考えられる。

魚の需要と天候については一般的に関係ないと考えられるので(次の日が嵐なので、魚がより食べたくなるみたいな関係はおそらくない)、$Y_i$と$Z_i$は無相関と考えられる。

そこで、このような気持ちを反映して次のようなモデルを仮定する。

$$
\begin{align}
& Y_i = \alpha + W_i\tau + \varepsilon_i,\quad\varepsilon_i\perp Z_i\\
& W_i = Z_i\gamma + \eta_i
\end{align}
$$

$\tau$が魚の価格に対して、需要に与える影響を表すパラメータである。このモデルを正しいとすると、魚の価格と魚の需要の関係を調査したいという問題は$\tau$ をデータから推定したいという問題に帰着させることができる。

いま、$\varepsilon_i\perp Z_i$であることから

$$
\mathop{\mathsf{Cov}}[Y_i, Z_i] = \mathop{\mathsf{Cov}}[W_i\tau + \varepsilon_i, Z_i] = \tau\mathop{\mathsf{Cov}}[W_i, Z_i]
$$

の関係が成り立つ。

したがって、

$$
\tau = \frac{\mathop{\mathsf{Cov}}[Y_i, Z_i]}{\mathop{\mathsf{Cov}}[W_i, Z_i]}
$$

となる。このように$Z_i$を介することで、$Y_i$と$W_i$にunconfoudnessが成り立たない状況でも $\tau$ を推定できる状況になっている(識別可能になっている)。このような変数 $Z_i$ のことを操作変数という。

<div class="definition">
<div class='box-title'>操作変数の定義</div>
アウトカム$Y_i$に関して外生的($\varepsilon_i\perp Z_i$)かつ$\mathop{\mathsf{Cov}}[W_i, Z_i]\neq 0$であるような変数を操作変数という。
</div>

上のモデルの例のように、$Z_i$は$W_i$を通じてのみ$Y_i$に影響を与えている。この条件をexclusion restriction という。

# 最適な操作変数

上の例では操作変数$Z_i$の値域は$\mathbb{R}$であったが、操作変数の値域が一般の集合$\mathcal{Z}$であるような状況を考える。$\mathcal{Z}$としては例えば適当な $\mathbb{R}^n$の部分集合などを想定している。

このような状況でも上の例と同様の議論により$\mathop{\mathsf{Cov}}[W_i, w(Z_i)]\neq 0$ であるような関数 $w:\mathcal{Z}\to\mathbb{R}$ について、

$$
\tau = \frac{\mathop{\mathsf{Cov}}[Y_i, w(Z_i)]}{\mathop{\mathsf{Cov}}[W_i, w(Z_i)]}
$$

を成立させることができる。ある$w$を指定することで、上式の共分散の一致推定量を代入した$\tau$の推定量$\tau_w$を考えることができる。
このような $w$ の候補は複数あるのでどの関数$w$を選ぶかという問題が生じるが、$n(\tau-\hat{\tau}_w)$の漸近分散が最も小さくなるような推定量を考えることで、

$$
w^\ast \propto \mathbb{E}[W_i|Z_i=z]
$$

という解が導かれる。つまり最適な関数$w^\ast$は$W_i$を$Z_i$から最もよく予測する関数の定数倍という条件を満たす。詳しい導出については[Causal Inference(スタンフォード大学の講義資料, stats361)](https://web.stanford.edu/~swager/stats361.pdf)を参照のこと。

# 共変量調整との関係

操作変数の仮定は共変量$X_i$についての条件付き独立の設定に拡張可能で、$\epsilon_i \perp \mid X_i$ となる。この設定での詳細な解析については[Abadie [2003]](https://economics.mit.edu/files/11873) で行われている。[Athey, Tibshirani, and Wager [2019]](https://arxiv.org/abs/1610.01271) では$X_i=x$のときの因果効果$\tau(x)$の推定方法についての手法が提案されている。


# 参考文献

- [Angrist, Graddy,
and Imbens [2000]](https://scholar.harvard.edu/imbens/publications/interpretation-instrumental-variables-estimators-simultaneous-equations-models-a)
- [Causal Inference(スタンフォード大学の講義資料, stats361)](https://web.stanford.edu/~swager/stats361.pdf)