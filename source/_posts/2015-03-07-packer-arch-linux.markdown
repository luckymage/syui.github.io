---
layout: post
title: "packer-arch-linux"
date: 2015-03-07 13:57:55 +0900
comments: true
categories: os
tags: [android,arch]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Packerをインストールしてみました。<!--more--><br clear="all">

{% codeblock lang:bash %}
$ wget https://aur.archlinux.org/packages/pa/packer/packer.tar.gz

$ tar -zxvf packer.tar.gz

$ cd packer

$ su archlinux

$ makepkg

$ sudo pacman -U packer-*.pkg.tar.xz

$ packer -S jq
{% endcodeblock %}

[ARMv7h](http://archlinuxarm.org/forum/viewforum.php?f=60)

そういえば、`makepkg`で`asroot`オプションがよく分からない事になってたので、patchを当てた気がしなくもないです。Android Terminal Emulatorでの操作はきつかったので、Gistに上げておきます。


{% codeblock lang:bash packer.patch https://gist.githubusercontent.com/syui/e1a23648f9aef95bbc9b/raw/packer-asroot.patch LINK %}
{% raw %}
--- /usr/bin/packer     2014-08-11 10:43:24.000000000 +0200
+++ /usr/bin/packer.xmw 2015-01-01 23:39:05.706239397 +0100
@@ -328,7 +328,9 @@

   # Installation (makepkg and pacman)
   if [[ $UID -eq 0 ]]; then
-    makepkg $MAKEPKGOPTS --asroot -f
+    id pacman >/dev/null 2>/dev/null || useradd -r -d /var/empty pacman
+    chown -R pacman:pacman .
+    su -c "makepkg $MAKEPKGOPTS -f" pacman
   else
     makepkg $MAKEPKGOPTS -f

   fi
{% endraw %}
{% endcodeblock %}

{% codeblock lang:bash %}
$ curl -O https://gist.githubusercontent.com/syui/e1a23648f9aef95bbc9b/raw/packer-asroot.patch

$ patch -u < packer-asroot.patch
{% endcodeblock %}

