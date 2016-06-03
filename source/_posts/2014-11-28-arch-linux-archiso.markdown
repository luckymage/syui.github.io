---
layout: post
title: "Arch Linux GUI"
date: 2014-11-28
comments: true
categories: os
tags: arch
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Arch LinuxのGUI環境設定<!--more--><br clear="all">

##Arch Linuxのインストール

<img src="http://lh6.ggpht.com/-JZpEgvb_HaQ/VHr0oM1b6HI/AAAAAAAAAHw/hgoDXRb5NNM/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png">

Archのインストールは、非常に簡単に終わります。起動に必要なものは、実際、いくつかのパッケージ群と、ブートローダーの設定くらいです。以下、最小限のインストール手順を紹介します。

はじめに、ディスクパーティションの作成、パッケージのディスクへのインストールなどを行います。

次に、パッケージをルートフォルダにインストールします。

最後に、ブートローダー`GRUB`を設定します。

方針としてスワップは設定しませんし、ブートディスクなども分けません。

まず、4G以上あるパソコンは、基本、スワップは不要であり、稀に遅くなる状況が存在するからです。また、`home`や`boot`、`root`なども分けたい人は分けてください。変更、追加されるコマンドは、`mkswap`、`mount`、`pacstrap`くらいです。

###コマンド

{% codeblock lang:bash %}
{% raw %}
$ loadkeys jp106
# キーボードをJISに変更

$ cfdisk /dev/sda
sda1 / 256GB
sda2 空 残り全部
# ディスクパーティションを設定

$ mkfs.ext4 /dev/sda1
# ディスクをフォーマット

$ mount /dev/sda1 /mnt
# 先ほどフォーマットしたディスクで、ルートに設定したものをマウント

$ pacstrap /mnt base base-devel
# 基本コマンドなどをインストール。場合によっては、 /etc/pacman.d/mirrorlist を編集

$ genfstab -U -p /mnt >> /mnt/etc/fstab
# ディスク情報を追加

$ arch-chroot /mnt
# 指定したディレクトリをルートとしてみなします

$ pacman -S grub
# ブートローダーであるGRUBをインストール

$ grub-install --force --recheck /dev/sda
# ブートローダーをインストールするディスクを指定し、 /boot/grub にブートローダーをインストール

$ grub-mkconfig -o /boot/grub/grub.cfg
# /etc/defaults/grub からブートローダーの設定である /boot/grub/grub.cfg を作成

$ pacman -S wireless_tools wpa_supplicant wpa_actiond dialog ifplugd
$ systemctl enable netctl-auto@wlp2s0
$ systemctl enable dhcpcd.service
# インターネットの設定をしておかないと、起動した時にパッケージなどのダウンロードが出来ないので困る

$ exit
# arch-chroot を終了

$ umount -R /mnt
# /mnt をアンマウント

$ reboot
# 再起動
{% endraw %}
{% endcodeblock %}

これで終わりです。

###ヒント

- 起動画面の`Boot existing OS`を選択するとHDDが起動します。

<img src="http://lh3.ggpht.com/-V9gzaGw2kFI/VHr0oheCW1I/AAAAAAAAAH4/p6X-PX9UPKA/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png">

`Arch Linux`が起動しなくなった時などは、CD/DVD/USBなどのライブディスクを挿入し、そこから修正していきます。具体的には以下のコマンドを実行します。この手順は、重要なので覚えておきましょう。通常は、`Boot existing OS`の項目を選択すると、先ほど作成したディスク、つまり、HDD/SSDが起動することになります。

起動しない時は、一番上の項目を選択して、以下のコマンドを実行し、修正します。

{% codeblock lang:bash %}
$ mount /dev/sda1 /mnt

$ arch-chroot /mnt

# あとは、設定ファイルを直したり、ログを見たりします。
# 再起動は、 "exit && umount /mnt && reboot" でも良いし、 "reboot" だけでも良いです。終了は "poweroff" です

$ reboot
{% endcodeblock %}

したがって、慣れないうちは、DVDなどを挿入しっぱなしでも良いかもしれません。起動時に、`Boot existing OS`を選択すればよいだけです。

- `cfdisk`は、`wirte`を選択し、`yes`を入力すると、一括保存できます。終了は、`quit`です。また、`type`を選択すると、色々便利です。

- `root`か`home`に設定した場所を`/mnt`にマウントします。

