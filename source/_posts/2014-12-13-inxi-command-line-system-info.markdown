---
layout: post
title: "システム情報の確認にinxiが便利だった件"
date: 2014-12-13
comments: true
categories: [linux, shell]
tags: [ arch, zsh]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">inxi<!--more--><br clear="all">

Archの場合は、元から入ってたような気がしますが、調べてみないと分かりません。

Macの場合は、必要な物があるので、それをインストールして使います。

{% codeblock lang:bash %}
$ inxi -b

$ svn checkout http://inxi.googlecode.com/svn/ inxi-read-only

$ brew install gawk

$ cd inxi-read-only/trunk

$ ./inxi -b

{% endcodeblock %}

{% raw %}
    System:    Host: arch Kernel: 3.17.4-1-ARCH x86_64 (64 bit) Desktop: Awesome 3.5.5 Distro: Arch Linux
    Machine:   System: innotek product: VirtualBox v: 1.2 serial: 0
               Mobo: Oracle model: VirtualBox v: 1.2 serial: 0 Bios: innotek v: VirtualBox date: 12/01/2014
    CPU:       Single core Intel Core i7 speed: 2201 MHz (max)
    Graphics:  Card: InnoTek Systemberatung VirtualBox Graphics Adapter
               tty size: 122x33 Advanced Data: N/A for archlinux
    Drives:    HDD Total Size: 2199.0GB (0.2% used)
    Info:      Processes: 0 Uptime: 0 min Memory: 155.3/1290.1MB Client: Shell (zsh) inxi: 2.2.16
{% endraw %}

https://code.google.com/p/inxi/

