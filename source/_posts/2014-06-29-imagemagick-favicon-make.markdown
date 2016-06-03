---
layout: post
title: "ImageMagickでFaviconを作成する方法"
date: 2014-06-29
comments: true
categories: [terminal]
tags: [cli, imagemagick, photo]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">検索で変換サイトを使うよりも確実です。<!--more--><br clear="all">

####マルチアイコンの作成

256、192、128、96、64、48、40、32、24、16のサイズでマルチアイコンを作ります。

{% codeblock lang:bash %}
$ convert icon.png -define icon:auto-resize favicon.ico
{% endcodeblock %}


####ファビコンの指定

ファビコンを指定するのは、`head`内に以下のタグを使います。

{% codeblock lang:bash %}
{% raw %}
<link rel="icon" href="/favicon.ico" />
{% endraw %}
{% endcodeblock %}

サイズの確認です。

{% codeblock lang:bash %}
$ identify favicon.ico
{% endcodeblock %}

このブログのファビコンも変更してみました。ただし、モバイルと分けているので、ブラウザによってどちらが表示されるか分かりませんが。



####iOS や Android 対応の ico ファイル作成する方法

{% codeblock lang:bash %}
$ convert -resize 152x152 icon.png favicon.png
{% endcodeblock %}

{% codeblock lang:bash %}
{% raw %}
<link rel="apple-touch-icon-precomposed" href="path/to/favicon.png">
{% endraw %}
{% endcodeblock %}

参考:

<a href="http://www.regentechlog.com/2014/04/03/imagemagick-multisize-ico/" target="_blank">ImageMagickでマルチアイコンを簡単に作る</a>


