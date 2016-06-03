---
layout: post
title: "FctixでIMEをOFFにする方法"
date: 2015-04-18
comments: true
categories: editor
tags: vim
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Vimのノーマルモードに移行する際は、IMEをOFFにする設定です。<!--more--><br clear="all">

この辺り、MacBookとは相性が悪いのか、相当訳のわからない挙動をしています。多分、Fctixが内部で無理なことしてるせいでしょうが、キーバインド自体にまでよくわからない挙動が広がってしまい、Linuxでは、相変わらずこの辺の挙動をコントロールするのに苦戦しているみたいです。

まず、IMEをOFFにしたり、切り替えたりするキーの設定をすると、変な挙動が発生します。

これは、Fctixだけの問題かというと、iBusもなんか言われてたし、難しいんだろうなと思っています。

一応、やりたいことは実現できたものの、やはり、こういったツールを使っているので、どうしても無理が出てきます。

https://github.com/syui/fctix-off.vim

具体的には、`C-j`を押した時に、ノーマルモードへの移行と、IMEをOFFにしたいのですが、なかなかよくわからないことになっています。

実現できた方法は、`xbindkeys`でvimにwindowがフォーカスしてる時だけ、`C-j`の挙動を変更し、特定のキーを押したり、windowフォーカスを一度移し替えたりなど、あまりよくない方法を使用することになりました。

{% codeblock lang:bash ~/.xbindkeysrc %}
"~/.vim/bundle/fctix-off.vim/fctix-off.sh"
    Control + j
{% endcodeblock %}

{% codeblock lang:bash ~/.vim/bundle/fctix-off.vim/fctix-off.sh %}
{% raw %}
#!/bin/bash

if ! xdotool getwindowname `xdotool getactivewindow` | grep vim > /dev/null 2>&1 ;then
    xvkbd -xsendevent -text "\[Control]\j"
else
    xvkbd -xsendevent -text "\[Escape]"
    xdotool windowfocus `xdotool getactivewindow`
    xdotool key ctrl+j
    fcitx-remote -c
fi
{% endraw %}
{% endcodeblock %}

https://github.com/syui/fctix-off.vim

あとは、コード見てください。(早く新しいサイトをデザインしないとなのですが、さすがに、仮想Macで書くのは辛すぎる...)

ついでに、Chromiumでアドレスバー(Omnibox)にて、初回起動時のみIMEがONにならない問題を同じような方法で解決してみました。

{% codeblock lang:bash ~/.xbindkeysrc %}
"~/.config/chromium/arch-chromium-xbindkeys-emacs/bindkeys/chromium_hangul.sh"
  Hangul
{% endcodeblock %}

ちなみに、キーバイドは、`xev`, `xbindkeys -k`などで調べてください。

{% codeblock lang:bash ~/.config/chromium/arch-chromium-xbindkeys-emacs/bindkeys/chromium_hangul.sh %}
{% raw %}
#!/bin/bash

if xdotool getwindowname `xdotool getactivewindow` | grep Chromium > /dev/null 2>&1 ;then
        xdotool windowfocus `xdotool search --onlyvisible --name lilyterm | head -n 1`
        xdotool windowfocus `xdotool search --onlyvisible --name chromium | head -n 1`
        #fcitx-remote -o
        #fcitx-remote -c
        xvkbd -xsendevent -text "\[Hangul]"
else

        xvkbd -xsendevent -text "\[Hangul]"
fi

# http://www.semicomplete.com/projects/xdotool/xdotool.xhtml
# https://developer.chrome.com/extensions/api_index
# https://developer.chrome.com/extensions/omnibox
# https://developer.chrome.com/extensions/commands
{% endraw %}
{% endcodeblock %}

こちらも、あとはコードを見てください。

https://github.com/syui/arch-chromium-xbindkeys-emacs


