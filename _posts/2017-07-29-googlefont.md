---
layout: post
title: JekyllでGoogle Fontsを利用する
tags: [jekyll,css,html]
---

## 背景
MacやiPhoneにはヒラギノフォントやhelveticaが入っているのでWebページが綺麗に表示されていいのですが，Windowsにはこれらのフォントは入っていないので違うものに置き換わってしまいます．またブラウザの設定によっても置き換わってしまうことがあります．

これを解決するために，OSやブラウザに依存しないwebフォントを利用することにしました．一番良さそうなものを調べたところ，google fontsのオープンソースの一部として提供されている[Google Fonts + Japanese Early Access](https://googlefonts.github.io/japanese/#notosansjapanese)の日本語フォントが綺麗で良さそうだったので利用することにしました．

## 方法

今回導入したのがNoto Sans Japaneseというフォントだったのでこれを例に説明します．[Google Fonts + Japanese Early Access](https://googlefonts.github.io/japanese/#notosansjapanese)にhtmlとcssのサンプルがあるので，これ見て適当なものを選べばいいと思います．

1.  `_layout/default.html`のヘッダ(`<head>`と`</head>`の間)に以下を追記します．

```html
<link href="https://fonts.googleapis.com/earlyaccess/notosansjapanese.css" rel="stylesheet" />
```

2.  `style.scss`の好きな要素の設定で`font-family: "Noto Sans Japanese"`を指定する．例えばp要素(本文)のフォントを変更したかったら，

```css
p {
  font-size: 17px;
  font-weight: 900;
}
```
のように書きます．`font-weight`というのは文字の太さでNoto Sans Japaneseでは以下の7種類に対応しています．太さは好みで適宜調整して下さい．

<h3 class="font-100">綺麗なWebフォントを使えます(font-weight:100)</h3>
<h3 class="font-200">綺麗なWebフォントを使えます(font-weight:200)</h3>
<h3 class="font-300">綺麗なWebフォントを使えます(font-weight:300)</h3>
<h3 class="font-350">綺麗なWebフォントを使えます(font-weight:350)</h3>
<h3 class="font-500">綺麗なWebフォントを使えます(font-weight:500)</h3>
<h3 class="font-700">綺麗なWebフォントを使えます(font-weight:700)</h3>
<h3 class="font-900">綺麗なWebフォントを使えます(font-weight:900)</h3>
