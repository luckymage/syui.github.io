---
layout: post
title: "xbindkeysを使ってChromium用のキー設定を行なう方法"
date: 2015-03-26
comments: true
categories: os
tags: [linux, archlinux, xbindkeys]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Chromiumを操作する時に、`C-w`で単語を削除する設定です。<!--more--><br clear="all">

一つの方法としては、以下のような方法が考えられます。(関係無いですが`curl | sh`でのインストール方法にハマった...1行目の`#!`が不要でした)

{% githubrepo syui/arch-chromium-xbindkeys-emacs %}

インストールは以下のような感じでできます。

{% codeblock lang:bash %}
$ curl -L https://raw.githubusercontent.com/syui/arch-chromium-xbindkeys-emacs/master/i.sh | sh
{% endcodeblock %}