- パッケージのダウンロードが出来ない場合や遅い場合は、`/etc/pacman.d/mirrorlist`を編集して、対象のURLを上に持ってきます。

##カスタマイズ

カスタマイズでは、ユーザーの作成、設定を行っていきます。

###インターネット接続

実は、この設定はインストール時に行っておくのがベストです。そのままではインターネットに接続できず、設定を変更したいのなら、再度、CD/DVDを使ってArchを起動し、そこから設定しなければならないからです。ちなみに、Archインストール時に実行した場合は、この手順は不要です。

{% codeblock lang:bash %}
{% raw %}
$ pacman -S wireless_tools wpa_supplicant wpa_actiond dialog ifplugd

$ systemctl enable netctl-auto@wlp2s0

$ systemctl enable dhcpcd.service
{% endraw %}
{% endcodeblock %}

ちなみに、もし、接続設定を忘れてしまった場合は、DVDから起動し、以下のコマンドを叩くしかないです。

{% codeblock lang:bash %}
$ mount /dev/sda1 /mnt

$ arch-chroot /mnt

$ pacman -S wireless_tools wpa_supplicant wpa_actiond dialog ifplugd

$ reboot
{% endcodeblock %}

ここで使った`systemctl`コマンドは、サービスの追加などによく使いますので覚えておきましょう。また、Archでは、スクリプトの自動実行はこのコマンドが推奨されています。例えば、`uim`を起動時に実行したいとして、以下のように使います。ちなみに、`uim`は日本語入力のアプリで、下記にて紹介している`ibus`などと同類のものです。したがって、実際、この手順は不要です。

{% codeblock lang:bash ~/.config/systemd/user/uim-env.service %}
[Unit]
Description=uim environment initialization
Before=xorg.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl --user set-environment XMODIFIERS=@im=uim
ExecStart=/usr/bin/systemctl --user set-environment GTK_IM_MODULE=uim
ExecStart=/usr/bin/systemctl --user set-environment QT_IM_MODULE=uim
{% endcodeblock %}

{% codeblock lang:bash ~/.config/systemd/user/uim.service %}
[Unit]
Description=uim daemon
Wants=uim-env.service
After=xorg.target

[Service]
ExecStart=/usr/bin/uim-xim
Restart=on-abort

[Install]
WantedBy=xorg.target
{% endcodeblock %}

{% codeblock lang:bash ~/.config/systemd/user/uim-toolbar.service %}
[Unit]
Description=uim toolbar
PartOf=uim.service

[Service]
ExecStart=/usr/bin/uim-toolbar-of-your-choice
Restart=on-abort

[Install]
WantedBy=uim.service
{% endcodeblock %}

以下のコマンドでサービスが有効になります。

```
$ systemctl --user enable uim.service uim-toolbar.service
```

###ユーザー設定

{% codeblock lang:bash %}
{% raw %}
# login : root
# passwd : root

$ pacman -Sy sudo

$ echo xxxx > /etc/hostname
# ホスト名を決める。user@hostnameとなり、私の場合はパソコン名称、OSなどにすることが多い

$ useradd -m -G wheel -s /bin/bash xxxx
# userをwheelグループで作成する。wheelグループは、rootの次くらいに管理ユーザー的なグループ

$ passwd
# rootのパスワードを設定

$ passwd xxxx
# userのパスワードを設定

$ su - xxxx
# userに切り替える
{% endraw %}
{% endcodeblock %}

####locale etc...

コメントアウトを外します。

{% codeblock lang:bash ~/etc/locale.gen %}
en_US.UTF-8 UTF-8
ja_JP.UTF-8 UTF-8
{% endcodeblock %}

{% codeblock lang:bash %}
$ ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
# タイムゾーン

$ hwclock --systohc --utc
# ハードウェアクロック、時計

$ visudo
# ユーザー権限の設定
{% endcodeblock %}

コメントアウトを外します。

{% codeblock lang:bash %}
Defaults env_keep += "HOME"
%wheel ALL=(ALL) ALL
{% endcodeblock %}


###GUI設定

####x

デスクトップです。

{% codeblock lang:bash %}
{% raw %}
$ pacman -S xorg-server xorg-server-utils xorg-xinit xorg-xclock xterm

$ lspci | grep VGA

$ pacman -S xf86-video-intel
# できない場合は、全部入りとして pacman -S xorg xorg-xinit xorg-input-drivers xorg-video-drivers を実行

