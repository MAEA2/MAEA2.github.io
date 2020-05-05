---
layout : post
title : Cauchy-Schwarzの不等式
tags: [math]
---

院試を解いてて次の不等式で立ち止まってしまったのでメモ。

$$
\left(\int_a^bf(x)\,dx \right)^2\leq(b-a)\int_a^bf(x)^2\,dx
$$

これはCauchy-Schwarzの不等式から直ちに出てきます。


### Cauchy-Schwarzの不等式

$$
\left(\int_a^bf(x)g(x)\,dx\right)^2\leq\int_a^b[f(x)]^2\,dx\int_a^b [g(x)]^2\,dx
$$

Cauchy-Schwarzの不等式で$g(x)\equiv 1$とすると

$$
\left(\int_a^bf(x)\,dx\right)^2\leq\int_a^b[f(x)]^2\,dx\int_a^b \,dx=(b-a)\int_a^b[f(x)]^2\,dx
$$

より上の不等式は成り立ちます。

<div class='proof'>

[証明]

$t$の$2$次方程式

$$
\int_a^b(tf(x)-g(x))^2\,dx=0
$$

を考える。この左辺は非負なので根の数はたかだか1つ。よってこの2次方程式の判別式$D$は$0$以下となる。

$$
\int_a^b(tf(x)-g(x))^2\,dx=t^2\int_a^b[f(x)]^2\,dx-2t\int_a^bf(x)g(x)\,dx+\int_a^b [g(x)]^2\,dx
$$

であるから

$$
\frac{D}{4}=\left(\int_a^bf(x)g(x)\,dx\right)^2-\int_a^b[f(x)]^2\,dx\int_a^b [g(x)]^2\,dx\leq 0
$$

よって不等式が成立する。

</div>
