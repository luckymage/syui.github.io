---
layout: post
title: "MacのBluetoothの音質を良くする方法"
date: 2014-09-05
comments: true
categories: os
tags: [ mac, bluetooth ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">デフォルトでどうなってるのか知りませんが。ちなみに、音質良くなってるのかもよく分かってませんが。<!--more--><br clear="all">

{% codeblock lang:bash %}
# apt-Xを有効にする
$ defaults write com.apple.BluetoothAudioAgent "Enable AptX codec" -bool true

# 確認
$ defaults read com.apple.BluetoothAudioAgent

# 設定の削除
$ defaults delete com.apple.BluetoothAudioAgent "Enable AptX codec"
{% endcodeblock %}