$ startx
{% endraw %}
{% endcodeblock %}

`VirtualBox`の場合は、以下のコマンドを実行するとよいでしょう。

{% codeblock lang:bash %}
{% raw %}
$ pacman -S virtualbox-guest-utils virtualbox-host-modules virtualbox-host-dkms

$ modprobe -a vboxguest vboxsf vboxvideo

$ echo -e "vboxguest\nvboxsf\nvboxvideo\nvboxdrv\nvboxnetadp\nvboxnetflt" > /etc/modules-load.d/virtualbox.conf

$ echo  'VBoxClient-all &' > ~/.xinitrc
# 自動起動の設定
{% endraw %}
{% endcodeblock %}

非常に重要な`X`の設定は、`/etc/X11/`以下にあり、サービスやスタート的の設定が`xinit`、ハード的なものが`xorg.conf.d`になります。重要なので覚えておきましょう。

例えば、私は、キーボード、タッチパッドのオリジナル設定を`/etc/X11/xorg.conf.d/`以下に書いています。


####slim

ログインマネージャーです。

{% codeblock lang:bash %}
$ pacman -S slim arhlinux-themes-slim slim-themes

$ vi /etc/slim.conf
{% endcodeblock %}

以下の箇所をコメントアウトや編集します。

{% codeblock lang:bash /etc/slim.conf %}
# 初回実行するコマンド
login_cmd exec /bin/zsh -l ~/.xinitrc %session

# 起動時にログインするユーザー
default_user hoge

# オートログイン有効
auto_login yes

# デーモン有効
daemon yes
{% endcodeblock %}


####awesome

ウィンドウマネージャーです。

<img src="http://lh6.ggpht.com/-hjWlV7sx8uI/VHr0nNc_x0I/AAAAAAAAAH0/jQgPhrTx8fE/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png">

{% codeblock lang:bash %}
$ pacman -S awesome

$ mkdir -p ~/.config/awesome
# Linux の設定ファイルは、 ~/.config 以下が推奨されています

$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/

$ pacman -S xcompmgr
# ウィンドウ透過のために必要

$ touch ~/.xinitrc
$ echo "xcompmgr -n &" >> .xinitrc
# ウィンドウ透過

$ echo "exec awesome" >> .xinitrc
# awesomeの自動起動

$ grep -n wallp /usr/share/awesome/themes/default/theme.lua
# 壁紙の設定、この箇所を編集します
{% endcodeblock %}

ちなみに、Linuxでも他のOSでもそうですが、設定ファイルのテンプレート等を欲しい時は、`/usr/share`などのフォルダを漁ると大体見つかるのでオススメです



####spacefm

ファイルマネージャーです。

{% codeblock lang:bash %}
$ pacman -S spacefm
{% endcodeblock %}

###端末設定

ターミナルで使うものなどをインストールしていきます。

{% codeblock lang:bash %}
$ pacman -S mlterm lilyterm terminator
# お勧めのターミナルです。私は lilyterm を使ってます

$ pacman -S zsh vim tmux w3m git curl wget openssl openssh
{% endcodeblock %}

###パッケージマネージャー

####yaourt

専用のリポジトリを追加します。

{% codeblock lang:bash /etc/pacman.conf %}
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch
{% endcodeblock %}

リポジトリを追加した後、次を実行してください:

{% codeblock lang:bash %}
$ pacman -Sy yaourt
# S --sync, y --refresh, -u --upgrades
{% endcodeblock %}

###日本語設定

####ibus-mozc

日本語入力環境を整えます。

`mozc`をインストールするために専用のリポジトリを追加します。

{% codeblock lang:bash /etc/pacman.conf %}
[pnsft-pur]
SigLevel = Optional TrustAll
Server = http://downloads.sourceforge.net/project/pnsft-aur/pur/$arch
{% endcodeblock %}

リポジトリを追加した後、次を実行してください:

{% codeblock lang:bash %}
$ pacman -Sy ibus ibus-mozc

$ ibus-setup

$ /usr/lib/mozc/mozc_tool --mode=config_dialog
# 注意点としては、 mozc は root では開けません
{% endcodeblock %}

端末から`mozc`の設定を開くには`/usr/lib/mozc/mozc_tool module=config_dialog`を実行します。

自動起動するには、以下の設定を行います。

{% codeblock lang:bash ~/.xinitrc %}
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus-daemon -drx
{% endcodeblock %}

