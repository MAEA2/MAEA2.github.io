---
layout: post
title: forkしてきたレポジトリの最新状態を取ってくる
tags: [github]
---

まずforkしてきたレポジトリをupstream(別にこの名前でなくても良い)名前で登録するためforkしたローカルレポジトリに移動して以下のコマンドを実行。

```
git remote add upstream フォークしたレポジトリのURL
```

これでフォーク元が`upstream`という名前で登録されます。
あとはupstreamの内容を以下のコマンドでとってきて

```
git fetch upstream
```

次のコマンドでマージして完了。
```
git merge upstream/master
```

### 参考
[GitHubでFork/cloneしたリポジトリを本家リポジトリに追従する](http://qiita.com/xtetsuji/items/555a1ef19ed21ee42873)
