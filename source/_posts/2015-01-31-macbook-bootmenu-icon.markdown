---
layout: post
title: "Macのブートメニューにアイコンを表示できるということで設定して遊んでみた"
date: 2015-01-31
comments: true
categories: os
tags: mac
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">`/.volumeicon.icns`を置くと良いらしいです。<!--more--><br clear="all">


https://www.iconfinder.com/icons/386477/mac_os_x_icon

{% codeblock lang:bash %}
#Macのディスクにアイコンを設定する
$ sudo cp 設定したいファイル /.volumeicon.icns

#復旧ディスクにアイコンを設定する
$ diskutil list
$ mkdir mnt
$ sudo mount -t hfs /dev/disk0s3 ./mnt
$ sudo cp 設定したいファイル ./mnt/.volumeicon.icns
{% endcodeblock %}

![](http://lh6.ggpht.com/-tpivihivnbE/VMxIk-NCr9I/AAAAAAAAAVk/xC4G44Gn-xs/boot_icons.png)