また、現在は、`fctix`というものが人気みたいです。

####fctix-anthy

{% codeblock lang:bash %}
$ pacman -S fcitx fcitx-anthy
{% endcodeblock %}

{% codeblock lang:bash ~/.xinitrc %}
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
fcitx
{% endcodeblock %}

<img src="http://lh4.ggpht.com/-IBEqoluX8B8/VHr0lZIMYdI/AAAAAAAAAHo/xEnwjtIuk-A/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png">

`Anthy`の設定では、オリジナルを作るよりも、`MS IME`など適当なキーバインドを選びましょう。

####system-font

embeddedのビットマップフォントの無効化と、ヒンティングを無効化します。

{% codeblock lang:html ~/.config/fontconfig/font.conf %}
{% raw %}
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit mode="assign" name="embeddedbitmap">
      <bool>false</bool>
    </edit>
    <edit mode="assign" name="hintstyle">
       <const>hintnone</const>
    </edit>
  </match>
</fontconfig>
{% endraw %}
{% endcodeblock %}

####ttf-font

{% codeblock lang:bash %}
$ yaourt -S ttf-migmix
{% endcodeblock %}

高度な設定を`/etc/vconsole.conf`ですることができ、起動時に`systemd`によって読み込まれます。

{% codeblock lang:bash /etc/vconsole.conf %}
FONT=lat2-16
FONT_MAP=8859-2
{% endcodeblock %}

{% codeblock lang:bash /etc/locale.conf %}
LANG=ja_JP.UTF-8
{% endcodeblock %}

###ブートローダー設定

ダサい起動画面は、変更するのが良いでしょう。

####grub


まず、テーマをダウロードしてきます。たくさん公開されてますので、検索とかすれば良いのが見つかるでしょう。

<img src="http://lh5.ggpht.com/-kWDAFrUDxBs/VHr0kmz4DWI/AAAAAAAAAHk/VoNQ3THVAu4/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png">

https://github.com/Generator/Grub2-themes

{% codeblock lang:bash %}
$ cd ~/Downloads

$ git clone git://github.com/Generator/Grub2-themes.git

$ cp -r ~/Downloads/Grub2-themes/{Archlinux,Archxion} /boot/grub/themes/
{% endcodeblock %}

そして、設定ファイルを編集します。

{% codeblock lang:bash /etc/default/grub %}
GRUB_THEME="/boot/grub/themes/Archlinux/theme.txt"
GRUB_GFXMODE=1024x768
{% endcodeblock %}

次に、設定ファイルを変換します。

{% codeblock lang:bash %}
$ grub-mkconfig -o /boot/grub/grub.cfg
{% endcodeblock %}

GRUBの設定は、元の設定ファイルである`/boot/grub/grub.cfg`を編集する方法と、簡易化された`/etc/default/grub`を編集して、`grub-mkconfig -o /boot/grub/grub.cfg`または、 `update-grub`コマンドで変換する方法があります。ここでは、後者の方法を採用しています。

私の場合は、ついでの設定として、以下を変更しました。

{% codeblock lang:bash /boot/grub/grub.cfg %}
default=0
timeout=10
splashimage=(hd0,0)/grub/splash.xpm.gz

# GRUB メニューインターフェイスを表示しないようにし、timeout 期間の経過後に default エントリをロードします。[Esc] キーを押すと、標準の GRUB メニューを表示できます
hiddenmenu
title Red Hat Enterprise Linux AS (2.6.8-1.523)
        # Linux カーネルのデバッグ出力など
        linux $grub_boot/vmlinuz-linux root=/dev/disk/by-uuid/$the_root_uuid ro quiet

# section to load Windows
title Windows
        rootnoverify (hd0,0)
        chainloader +1
{% endcodeblock %}

注目すべきは、`linux`の最後のオプションです。

| オプション | 内容 |
| --- | --- |
| ro | root 読み取りマウント
| rw | root 読み書きマウント
| quiet | デバッグ出力削減
| rhgb | グラフィカル表示
| splash/nosplash | スプラッシュ表示

<a href="https://docs.oracle.com/cd/E39368_01/e48214/ch04s02.html" target="_blank">4.2 GRUBブート・ローダーについて</a>

<a href="http://www2.it-shikaku.jp/top30.php?hidari=101-02-02.php" target="_blank">GRUB LPIC対策</a>


