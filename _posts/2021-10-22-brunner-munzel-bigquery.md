---
layout: post
title: BigQuery+pythonでBrunner-Munzel検定を行う。
tags: [statistics]
thumbnail: "/images/avatar.png"
---

# モチベーション

2つの確率変数 $X_1, X_2$ に対して、これらが同じ分布に従うという帰無仮説を検定したいことがあります。
正規性が成り立たない場合に頑健なノンパラメトリック検定としてはWilcoxon-Mann-Whitney検定が有名ですが、Wilcoxon-Mann-Whitney検定は2つの分布の分散が異なる場合などに頑健でないことが知られています。
Brunner-Munzel検定は正規性が成り立たず、分散が異なる場合にも適用可能な検定の手法です。

Brunner-Munzel検定ではデータの順位を計算する処理がありますが、データがBigQuery上にある場合は順位計算などの重めの処理をBigQuery上で処理してしまうのが良いです。
本記事ではBrunner-Munzel検定をBigQuery+pythonで行う方法を紹介します。

# コード

[奥村先生のページ](https://oku.edu.mie-u.ac.jp/~okumura/stat/brunner-munzel.html)で使われているデータ例を用います。

2つのデータ列 `[1,2,1,1,1,1,1,1,1,1,2,4,1,1]` と `[3,3,4,3,1,2,3,1,1,5,4]` が同じ分布に従うかどうかを Brunner-Munzel検定で確かめます。

実際のデータに適用する場合は `dataset_1` や `dataset_2` を検定したいものに置き換えてください。

## 統計量の集計

<script src="https://gist.github.com/MAEA2/ae81048a9177a7347d27f50c6af50ef4.js"></script>

上記のクエリをBigQueryで回すと、以下の結果が得られる。

| dataset_number | n   | avg_whole_rank     | variance           |
| -------------- | --- | ------------------ | ------------------ |
| 1              | 14  | 9.821428571428573  | 4.21565934065934   |
| 2              | 11  | 17.045454545454547 | 12.922727272727276 |

## t統計量/P値の計算

集計した統計量からt統計量を計算します。pythonのコードは以下です。

<script src="https://gist.github.com/MAEA2/1af0a491631f07874fb33ee01925ff1a.js"></script>

```
$python brunner_munzel.py 14 11 4.21565934065934 12.922727272727276 9.821428571428573 17.045454545454547
# test statistic: 3.1374674823029496 degrees of freedom: 17.682841979481545 p-value: 0.0057862086661
```

## 検算

Rには`lawstat`パッケージにBrunner-Munzel検定を行うことができる関数 `brunner.munzel.test()` があります。
先程用いたデータ例を入力してみると同じ結果になっていることがわかります。

```r
> library("lawstat")
> x = c(1,2,1,1,1,1,1,1,1,1,2,4,1,1)
> y = c(3,3,4,3,1,2,3,1,1,5,4)
> brunner.munzel.test(x, y)

	Brunner-Munzel Test

data:  x and y
Brunner-Munzel Test Statistic = 3.1375, df = 17.683, p-value = 0.005786
95 percent confidence interval:
 0.5952169 0.9827052
sample estimates:
P(X<Y)+.5*P(X=Y) 
        0.788961 
```

# 参考文献

- [Brunner-Munzel検定](https://oku.edu.mie-u.ac.jp/~okumura/stat/brunner-munzel.html)
- [マイナーだけど最強の統計的検定 Brunner-Munzel 検定](https://hoxo-m.hatenablog.com/entry/20150217/p1)
- [ScipyでBrunner-Munzel検定](https://ajhjhaf.hatenablog.com/entry/2018/12/22/160652)