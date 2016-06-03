---
layout: post
title: "ClipMenuをコマンドラインから参照するスクリプト"
date: 2014-07-31
comments: true
categories: [os]
tags: [clipboard, mac, cli]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ちょっとだけ変更しました。<!--more--><br clear="all">

必要な物は、 <a href="https://github.com/peco/peco" target="_blank">peco</a>とか`xml`をパースする<a href="http://qiita.com/richmikan@github/items/e051b5d882c3dd2a39c6" target="_blank">スクリプト</a>とか。

{% codeblock lang:bash %}
$ curl -O https://gist.githubusercontent.com/richmikan/3251311/raw/290c70b9a45b5eb66036b83de79bfe6bb0b3b054/parsrx.sh

$ chmod +x !$:t
{% endcodeblock %}

<script src="https://gist.github.com/syui/fafe05df50c753b15e3d.js"></script>

