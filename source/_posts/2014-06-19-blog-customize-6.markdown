---
layout: post
title: "画像に余白を設定する場合の処置"
date: 2014-06-19
comments: true
categories: [blog]
tags: [octopress, github, html, css]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">画像を中央に近づける。<!--more--><br clear="all">


画像の左右に`margin`で余白を設定します。しかし、それでは画面いっぱいの画像を中央に表示することが難しくなります。

したがって、`max-width`を`100%`ではなく、`90%`で調整します。

{% codeblock lang:css %}
img {
white-space: inherit;
margin:0 7px 0 7px;
}

.flex-content, article img, article video, article .flash-video {
max-width: 97%;
}
{% endcodeblock %}

