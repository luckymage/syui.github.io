---
layout: post
title: "MacBookAirにArchLinuxをインストールした場合のハード周りの設定"
date: 2015-01-31
comments: true
categories: os
tags: arch
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">主に、ブートローダーに関する設定とハード周りに関する設定です。<!--more--><br clear="all">

##EFI

MacのEFIに関する仕組みは、かなり厄介ですが、解決は可能です。MacBookにMacを削除し、ArchLinuxをインストールすると、起動時に30秒ほど、`/System/Library/CoreServices/boot.efi`を探しますが、これは起動時間を長くしているだけなので、時間の無駄です。(正確には違うけど、これから実行するコマンドを分かりやすくするための表現です)

よって、この問題を解消します。

私は、元から使ってるブートローダー`disk0s1/efi/EFI/arch/grubx64.efi`で上書きしますが、アイコンとかもいい感じなので、場合によっては、Macのブートローダーをデフォルトにしておいても良いだろうと思います。(この場合、上書き手順は不要となります)

###installer

まず、MacのインストールUSBを作成します。`Yosemite`でも同じような感じでしょうが、バージョンは低いほうが、ブートローダー周りの問題をハックしやすいだろうと考えましたので、`Mavericks`を使用しました。(調べてないけど)

{% codeblock lang:bash %}
$ sudo /Volumes/Untitled/soft/os/Install\ OS\ X\ Mavericks.app/Contents/Resources/createinstallmedia --volume /Volumes/s/ --applicationpath /Volumes/Untitled/soft/os/Install\ OS\ X\ Mavericks.app --nointeraction
{% endcodeblock %}

###bless

それを起動し、以下のコマンドを実行します。

{% codeblock lang:bash %}
$ diskutil list
disk0s1 200M EFI vfat
disk0s2 100G / ext4

$ cd /Volumes
$ mkdir efi
$ mount -t msdos /dev/disk0s1 /Volumes/efi

$ cp -r Image \Volume/System /Volumes/efi
$ cp /Volumes/efi/EFI/arch/grubx64.efi /Volumes/efi/System/Library/CoreServices/boot.efi
$ bless --folder=/Volumes/efi --file=/Volumes/efi/System/Library/CoreServices/boot.efi --setBoot

$ reboot
{% endcodeblock %}

##nvram

起動音を削除したい場合は、再起動前に以下のコマンドを2回実行しておきましょう。

{% codeblock lang:bash %}
$ nvram SystemAudioVolume=%00
$ nvram SystemAudioVolume=%00

$ nvram -p
{% endcodeblock %}

###grub

ちなみに、私のブートローダー作成方法は、以下のような感じです。参考までに。

既にArchLinuxをインストールしている場合は、実行しないでくださいね。念のため。

{% codeblock lang:bash %}
$ mkfs.vfat /dev/sda1

$ grub-install --force --recheck /dev/sda
{% endcodeblock %}

###icns

`/`にアイコンを置くと、表示されるみたいな情報もあります。

> エントリのアイコンは対象パーティションのルートに/.VolumeIcon.icnsというMacアイコンファイルが存在すれば、それが使われます。

