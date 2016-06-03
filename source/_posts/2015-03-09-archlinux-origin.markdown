---
layout: post
title: "archlinux-origin"
date: 2015-03-09
comments: true
categories: os
tags: [arch,android,usb]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">最近、Arch化が進行しています。<!--more--><br clear="all">

![](http://lh4.ggpht.com/-0Npa6eEZa8k/VP1bctn48rI/AAAAAAAAAhM/K7N-PLtJdPw/Screenshot_2015-03-09-17-26-09.jpg)

MacBookにも、Androidも、USBもArchと、最近、Arch Linux化が自分の中で進行中です。一部、独自改造して使っていますが、一般的な設定スクリプトは以下に置きました。

{% githubrepo syui/arch-setup %}

{% githubrepo syui/arch-android %}

ちなみに、[こちら](http://www.amazon.co.jp/dp/B00SGPG6I6)のUSBを購入し、Arch Linuxを入れたのですが、microUSBを採用しているため、それを、Androidでマウントすることもできます。

![](http://lh3.ggpht.com/-kQ-aH5eyqbc/VP1baQnUIbI/AAAAAAAAAhI/tzdDh6vM4oA/Screenshot_2015-03-09-17-26-09.png)

{% codeblock lang:bash %}
$ ls /dev/block/sda*

$ mkdir -p /sdcard/mnt

$ mount -t ext4 /dev/block/sda2 /sdcard/mnt

$ df /sdcard/mnt
{% endcodeblock %}

こうしておくことで、Archというのは、割りと壊れる事が多いので、Androidで修正できるようにしておくと便利だと思われます。

