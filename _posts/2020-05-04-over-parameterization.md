---
layout : post
title: ニューラルネットのover-parameterizationについて最近の論文を読んだ。
tags: [machine-learning]
---

* index
{:toc}

# モチベーション

近年用いられるニューラルネットではデータ数に対してパラメータ数が非常に多い状況が多い。これは既存の学習理論の枠組みとは相反する。パラメータ数が非常に多いモデルのことをover-parameterized modelという。

# 2層の場合の結果

[1]では2層のニューラルネットで二乗損失を用いた場合に十分にユニット数で$m$が大きければ、勾配法による学習によって損失を限りなく小さくできることを示している。

## [1]の論文の設定

2層ニューラルネットは次式で定義される。ここで$\sigma$はReLUである。

$$
f(\boldsymbol{x};\boldsymbol{W},\boldsymbol{a})=\frac{1}{\sqrt{m}}\sum_{r=1}^ma_i\sigma(\boldsymbol{w}_r^\top\boldsymbol{x})
$$

次の二乗損失を最小化する。

$$
    L(\boldsymbol{W}, \boldsymbol{a}) = \sum_{i=1}^n \frac{1}{2}\left(y_i-f(\boldsymbol{x}_i;\boldsymbol{W}, \boldsymbol{a})\right)^2
$$

学習は勾配法で行う。

$$
\boldsymbol{W}(k+1) = \boldsymbol{W}(k)-\eta\frac{\partial L(\boldsymbol{W}(k), \boldsymbol{a})}{\partial\boldsymbol{W}(k)}
$$

## Neural Tangent Kernel

いま、損失を$L(\boldsymbol{W},\boldsymbol{a})=\sum_{i=1}^n \ell_i(f_{\boldsymbol{W}}(\boldsymbol{x}_i);\boldsymbol{a})$で定めておく。$\boldsymbol{a}$は固定するのがポイントになっている。Neural Tangent Kernelは2層ニューラルネットの勾配流を考えると出てくる量
で解析の際に重要な役割を果たす。学習のステップ幅を限りなく小さくすると、次の勾配流の式がでてくる。

$$
\frac{\mathrm{d}\boldsymbol{w}_r}{\mathrm{d}t}=-\nabla_{\boldsymbol{w}_r} L(\boldsymbol{W},\boldsymbol{a})
$$

ここで、

$$
\begin{align}
\frac{\mathrm{d}\boldsymbol{w}_r}{\mathrm{d}t}&=-\nabla_{\boldsymbol{w}_r} L(\boldsymbol{W},\boldsymbol{a})\\
&=-\sum_{i=1}^n \nabla_{\boldsymbol{w}_r} \ell_i(f_{\boldsymbol{W}}(\boldsymbol{x}_i);\boldsymbol{a})\\
&=-\sum_{i=1}^n \frac{\mathrm{d}\ell_i(f_{\boldsymbol{W}})}{\mathrm{d}f_{\boldsymbol{W}}}a_r\nabla_{\boldsymbol{w}_r}\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}_i)\\

\end{align}
$$

したがって、

