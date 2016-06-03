---
layout: post
title: "ArchLinuxをUSBにインストールして持ち運ぶ"
date: 2015-02-01
comments: true
categories: os
tags: arch
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">前は、他のOSをカスタマイズしたUSBを使っていたのですが、ArchLinuxをカスタマイズしたやつを使うようにしました。<!--more--><br clear="all">

カスタムUSBを持ち運ぶ際は、どのマシンに挿しても起動できるように、または、キーボードその他の設定も切り替えられるようにシステムを構築していきたいですね。

ということで、まずは、ブートシステムからなわけですが、これは非常に面倒くさいのです。なぜなら、ほとんどの人は、`grub-install`の自動判断に任せて、マシンにブートローダーをインストールしているからです。これを、1つずつ`--target`を使用して、ファイルシステムを作成していくことになります。

ただし、私の場合は、既にMacBook用に作ってありましたので(`x86_64-efi`)、それをコピーし、USBにArchLinuxをインストールする際は、`--target=i386-pc`にしました。

{% codeblock lang:bash %}
$ grub-install --target=i386-pc --recheck --debug --force /dev/sdb1
{% endcodeblock %}

{% codeblock lang:bash %}
# USB2:/mnt/sdb2
$ mkdir -p  /mnt/sdb2
$ mount /dev/sdb2 /mnt/sdb2

# HDD2:/mnt/sda2
$ mkdir -p /mnt/sda2
$ mount /dev/sda2 /mnt/sda2

# x86_64-efi:HDD2 → USB2
$ cp -r /mnt/sda2/boot/grub/x86_64-efi /mnt/sdb2/boot/grub/
{% endcodeblock %}

`sdb2:USB2`は、こんな感じの構成になります。

{% raw %}
    /boot/grub/
      x86_64-efi
      i386-pc
{% endraw %}


ついでに、[前回](http://syui.github.io/blog/2015/01/31/macbookair-archlinux-bootloader/#tocAnchor-1-1)で解説したMac用の起動時間短縮設定もコピーしておきましょう。

{% codeblock lang:bash %}
# HDD1:/mnt/efi
$ mkdir -p /mnt/efi
$ mount /dev/sda1 /mnt/efi

# USB1:/mnt/efi-usb
$ mkdir -p /mnt/efi-usb
$ mount /dev/sdb1 /mnt/efi-usb

# System:HDD → USB
$ cp -r /mnt/efi/System /mnt/efi-usb 
{% endcodeblock %}

`sdb1:USB1`は、こんな感じになります。

{% raw %}
    /System/Library/CoreServices/Boot.efi
{% endraw %}

簡単に説明すると、これは、中身が`sda1`にある`efi/EFI/arch/grubx64.efi`なので、それを使ってもよいです。

{% codeblock lang:bash %}
$ mkdir -p /mnt/efi-usb/System/Library/CoreServices/

$ cp -r /mnt/efi/efi/EFI/arch/grubx64.efi /mnt/efi-usb/System/Library/CoreServices/Boot.efi
{% endcodeblock %}

説明していて思ったのですが、かなりややこしいですね。

ブートできるようになったら、マシンを使って、ArchLinuxをカスタマイズしていけばよいです。もちろん、既存のものを丸ごとコピーしてきても良いですが、その場合は、権限に注意しなければなりません。(全体コピーなら大丈夫なのかな...その辺りは分かりません)

{% codeblock lang:bash 例 %}
# すべてのユーザーに読み,書き,実行権限を与え、グループの実行権限を除き、その他のユーザーの書き,実行権限を除く(ディレクトリ再帰)
$ chmod -R a+rwx,g-x,o-wx /home/user/
{% endcodeblock %}

ここで、結果は`-rwxrw-r--`になります。

##追記

以下のスクリプトを見ていただければ大体の手順がわかります。これは、Mac用のブートシステムを`/dev/sdb1`にインストールするやり方です。実行すれば、Mac PCでLinux USBを起動できます。

{% codeblock lang:bash %}
#!/bin/bash
su
# usb-efi-boot
mkdir -p /boot/efi
mount -t vfat /dev/sdb1 /boot/efi
if [ ! -d /boot/efi/EFI ];then
    pacman -S efibootmgr
    grub-install --force --recheck --target=x86_64-efi --efi-directory=/boot/efi
    grub-mkconfig -o /boot/grub/grub.cfg
    cp /home/dotfiles/icon/arch-dark.volumeicon.icns /boot/efi/.volumeicon.icns
    mkdir -p /boot/efi/System/Library/CoreServices
    cp /boot/efi/EFI/arch/grubx64.efi /boot/efi/System/Library/CoreServices/Boot.efi
    echo 'HOOKS="base udev block autodetect modconf filesystems keyboard fsck"' >> /etc/mkinitcpio.conf
    mkinitcpio -p linux
fi
{% endcodeblock %}

