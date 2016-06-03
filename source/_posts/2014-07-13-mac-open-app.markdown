---
layout: post
title: "Macで起動時にスクリプトを実行する方法"
date: 2014-07-13
comments: true
categories: [os, programming]
tags: [applescript, mac]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Macは、突然、従来のやり方が通用しなくなることがよくあります。<!--more--><br clear="all">

{% codeblock lang:bash %}
$ open -a Automator
{% endcodeblock %}

ワークフローをライブラリを使って作成し、アプリケーション形式で保存します。



ライブラリでは、シェルスクリプトやAppleScriptが使えます。





最終的には、`システム環境設定 -> ユーザーとグループ -> ログイン項目`で作成したアプリを登録します。


