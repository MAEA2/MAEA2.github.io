---
layout: post
title: スクレイピングとMeCabを使う練習
tags: [python]
---

## 知恵袋の関連する質問

知恵袋の質問文を集めてスクレイピングの練習．
ある質問の下辺りにあわせて知りたいみたいなのがある．これは今見ている質問に関連した質問を表示してくれている．


![あわせて読みたい](/images/related.png)


```python
from urllib.request import urlopen
from bs4 import BeautifulSoup
from urllib.error import HTTPError
from urllib.error import URLError
import sys,io
import re
import MeCab


def get_question(url):
    try:
        html=urlopen(url)
    except HTTPError as e:
        print(e)
        #return, null, break, or do plan B which is altenertive to plan A
    except URLError as e:
        print("URL is wrong!")
    else:
        pass
    bsObj=BeautifulSoup(html.read(),"lxml")
    name=bsObj.find("meta",{"property":"og:title"})
    return name.attrs["content"]



def get_related_question(url):
    related_links=[]
    questions=[]
    try:
        html=urlopen(url)
    except HTTPError as e:
        print(e)
        #return, null, break, or do plan B which is altenertive to plan A
    except URLError as e:
        print("URL is wrong!")
    else:
        pass
    bsObj=BeautifulSoup(html.read(),"lxml")

    for link in bsObj.find("div",{"class":"md_listCmmn"}).findAll("a"):
        if "href" in link.attrs:
            related_links.append(link.attrs["href"])
    for link in related_links:
        questions.append(get_question(link))
    return questions

url="https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q10177422190"
l=get_related_question(url)
#wakatiko
m = MeCab.Tagger ("-Owakati")
for q in l[:5]:
    print(m.parse (q))
```

    海水 魚 を 飼っ て た 水槽 で 金魚 を 飼お う と 思う けど どう し たら いい です か ？

    今日 子供 が お 祭り に 行き 帰っ て 来 たら 金魚 を 持ち帰っ て き まし た 。 うち に はらん ち ゅうがいてそのらんちゅうと 同じ 水槽 に 入れ て いい か 考え て い ます 。 病気 を もっ て たら や だ ...

    水槽 による 天井 から の 水 漏れ

    ザリガニ と 金魚 を 共存 さ せ たい

    水槽 の 後ろ に 貼る 壁紙 ？ の よう な もの は




```python

```
