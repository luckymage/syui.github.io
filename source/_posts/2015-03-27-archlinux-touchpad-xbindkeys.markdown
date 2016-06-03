---
layout: post
title: "archlinux-touchpad-xbindkeys"
date: 2015-03-27
comments: true
categories: os
tags: [linux, archlinux, xbindkeys, touchpad, macbook]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">xvkbdよりも、xdotoolのほうが速い感じだったので、変更してみました。<!--more--><br clear="all">

X11で使うタッチパッドですが、特定の動作にキーを割り当てることも可能です。

キーを割り当てる具体的な方法は、マウスのボタンをエミュレート設定し、そこに、`xbindkeys`の割り当てを設定するという感じの方法があります。`xbindkeys`では、`b:n`がマウスのボタンになります。

ここで、例えば、`b:9`などは高機能マウスでしか存在しませんので、通常は使うことがありません。したがって、普通は余ってますので、利用価値が出てきます。

私は、これをタッチパッドにエミュレートし、エミュレートしたタッチパッドの動作に特定のキーに割り当てています。

割り当ては、ブラウザやファイラーで通常設定されている`戻る`や`進む`の`Alt+Up,Down,Left,Right`がオススメです。

{% codeblock lang:bash /etc/X11/xorg.conf.d/10-evdev.conf %}
# マウスのb:9にエミュレート
Section "InputClass"
        Identifier "Emulate Middle Butten"
        MatchIsPointer "on"
        Option "Emulate9Buttons" "on"
EndSection

# マウスのb:8にエミュレート
Section "InputClass"
        Identifier "Emulate Middle Butten"
        MatchIsPointer "on"
        Option "Emulate8Buttons" "on"
EndSection
{% endcodeblock %}

{% codeblock lang:bash /etc/X11/xorg.conf.d/50-synaptics.conf %}
Section "InputClass"
        Identifier "touchpad catchall"
        Driver "synaptics"
        MatchIsTouchpad "on"
        Option "HorizTwoFingerScroll" "on"
        Option "PalmDetect" "1"
        Option "PalmMinWidth" "10"
        Option "PalmMinZ" "200"
        Option "TapButton1" "1"
        #右クリック
        Option "TapButton2" "3"
        #Alt+Right(xbindkeys)
        Option "TapButton3" "9"
        #Alt+Left,Right(xbindkeys)
        #右上を1回タップするとマウスのb:8
        Option "RTCornerButton" "8"
        #右下
        Option "RBCornerButton" "8"
        #左上
        Option "LTCornerButton" "9"
        #左下
        Option "LBCornerButton" "9"
EndSection
{% endcodeblock %}

あとは、`xbindkeys`の設定です。このツールは、特定のキーをコマンドに置き換えます。

{% codeblock lang:bash %}
$ sudo pacman -S xbindkeys xdotool

# デフォルトの設定ファイルを作る
$ xbindkeys -d > ~/.xbindkeysrc

# キーを調べる
$ xbindkeys -k
{% endcodeblock %}

{% codeblock lang:bash ~/.xbindkeysrc %}
#xvkbd -xsendevent -text "\[Alt]\[Right]"
"xdotool key --window `xdotool getactivewindow` --clearmodifiers alt+Right"
b:8

#xvkbd -xsendevent -text "\[Alt]\[Left]"
"xdotool key --window `xdotool getactivewindow` --clearmodifiers alt+Left"
b:9
{% endcodeblock %}

ここで、`xvkbd`の代わりに`xdotool`を使います。これは、ウィンドウとキー入力を関連付け実行するツールです。高機能。

{% codeblock lang:bash %}
$ xdotool help

# chromiumにフォーカスし、C+BSを押す
$ xdotool windowfocus `xdotool search --onlyvisible --name chromium`; xdotool key ctrl+BackSpace;
{% endcodeblock %}

さて、大体の説明を終えた所で、タッチパッドの端(左下)を触ってみましょう。`Alt+Left`が押されます。これは、ブラウザでいうところの`戻る`に該当します。また、この戻るキーは、3指同時タップにも設定してあります。これで、少しはブラウジングが快適になるかもです。

ちなみに、端(角)というのは、本当に端なので、そこを触る感じで。


