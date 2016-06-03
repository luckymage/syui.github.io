---
layout: post
title: "command-stream"
date: 2014-09-25
comments: true
categories: shell
tags: zsh
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">流れる文字列を扱うコマンドストリームというツールを作った<!--more--><br clear="all">

{% githubrepo syui/command-stream %}

コマンドを引数1に渡すと、そのコマンドの実行結果を特定の文字数(引数2)で流してくれます。

```
$ ./command-stream "{command}" {count}
```

引数なしでもデフォルトが設定されていますので、`Mac`では有効だと思いますが、分かりません。デフォでは、ディスクを流します。`df | grep disk`

```
$ ./command-stream
```

