---
layout: post
title: 院試の問題を数値計算で検算した
tags: [math,statistics,python,numerical_analysis]
---

**注. この記事を書いた日付院試直後ですが、記事の公開は本入試問題がWebで公開されてから行っています。**

## 問題

京都大学システム科学専攻・専門科目・確率統計　問題[1]　より抜粋．

標本$X_1,X_2,\ldots,X_n,Y_1,Y_2,\ldots,Y_m$は$X_1,X_2,\ldots,X_n\sim\mathcal{N}(a\theta,\sigma^2),Y_1,Y_2,\ldots,Y_m\sim\mathcal{N}(b\theta,\sigma^2)$であり各々が独立であるとする．

このとき$\theta,\sigma^2$の最尤推定量を求めなさい．

## 解答

尤度関数$L(\theta,\sigma^2)$は

$$
L(\theta,\sigma^2)=\frac{1}{(2\sigma^2\pi)^{m+n/2}} \exp\left[-\sum_{i=1}^n\frac{(X_i-a\theta)^2}{2\sigma^2}-\sum_{i=1}^m\frac{(Y_i-b\theta)^2}{2\sigma^2}\right]
$$

微分して

$$
\begin{align}
&\frac{\partial\log L(\theta,\theta)}{\partial\theta}=\sum_{i=1}^n\frac{a(X_i-a\theta)}{\sigma^2}+\sum_{i=1}^m\frac{b(Y_i-b\theta)}{\sigma^2}=0\\
&\frac{\partial\log L(\theta,\theta)}{\partial\sigma^2}=-\frac{m+n}{2}\frac{1}{\sigma^2}+\sum_{i=1}^n\frac{(X_i-a\theta)^2}{2(\sigma^2)^2}+\sum_{i=1}^m\frac{(Y_i-b\theta)^2}{2(\sigma^2)^2}=0
\end{align}
$$

$\theta,\sigma^2$の最尤推定量$\hat{\theta},\hat{\sigma^2}$はそれぞれ



$$
\begin{align}
&\hat{\theta}=\frac{a\sum_{i=1}^nX_i+b\sum_{i=1}^mY_i}{na^2+mb^2}\\
&\hat{\sigma^2}=\frac{\sum_{i=1}(X_i-a\hat{\theta})^2+\sum_{i=1}^m(Y_i-b\hat{\theta})^2}{m+n}
\end{align}
$$

## 検算


```python
#実験してみましょう
import numpy as np
import numpy.random as random
theta=random.rand()*10
sigma=random.rand()*10
a=random.rand()
b=random.rand()
n=1000000
m=2000000
X=random.normal(loc=a*theta,scale=sigma,size=n)
Y=random.normal(loc=b*theta,scale=sigma,size=m)
print("theta= %f" % theta)
print("sigma^2= %f" % (sigma*sigma))
```

    theta= 8.835112
    sigma^2= 28.617020



```python
theta_hat=(a*X.sum()+b*Y.sum())/(n*a**2+m*b**2)
sigma_hat=(((X-a*theta_hat)*(X-a*theta_hat)).sum()+((Y-b*theta_hat)*(Y-b*theta_hat)).sum())/(m+n)
print("theta_hat=%f" % theta_hat)
print("sigma^2_hat=%f" % sigma_hat)
```

    theta_hat=8.838706
    sigma^2_hat=28.597740

## 過去問
