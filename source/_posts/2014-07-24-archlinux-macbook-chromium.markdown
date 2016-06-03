---
layout: post
title: "XorgでTouchPadの戻る、進むを設定する方法"
date: 2014-07-24
comments: true
categories: [os]
tags: [linux, x, arch]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">MacBookのタッチパッドには、戻る、進むが簡単に行えるのですが、Synapticsではある程度の工夫が必要でした。<!--more--><br clear="all">

前提として、ブラウザの設定を変更することで、対応できる場合があります。下記は、`Firefox`の場合ですね。

> mousewheel.default.action.override_x = 2

しかし、他のブラウザはそうは行きませんので、無理やり対応させてみます。具体的には、マウスボタンにキーを割り当て、それをタッチパッドの特定の動作に設定します。

{% codeblock lang:bash %}
$ sudo pacman -S xvkbd xbindkeys

$ vim ~/.xbindkeysrc
{% endcodeblock %}

{% codeblock lang:bash ~/.xbindkeysrc https://wiki.ubuntulinux.jp/UbuntuTips/Hardware/ExtensionOfMouseButtonWithXbindkeysAndXvkbd LINK %}
#"/usr/bin/xvkbd -text "\[設定したいキー]\[設定したいキー2]""
#  b:(設定したいマウスボタンの番号)

"/usr/bin/xvkbd -text "\[Alt_L]\[Up]""
  b:8

"/usr/bin/xvkbd -text "\[Alt_L]\[Down]""
  b:9
{% endcodeblock %}

ちなみに、`xbindkeys`はデーモンで起動しておくと、設定が永続化されます。

その後は、先ほど設定したマウスボタンをエミュレートします。ちなみに、これは本当に必要かどうかよく分かっていません。

{% codeblock lang:bash /etc/X11/xorg.conf.d/10-evdev.conf %}
Section "InputClass"
        Identifier "Emulate Middle Butten"
        MatchIsPointer "on"
        Option "Emulate3Buttons" "on"
EndSection

Section "InputClass"
        Identifier "Emulate Middle Butten"
        MatchIsPointer "on"
        Option "Emulate8Buttons" "on"
EndSection

Section "InputClass"
        Identifier "Emulate Middle Butten"
        MatchIsPointer "on"
        Option "Emulate9Buttons" "on"
EndSection
{% endcodeblock %}

最後に、エミュレートしたボタンをタッチパッドの動作に指定します。

{% codeblock lang:bash /etc/X11/xorg.conf.d/50-synaptics.conf https://wiki.archlinux.org/index.php/Touchpad_Synaptics/10-synaptics.conf_example LINK %}
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton2" "3"
        Option "TapButton3" "8"
        Option "RTCornerButton" "8"
        Option "RBCornerButton" "8"
        Option "LTCornerButton" "9"
        Option "LBCornerButton" "9"
EndSection
{% endcodeblock %}

なぜか、`CornerButton`が効かないみたいです。

それでも、3本指でタップすると、`Alt+Up`が押されて戻れます。

参考:

- <a href="https://stuffivelearned.org/doku.php?id=os:linux:general:synapticstouchtricks" target="_blank">Synaptics Touchpad Tricks</a>

- <a href="https://wiki.ubuntulinux.jp/UbuntuTips/Hardware/ExtensionOfMouseButtonWithXbindkeysAndXvkbd" target="_blank">UbuntuTips/Hardware/ExtensionOfMouseButtonWithXbindkeysAndXvkbd - Ubuntu Japanese Wiki</a>

