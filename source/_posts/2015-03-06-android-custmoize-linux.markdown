---
layout: post
title: "Android上のArch Linuxをカスタマイズしてみた"
date: 2015-03-06
comments: true
categories: os
tags: android, linux
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">pecoとか動きますので、嬉しいのです。<!--more--><br clear="all">


![](http://lh4.ggpht.com/-vnHuR-kkkbI/VPl1OaeNxNI/AAAAAAAAAgk/SSOGuJKPfLA/Screenshot_2015-03-06-18-36-04.png)

##解説

###容量の変更

[Arch Linux on Android ](http://sourceforge.net/projects/linuxonandroid/files/ArchLinux/)のイメージは、容量が少ないので、それを拡張してみます。

> $ ./resize.sh

{% codeblock lang:bash Linux %}
#!/bin/bash
img=archlinux.img
dir=/media/
size=3G

pacman -S qtemu
qemu-img resize $img $size
sudo losetup /dev/loop0 $img 
sudo mount -t ext4 /dev/loop0 /mnt
sudo resize2fs /dev/loop0 $size
{% endcodeblock %}

{% codeblock lang:bash Mac %}
$ adb push archlinux.img /sdcard/arch
{% endcodeblock %}

{% codeblock lang:bash Android %}
$ su

$ sh /sdcard/arch/bootscript.sh
{% endcodeblock %}

ちなみに、`bootscript.sh`は、[こちら](http://sourceforge.net/projects/linuxonandroid/files/ArchLinux/bootscript-devfix.sh/download)のものを使用します。

使い方は、[こちら](http://syui.github.io/blog/2015/02/28/android-arch-linux/)の記事で紹介しています。

簡単に言うと、Arch Linuxの[イメージ](http://sourceforge.net/projects/linuxonandroid/files/ArchLinux)の好きなモノをダウンロードして、それを、Androidのストレージに置き、`bootscript.sh`を実行するという手順です。いくつかのコマンドを実行するのに、[ルート化](https://github.com/syui/arch-android/blob/master/root.sh)が必要であることと、`/sdcard/arch`にファイル名を`archlinux.img`としておく場合の[スクリプト](https://github.com/syui/arch-android/blob/master/bootscript.sh)は、以下になることを紹介しておきます。

{% codeblock lang:bash %}
curl -L https://raw.githubusercontent.com/syui/arch-android/master/bootscript.sh

curl -O https://raw.githubusercontent.com/syui/arch-android/master/bootscript.sh
{% endcodeblock %}

###pecoの起動

> $ ./peco.sh

{% codeblock lang:bash Android-ArchLinux %}
#!/bin/bash

pacman -S go
if [ -x "`which go`" ]; then
  export GOPATH=$HOME/go
  export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
fi

if [ ! -f $GOPATH/bin/peco ];then
    go get github.com/peco/peco/cmd/peco
fi
ls | peco
{% endcodeblock %}


##個人設定

個人的には、以下のスクリプトを起動するだけ。

{% codeblock lang:bash Mac %}
$ curl -O https://raw.githubusercontent.com/syui/dotfiles/master/android/init.sh

$ adb push init.sh /sdcard/arch
{% endcodeblock %}

{% codeblock lang:bash Android-ArchLinux %}
$ su

$ sh /sdcard/arch/archlinux.img

$ bash /sdcard/arch/init.sh
{% endcodeblock %}

##その他

Nexus7(2013)を買いました。すごくいいです。ルート化しました。

[CF-Auto-Root-flo-razor-nexus7.zip](http://download.chainfire.eu/347/CF-Root/CF-Auto-Root/CF-Auto-Root-flo-razor-nexus7.zip)

{% codeblock lang:bash %}
$ adb reboot-bootloader

$ chmod +x root-mac.sh 

$ ./root-mac.sh 
{% endcodeblock %}

