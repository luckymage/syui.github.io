---
layout: post
title: "SpaceFMの使い方"
date: 2015-02-01
comments: true
categories: os
tags: [linux, filemanager, arch]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">`spacefm`の設定です。<!--more--><br clear="all">

{% githubrepo IgnorantGuru/spacefm %}

##mount

{% codeblock lang:bash %}
$ sudo pacman -S fuse-exfat exfat-utils gvfs udevil ntfs-3g
{% endcodeblock %}

`exfat`, `ntfs`などのフォーマットに対応したり、自動マウントを支援したりするためのコマンドです。

![](http://lh3.ggpht.com/-eNW9KZYivWg/VM3yNQvsAdI/AAAAAAAAAV8/Spm8Ne-U8qc/s0/2015-02-01-005125884.png)

##exfat

ただし、`spacefm`のデフォルト設定では、`exfat`が自動マウントされないので、`udevil`の設定が必要になります。

`default_options_exfat`の追加と`allowed_options`の末尾に`nonempty`を追加します。

{% codeblock lang:bash %}
default_options = nosuid, noexec, nodev, noatime
default_options_exfat = nosuid, noexec, nodev, noatime, nonempty

allowed_options = nosuid, noexec, nodev, noatime, fmask=0133, dmask=0022, uid=$UID, gid=$GID, ro, rw, sync, flush, iocharset=*, utf8, remount, nonempty
{% endcodeblock %}

https://github.com/IgnorantGuru/udevil/issues/52

##root

`spacefm`は、`root`起動すると、非常に扱いやすく、場合によっては、Windowsのファイル救出などに役立つかもしれません。もちろん、こちらのモードをデフォルトにすることもできますが、オススメはしません。

{% codeblock lang:bash %}
$ sudo spacefm
{% endcodeblock %}

![](http://lh4.ggpht.com/-l_JWvTYcxGk/VM3yNjx8IDI/AAAAAAAAAV4/4xszY9M2XKk/s0/2015-02-01-005125884.png)

##menu

`spacefm`は、メニューが豊富で分かりやすいです。様々なコマンド支援、マウント支援が行えます。これは、解説なくてもわかると思いますので、省略します。

日本語メニューを使う方法は、多分、ご存知かと思いますが、以下のファイルで設定します。

{% codeblock lang:bash /etc/locale.conf %}
LANG=ja_JP.utf8
{% endcodeblock %}

##icon,theme

テーマとかの設定は、以前説明したかと思いますが、以下のコマンドを実行します。

{% codeblock lang:bash %}
{% raw %}
$ sudo pacman -S numix-themes
$ yaourt -S numix-icon-theme-git

$ touch ~/.gtkrc-2.0
$ cat << EOF >> !$
gtk-icon-theme-name = "Numix"
gtk-theme-name = "Numix"
EOF

$ gtk-update-icon-cache -f /usr/share/icons/Numix

$ pkill spacefm
$ spacefm
{% endraw %}
{% endcodeblock %}


