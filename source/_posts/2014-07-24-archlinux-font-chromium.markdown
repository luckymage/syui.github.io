---
layout: post
title: "Arch LinuxのChromiumが文字化けする"
date: 2014-07-24
comments: true
categories: [os, browser]
tags: [linux, arch, chrome, font]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Arch LinuxのChromiumが文字化けしたので、それを直しました。<!--more--><br clear="all">

この前、`Firefox`から`Chromium`に移行したので。

###システム全体にフォントを設定する

{% codeblock lang:bash %}
{% raw %}
$ sudo yaourt -S otf-ipaexfont

$ sudo cat << EOF > /etc/fonts/conf.avail/71-no-embedded-bitmaps.conf
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
EOF

$ sudo ln -s /etc/fonts/conf.avail/71-no-embedded-bitmaps.conf /etc/fonts/conf.d/71-no-embedded-bitmaps.conf

$ fc-cache -vf
{% endraw %}
{% endcodeblock %}

Arch Linuxで文字を綺麗に表示する検証をされている方のブログが非常に参考になりました。

###従来のフォント設定

ちなみに、従来のやり方では、以下のように`$HOME`に`.fonts.conf`を作ればよいみたいです。

{% codeblock lang:bash %}
$ sudo yaourt -S ttf-migmix

$ fc-list

$ fc-list :lang=ja

$ cat << EOF > ~/.fonts.conf
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <alias>
    <family>serif</family>
    <prefer>
       <family>DejaVu Sans</family>
       <family>MigMix 1P</family>
    </prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>DejaVu Serif</family>
       <family>MigMix 1P</family>
    </prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer>
      <family>Nimbus Mono L</family>
    </prefer>
  </alias>
</fontconfig>
EOF
{% endcodeblock %}

###参考

- <a href="https://wiki.archlinux.org/index.php/Font_Configuration_(%E6%97%A5%E6%9C%AC%E8%AA%9E)#Fontconfig_.E8.A8.AD.E5.AE.9A" target="_blank">Font Configuration (日本語) - ArchWiki</a>

- <a href="http://archlinux-blogger.blogspot.jp/2013/08/arch-linux.html" target="_blank">普段使いのArch Linux: Arch Linuxで日本語フォントを設定 | 日本語フォントのインストール・見やすく表示する設定</a>

- <a href="http://spxi.ie-t.net/archlinux/lang.html" target="_blank">日本語環境構築とフォント設定 [Arch Linux] | SPxI</a>

しかし、Arch系のOSは、レベル高いブログが多くて、問題が一瞬で解決する場合が多く、良いですね。

