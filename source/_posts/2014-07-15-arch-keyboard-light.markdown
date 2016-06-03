---
layout: post
title: "ArchLinxuでMacBookAirのキーボードを光らせる"
date: 2014-07-15
comments: true
categories: [os]
tags: [arch]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">MacBookにLinuxを入れると、色々と設定が面倒です。<!--more--><br clear="all">


スクリプトが用意されていますので、それを使えば簡単ですね。

{% codeblock lang:bash %}
$ git clone https://github.com/hobarrera/kbdlight/

$ cd !$:t

$ sudo make

$ sudo make install

$ sudo ./kbdlight max
{% endcodeblock %}

<a href="https://wiki.archlinux.org/index.php/MacBook_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">MacBook (日本語) - ArchWiki</a>