$$
\begin{align}
\frac{\mathrm{d} f_{\boldsymbol{W}}(\boldsymbol{x})}{\mathrm{d}t}=&\sum_{r=1}^m\nabla_{\boldsymbol{w}_r}^\top f_{\boldsymbol{W}}\frac{\mathrm{d}\boldsymbol{w}_r}{\mathrm{d}t}\\
=&\sum_{r=1}^m\nabla_{\boldsymbol{w}_r}^\top f_{\boldsymbol{W}}\left(-\sum_{i=1}^n \frac{\mathrm{d}\ell_i(f_{\boldsymbol{W}})}{\mathrm{d}f_{\boldsymbol{W}}}\nabla_{\boldsymbol{w}_r}\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}_i)\right)\\
=&\sum_{r=1}^m\nabla_{\boldsymbol{w}_r}^\top f_{\boldsymbol{W}}(\boldsymbol{x})\left(-\sum_{i=1}^n \frac{\mathrm{d}\ell_i(f_{\boldsymbol{W}})}{\mathrm{d}f_{\boldsymbol{W}}}\nabla_{\boldsymbol{w}_r}\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}_i)\right)\\
=&\sum_{r=1}^ma_r\nabla_{\boldsymbol{w}_r}^\top\sigma(\boldsymbol{w}_r^\top\boldsymbol{x})\left(-\sum_{i=1}^n \frac{\mathrm{d}\ell_i(f_{\boldsymbol{W}})}{\mathrm{d}f_{\boldsymbol{W}}}\nabla_{w_r}\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}_i)\right)\\
=&-\sum_{i=1}^n\frac{\mathrm{d}\ell_i(f_{\boldsymbol{W}})}{\mathrm{d}f_{\boldsymbol{W}}}\underbrace{\sum_{r=1}^ma_r\nabla_{\boldsymbol{w}_r}^\top\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}) \nabla_{w_r}\sigma(\boldsymbol{w}_r^\top\boldsymbol{x}_i)}_{=:k_{\boldsymbol{W}}(\boldsymbol{x},\boldsymbol{x}_i)}
\end{align}
$$

$k_{\boldsymbol{W}}$をNeural Tangent Kernelという。多層の場合も中間層の出力を考えれば同様の手順で求めることができるはず。

## [1]の論文のキモ

他の論文でも繰り返し出てくるが、次のGram matrix $\boldsymbol{H}^\infty$が非常に重要な役割を果たす。

$$
\boldsymbol{H}^\infty_{i,j} = \mathbb{E}_{\boldsymbol{w}\sim\mathcal{N}(\boldsymbol{0},\boldsymbol{I})}\left[\boldsymbol{x}_i^\top\boldsymbol{x}_j\mathbb{I}_{\left\{\boldsymbol{w}^\top\boldsymbol{x}_i\geq 0\text{ and } \boldsymbol{w}^\top\boldsymbol{x}_j\geq 0\right\}}\right]
$$

## [1]の論文の主張

<div class='box'>

$\boldsymbol{w}_r\sim\mathcal{N}(\boldsymbol{0},\boldsymbol{I})$
, $a_r\sim\mathrm{unif}(0,1)$で初期化された2層ニューラルネットはユニット数を$m=\Omega\left(n^6/\lambda^4\delta^3\right)$にし、学習率$\eta=\Omega(\lambda_0/n^2)$をとすると確率$1-\delta$で次式が成り立つ。ここで$\boldsymbol{u}_i(k)=f(\boldsymbol{x}_i;\boldsymbol{W}(k),\boldsymbol{a})(i=1,2,\dots,n$である。

$$
\|\boldsymbol{u}(k)-\boldsymbol{y}\|_2^2\leq \left(1-\frac{\eta\lambda_0}{2}\right)^k\|\boldsymbol{u}(0)-\boldsymbol{y}\|_2^2
$$

</div>

## [2]の論文の設定

実は[2]の論文で$L(\boldsymbol{W},\boldsymbol{a})$の挙動の式が得られている。[2]では高い確率で

$$
L(\boldsymbol{W},\boldsymbol{a})\approx\frac{1}{2}\|(\boldsymbol{I}-\eta\boldsymbol{H}^\infty)^k\boldsymbol{y}\|_2^2
$$

が成り立つことが示されている。

## [2]の論文のキモ

## [2]の論文の主張

# 多層の場合の結果





# 参考文献

[1] [GRADIENTDESCENTPROVABLYO PTIMIZES OVER-PARAMETERIZEDNEURALN ETWORKS](https://arxiv.org/abs/1810.02054)

[2] [Fine-Grained Analysis of Optimization and Generalization for Overparameterized Two-Layer Neural Networks](https://arxiv.org/abs/1901.08584)

[3] [A Convergence Theory for Deep Learning via Over-Parameterization](http://arxiv.org/abs/1811.03962)

[4] [Gradient Descent Finds Global Minima of Deep Neural Networks](http://arxiv.org/abs/1811.03804)

[5] [Learning and Generalization in Overparameterized Neural Networks, Going Beyond Two Layers](https://arxiv.org/abs/1811.04918.)
