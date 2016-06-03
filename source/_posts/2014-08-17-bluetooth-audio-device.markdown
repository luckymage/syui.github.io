---
layout: post
title: "オーディオデバイスの入出力をコマンドラインから設定する"
date: 2014-08-17
comments: true
categories: [ os , shell ]
tags: [ mac, audio , peco , golang ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">自分が持っているデバイスは、残念ながら回避不能な問題があるのですが、一応、紹介します。<!--more--><br clear="all">

[switchaudio-osx](https://github.com/deweller/switchaudio-osx) -github

[switchaudio-osx](https://code.google.com/p/switchaudio-osx/downloads/list) -download

`au`コマンドで出力を変更します。`-i`で入力です。デバイスの選択は、`peco`を使います。

{% codeblock lang:bash ~/.zshrc %}
{% raw %}
function au(){
case $1 in
    -o|*)
        SwitchAudioSource -a | grep output | cut -d '(' -f 1 | sed -e 's/ *$//' -e 's/$/"/g' -e 's/^/"/g' | peco | xargs -J % SwitchAudioSource -s %
    ;;
    -i)
        SwitchAudioSource -a | grep input | cut -d '(' -f 1 | sed -e 's/ *$//' -e 's/$/"/g' -e 's/^/"/g' | peco | xargs -J % SwitchAudioSource -t input -s %
    ;;
esac
}
zle -N au
bindkey '\^^' au
{% endraw %}
{% endcodeblock %}

関係ありませんが、私が使っているBluetoothイヤホン、2度電源を入れないと、なぜか使えるようにならないんですよね...。

