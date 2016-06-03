---
layout: post
title: "ManjaroLinuxでBluetoothの設定をしてみた"
date: 2014-06-30
comments: true
categories: [os]
tags: [linux, manjaro, arch, bluetooth]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ManjaroLinuxはArchLinuxの設定で通用します。<!--more--><br clear="all">

{% codeblock lang:bash %}
$ sudo pacman -S bluez bluez-utils dbus

$ sudo systemctl enable bluetooth

$ sudo systemctl start bluetooth

$ bluetoothctl
{% endcodeblock %}

あとは、`bluetooth`を設定するための CLI ツールです。スキャンした後に、 Mac アドレスを指定して接続します。

> [bluetooth]# agent KeyboardOnly

> [bluetooth]# default-agent

> [bluetooth]# power on

> [bluetooth]# scan on

> [bluetooth]# pair 00:00:00:00:00:00

> [bluetooth]# trust 00:00:00:00:00:00

> [bluetooth]# connect 00:00:00:00:00:00

> [bluetooth]# quit

自動接続の設定は以下の通りです。

{% codeblock lang:bash /etc/udev/rules.d/10-local.rules %}
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"
{% endcodeblock %}

{% codeblock lang:bash %}
$ systemctl enable bluetooth.service
{% endcodeblock %}

<a href="https://wiki.archlinux.org/index.php/Bluetooth" target="_blank">Bluetooth - ArchWiki</a>

