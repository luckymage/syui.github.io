---
layout: post
title: "winetricksでsha1sum mismatch! Renameのエラーが出る場合、それを回避する方法"
date: 2014-07-23
comments: true
categories: [os]
tags: [linux, wine, winetricks]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">直接スクリプトを編集すると、エラーを回避できます。<!--more--><br clear="all">

{% codeblock lang:bash %}
{% raw %}
$ winetricks vcrun6
> sha1sum mismatch! Rename /home/{mainuser}/.cache/winetricks/vcrun6/vc6redistsetup_enu.exe and try again.

$ sha1sum ~/.cache/winetricks/vcrun6/vc6redistsetup_enu.exe
> afji48djsie494jaiodsdaoa045992vfdhsioj44 ~/.cache/winetricks/vcrun6/vc6redistsetup_enu.exe

$ sudo vim /usr/bin/winetricks
{% endraw %}
{% endcodeblock %}

ここで、ダウンロードしたファイルの`sha1sum`の結果を`load_vcrun6`の`w_download`の場所に記述します。

{% codeblock lang:bash /usr/bin/winetricks %}
load_vcrun6() {
- w_download http://storefront.steampowered.com/download/vc6redistsetup_enu.exe b058jifdja40jkfsdjalj4vcdla5brie4gfds44w
+ w_download http://storefront.steampowered.com/download/vc6redistsetup_enu.exe afji48djsie494jaiodsdaoa045992vfdhsioj44
}
{% endcodeblock %}


参考:

https://forum.winehq.org/viewtopic.php?f=8&t=16479

https://code.google.com/p/winetricks/issues/detail?id=227


