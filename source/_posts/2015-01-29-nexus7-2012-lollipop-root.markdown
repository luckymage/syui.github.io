---
layout: post
title: "Nexus7のlollipopをroot化する方法"
date: 2015-01-29
comments: true
categories: mobile
tags: [android, root]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">root化できました。twrpの2012と2013のイメージを間違えていただけでした。<!--more--><br clear="all">

すいません。[こちら](http://syui.github.io/blog/2015/01/28/android-5-dot-0-2-nexus7-root/)の記事も修正しておきました。

[http://techerrata.com/browse/twrp2/grouper](http://techerrata.com/browse/twrp2/grouper) ...2012

[http://techerrata.com/browse/twrp2/flo](http://techerrata.com/browse/twrp2/flo) ...2013

{% codeblock lang:bash %}
$ adb reboot bootloader

$ fastboot flash recovery openrecovery-twrp-2.8.4.1-grouper.img
{% endcodeblock %}

後は、予めインストールしておいた[supersu](https://play.google.com/store/apps/details?id=eu.chainfire.supersu&hl=ja)が`supersu installer`を発動しますので、それを実行し、`twrp`経由で`supersu`をインストールします。

