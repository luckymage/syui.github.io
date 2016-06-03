---
layout: post
title: "Arch LinuxのTouchPadを快適にする設定"
date: 2014-07-24
comments: true
categories: [os]
tags: [macbook, linux, arch, touchpad]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">キーボード入力中にタッチパッドが頻繁に発動すると思ったら、手のひら検出機能が動作していなかったみたいです。<!--more--><br clear="all">

タッチパッドの設定は、通常、`/etc/X11/xorg.conf.d/50-synaptics.conf`になります。`Ctrl+Alt+BackSpace`でXを再起動することにより設定が反映されます。

{% codeblock lang:bash /etc/X11/xorg.conf.d/50-synaptics.conf https://wiki.archlinux.org/index.php/Touchpad_Synaptics/10-synaptics.conf_example LINK %}
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
        # 一本指のタップをマウスボタン1に割り当てる
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
        Option "VertTwoFingerScroll" "on"
        Option "HorizTwoFingerScroll" "on"
        Option "CircularScrolling" "on"
        Option "EmulateTwoFingerMinZ" "100"
        Option "EmulateTwoFingerMinW" "50"
        Option "CoastingSpeed" "50"
        #Option "VertEdgeScroll" "on"
        #Option "HorizEdgeScroll" "on"
        #Option "CircScrollTrigger" "2"
        # 手のひら自動検出を有効にする
        # synclient PalmDetect=1
        Option "PalmDetect" "1"
        # synclient PalmMinWidth=10
        Option "PalmMinWidth" "10"
        # synclient PalmMinZ=200
        Option "PalmMinZ" "200"
EndSection
{% endcodeblock %}


分からない時は、以下のコマンドを叩きます。

{% codeblock lang:bash %}
# タッチパッドの情報を調べる
$ xinput -list

# すべてのオプションを調べる
$ man synaptics

# 現在の設定をリスト化する
$ synclient -l

# オプションを一時的に設定する
$ synclient PalmDetect=1 (手のひら検出を有効にする)
$ synclient TapButton1=1 (ボタンのイベントを設定する)
$ synclient TouchpadOff=1 (タッチパッドを無効にする)
{% endcodeblock %}

だいぶ快適になりました。

<a href="https://wiki.archlinux.org/index.php/Touchpad_Synaptics_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Touchpad Synaptics (日本語) - ArchWiki</a>


