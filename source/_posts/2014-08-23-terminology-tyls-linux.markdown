---
layout: post
title: "ターミナル上で画像や動画を再生するTerminology"
date: 2014-08-23
comments: true
categories: [ os, terminal ]
tags: [ linux, terminal ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ターミナル上で画像や動画のサムネイルを表示したい場合はおすすめです。<!--more--><br clear="all">



{% codeblock lang:bash %}
$ sudo pacman -S terminology emotion_generic_players

$ terminology

$ cd ~/Pictures

$ tyls -m
{% endcodeblock %}

> screen, tmuxとかでは表示できない場合もあるので注意。



####tyls

ファイル一覧を表示します。

####tycat

個別ファイルを指定します。

####tybg

ファイルをバックグラウンドで再生します。

####typop

ポップアップ表示です。