[http://d.hatena.ne.jp/ichelm/20141209](http://d.hatena.ne.jp/ichelm/20141209)

`.png`を変換するなら、以下のようにすると良いらしいです。

{% codeblock lang:bash %}
$ mkdir app_name.iconset

$ cd !$

$ curl -o icon_512x512.png https://cdn0.iconfinder.com/data/icons/flat-round-system/512/archlinux-512.png

$ iconutil -c icns .

$ mv ..icns /Volumes/efi/.volumeicon.icns
{% endcodeblock %}

[https://www.iconfinder.com/icons/386451/arch_linux_archlinux_icon](https://www.iconfinder.com/icons/386451/arch_linux_archlinux_icon)

自分の場合、ブラウザでダウンロードし、それをブートルートにコピーしておきました。

{% codeblock lang:bash %}
$ sudo mkdir -p /mnt/efi

$ sudo mount /dev/sda1 /mnt/efi

$ sudo cp .volumeicon.icns /mnt/efi
{% endcodeblock %}

![](http://lh3.ggpht.com/-tvNEjzNZPrI/VMwAvYQNA1I/AAAAAAAAAVU/8gKtMPv9msE/archlinux_macboot_efi.jpg)

> 写真技術が酷すぎてすいません。

##keyboard

私の場合、`F1-F12`をハード調整機能にするものと、通常のキーとして機能させるものに分けており、`awesome`の設定にて、ショートカットで切り替えられるようにしています。

{% codeblock lang:lua ~/.config/awesome/rc.lua %}
globalkeys = awful.util.table.join(
  awful.key({ modkey }, "[", function () awful.util.spawn_with_shell("xmodmap ~/.xmodmap.default") end),
  awful.key({ modkey }, "]", function () awful.util.spawn_with_shell("xmodmap ~/.xmodmap.origin") end),
)
{% endcodeblock %}

###xbacklight

例えば、輝度の調整です。

{% raw %}
    明るくする:
    $ xbacklight -inc +10
    弱くする:
    $ xbacklight -dec +10
{% endraw %}

keycodeに`XF86MonBrightnessUp`とかあるみたいです。ということで、これを設定します。

{% codeblock lang:lua ~/.config/awesome/rc.lua %}
awful.key({  }, "XF86MonBrightnessDown", function ()
  awful.util.spawn_with_shell("xbacklight -inc +10") end),
awful.key({  }, "XF86MonBrightnessUp", function ()
  awful.util.spawn_with_shell("xbacklight -dec +10") end),
{% endcodeblock %}

###xbdlight

同じく、[xbdlight](https://aur.archlinux.org/packages/kbdlight/)をインストールして、

{% codeblock lang:lua ~/.config/awesome/rc.lua %}
awful.key({  }, "XF86KbdBrightnessDown", function ()
  awful.util.spawn_with_shell("xbdlight off") end),
awful.key({  }, "XF86KbdBrightnessUp", function ()
  awful.util.spawn_with_shell("xbdlight max") end),
{% endcodeblock %}

その他も、こんな感じで使えそうなキーでもご自由に。

###xbindkeys

[xbindkeys](https://wiki.archlinux.org/index.php/Xbindkeys)は、結構使えるのです。

##network

[ArchWiki](https://wiki.archlinux.org/index.php/MacBook)では、[networkmanager](https://wiki.archlinux.org/index.php/NetworkManager)がおすすめされていますが、[netctl](https://wiki.archlinux.org/index.php/netctl)がオススメ。

`netctl-ifplugd@interface.service`は初期から起動していると思われます。ArchLinuxインストール時にリポジトリダウンロードするためにネットワーク接続がどうしても必要ですから、どうやらこれが使われているみたいです。

{% codeblock lang:bash %}
# デフォルトでインストールされている
$ sudo pacman -S netctl

$ yaourt -S netgui

$ wifi-menu
{% endcodeblock %}

ただし、メニューバーに表示させるには、`networkmanager`の`nm-applet`が必要なので、どうしようかと思っています。

[wifi](https://wiki.archlinux.org/index.php/Wireless_Setup)の設定関連の情報はこちら。

{% codeblock lang:bash %}
# 有線接続のデーモン化
$ systemctl enable netctl-ifplugd@interface.service

# 無線接続のデーモン化
$ systemctl enable netctl-auto@interface.service
{% endcodeblock %}

接続がバッティングする場合、どちらかのプロファイルを使うかは、設定によって変更できます。自分の場合、設定してなくても有線が優先する感じです。後は、wifiをoffにすることさえ簡単にできるようにしておけば、便利になります。

{% codeblock lang:bash %}
# list
$ netctl-auto list

# stop
$ netctl-auto disable-all

# start
$ netctl-auto enable-all
{% endcodeblock %}

そういえば、自動起動アプリのことを、何となくデーモンと呼ぶことがあるのですが(あくまで私の中では)、これって正しいのだろうか。特に調べてないです。

