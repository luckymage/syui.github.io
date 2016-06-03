---
layout: post
title: "Macでアクティブなウィンドウをコマンドラインから選択する方法"
date: 2014-09-30
comments: true
categories: [os, shell]
tags: [mac, applescript, shellscirpt, zsh]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">osx-select-windowというものを作りました。<!--more--><br clear="all">

インターフェイスは、`peco`ですので、注意です。

{% codeblock lang:bash %}
$ brew tap peco/peco

$ brew install peco
{% endcodeblock %}

{% githubrepo syui/osx-select-window %}

一時ファイル、キャッシュを作る処理をすると、素早く選択できるようになります。作っていませんが。

作ってもらえると嬉しいです。私も自分で使っていて、もし不便があるようなら作るかもしれませんが...。

