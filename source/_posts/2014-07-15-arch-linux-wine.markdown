---
layout: post
title: "LinuxでWineを使ってみる"
date: 2014-07-15
comments: true
categories: [os]
tags: [linux, arch, game]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">初めてパソコンでゲームをしてみたよ。<!--more--><br clear="all">

##パソコンゲーム

私にとってゲームというのは、PSPであり、PSPでしかありませんでした。

しかし、今回は、はじめてパソコンゲームというのをやってみました。

パソコンゲームをやるなんてこれが初めてで違和感だらけですが、`Wine`を使えば起動します。

通常、パソコンゲームは、 Windows でしか動作しない物が多く、そのため、 Linux で Windoes アプリを動作させる`Wine`が必要になります。

ただ、寝転がってプレイできないというのは、不便なものですね...。

##wine

{% codeblock lang:bash %}
$ pacman -S wine winetricks

$ wine /media/path/to/hoge.exe
{% endcodeblock %}

ディスクは、ISO化して、マウントしましょう。(MacBookAirには、ドライブがないので

しかし、このままでは文字化けしてしまいます。私の場合は、フォントを仮想 C ドライブにコピーすることで、解決しました。

{% codeblock lang:bash %}
$ sudo cp /usr/share/fonts/TTF/*.ttf ~/.wine/drive_c/windows/Fonts
{% endcodeblock %}

`winetricks`でもインストールできるようですね。ついでに、ゲームの動作に必要になるパッケージもインストールしておきましょう。

{% codeblock lang:bash %}
$ winetricks allfonts
{% endcodeblock %}

パソコンでゲームなんて、なんか大人な感じです。

しかし、Vita、もっと便利にならないかな。PSPよりも不便になったところが多すぎて、結構残念感があります。

<a href="https://wiki.archlinux.org/index.php/Wine_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Wine (日本語) - ArchWiki</a>

<a href="http://www.kkaneko.com/rinkou/linux/wine.html" target="_blank">Linux で Wine のインストールと種々の設定</a>


