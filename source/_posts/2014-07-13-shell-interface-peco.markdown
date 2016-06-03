---
layout: post
title: "pecoを入れてみたり、coreOSを試してみたり"
date: 2014-07-13
comments: true
categories: [terminal, os, virtual]
tags: [coreos, go, vagrant]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">最近、試せていないこと多いのです。<!--more--><br clear="all">

##peco

{% githubrepo peco/peco %}

http://peco.github.io/

[percol](https://github.com/mooz/percol)を`golang`で書いた Shell Interface です。

といっても、出力を選択するというシンプルな機能。故に、手軽な使いやすさと取り込みやすさがあります。

###pecoのインストール

{% codeblock lang:bash %}
$ brew tap peco/peco

$ brew install peco
{% endcodeblock %}

###pecoの感想

予想通り、`python`の`percol`よりも速い印象。

##coreOS

###coreOSとは

`Gentoo`派生で、アプリケーションは基本、[Docker](https://coreos.com/using-coreos/docker/)から使うらしいです。

OS環境の切り替え、分散処理の簡易化に特化したOSという感じでしょうか。

<a href="http://qiita.com/mopemope/items/fa9424b094aae3eac580" target="_blank">CoreOS 入門 - Qiita</a>

###coreOSのインスール

{% codeblock lang:bash %}
$ git clone https://github.com/coreos/coreos-vagrant/

$ cd coreos-vagrant

$ vagrant up

$ vagrant ssh

$ docker run ubuntu echo test
{% endcodeblock %}

