---
layout: post
title: BigQuery+pythonでBrunner-Munzel検定を行う。
tags: [statistics]
---

# モチベーション

2つの確率変数 $X_1, X_2$ に対して、これらが同じ分布に従うという帰無仮説を検定したいことがあります。
正規性が成り立たない場合に頑健なノンパラメトリック検定としてはWilcoxon-Mann-Whitney検定が有名ですが、Wilcoxon-Mann-Whitney検定は2つの分布の分散が異なる場合などに頑健でないことが知られています。
Brunner-Munzel検定は正規性が成り立たず、分散が異なる場合にも適用可能な検定の手法です。

Brunner-Munzel検定ではデータの順位を計算する処理がありますが、データがBigQuery上にある場合は順位計算などの重めの処理をBigQuery上で処理してしまうのが良いです。
本記事ではBrunner-Munzel検定をBigQuery+pythonで行う方法を紹介します。

# コード

2つのデータ列 `[1,2,1,1,1,1,1,1,1,1,2,4,1,1]` と `[3,3,4,3,1,2,3,1,1,5,4]` が同じ分布に従うかどうかを(奥村先生のブログにあるデータ例) Brunner-Munzel検定で確かめる。

実際のデータに適用する場合は `dataset_1` や `dataset_2` を検証したいものに置き換えれば良い。

## 統計量の集計

<script src="https://gist.github.com/MAEA2/ae81048a9177a7347d27f50c6af50ef4.js"></script>

上記のクエリをBigQueryで回すと、以下の結果が得られる。

| dataset_number | n   | avg_whole_rank     | variance           |
| -------------- | --- | ------------------ | ------------------ |
| 1              | 14  | 9.821428571428573  | 4.21565934065934   |
| 2              | 11  | 17.045454545454547 | 12.922727272727276 |

## t統計量/P値の計算

集計した統計量からt統計量を計算する。pythonのコードは以下。

<script src="https://gist.github.com/MAEA2/1af0a491631f07874fb33ee01925ff1a.js"></script>

```
$python brunner_munzel.py 14 11 4.21565934065934 12.922727272727276 9.821428571428573 17.045454545454547
# test statistic: 3.1374674823029496 degrees of freedom: 17.682841979481545 p-value: 0.0057862086661
```

これは、Rのパッケージである `brunner.munzel.test()` の値とも一致している(cf. [奥村先生のページ](https://oku.edu.mie-u.ac.jp/~okumura/stat/brunner-munzel.html))。

# 参考文献

- [Brunner-Munzel検定](https://oku.edu.mie-u.ac.jp/~okumura/stat/brunner-munzel.html)
- [マイナーだけど最強の統計的検定 Brunner-Munzel 検定](https://hoxo-m.hatenablog.com/entry/20150217/p1)
- [ScipyでBrunner-Munzel検定](https://ajhjhaf.hatenablog.com/entry/2018/12/22/160652)