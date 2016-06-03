---
layout: post
title: "QuickTime Playerの動画キャプチャが上手く動作しない"
date: 2014-08-17
comments: true
categories: [ os ]
tags: [ mac, tty, cli, video, screen ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">どうやら、メニューバーからの操作に変わったみたいです。<!--more--><br clear="all">

##上手く行かなかった方法

{% codeblock lang:bash %}
{% raw %}
# スタート
$ osascript -e 'tell application "QuickTime Player" to start (new screen recording)'

# ストップと保存
$ osascript << EOF
  tell application "QuickTime Player"
    stop document 1
    tell document 1
    save in item 1 of ~/Movies/out.mov
    close every document saving no
    quit
    end tell
  end tell
EOF

# GIFに変換
$ ffmpeg -i *.mov -r 8 %04d.png && gm convert *.png hoge.gif && rm *.png

# VLCでキャプチャ
/Applications/VLC.app/Contents/MacOS/VLC screen:// --screen-fps=25 --quiet --sout "#transcode{vcodec=h264,vb=3072}:standard{access=file,mux=mp4,dst=$HOME/Movies/vlc.mp4}" --no-interact --pidfile $HOME/Movies/vlc.pid -d
{% endraw %}
{% endcodeblock %}

http://netjunki.org/capturing-video-with-applescript-and-quicktime.html

##上手くいった方法

###ttyrec, ttygif



####インストール

{% codeblock lang:bash %}
$ brew install ttyrec

$ git clone https://github.com/icholy/ttygif.git

$ cd ttygif

$ make
{% endcodeblock %}

####使い方

{% codeblock lang:bash %}
$ ttyrec

$ echo command.

$ exit

$ ./ttygif ttyrecord

$ gm convert *.png output.gif && rm *.png

$ qlmanage -p output.gif
{% endcodeblock %}

ちなみに、`.gif`への変換は、`./concat_osx.sh`が使えます。

