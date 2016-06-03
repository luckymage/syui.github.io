---
layout: post
title: "Mplayerで再生中のファイル名を取得する"
date: 2014-09-24
comments: true
categories: music
tags: mplayer
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">便利なオプションあったら教えて下さい。<!--more--><br clear="all">

[mplayer](http://www.mplayerhq.hu/DOCS/man/en/mplayer.1.html)

`peco`でディレクトリを選択し、それを再生します。出力は、`~/Music/info.txt`に保存します。

{% codeblock lang:bash ~/Music/script/mplayer_play.sh %}
{% raw %}
#!/bin/bash

sea="ID_FILENAME"
dir1=$HOME/Music
rm -rf $dir1/*/.DS_Store >/dev/null 2>&1

dir2="$dir1/"`zsh -c "ls -A $dir1 | peco"`
pla=`mplayer -novideo -speed 2 -af scaletempo,volnorm -loop 20 -quiet -msglevel all=0 -identify $dir2/* > $dir1/info.txt`

#cat $dir1/info.txt | grep FILE | tail -n 1 | xargs basename | cut -b 1-6

rm $dir1/info.txt
{% endraw %}
{% endcodeblock %}

再生中のファイル名を取得するのは簡単で、`cat ~/Music/info.txt | grep FILE | tail -n 1 | xargs basename`でいけます。

例えば、出力を使って、4文字ごとに流すように取得してみます。

{% codeblock lang:bash ~/Music/script/mplayer_name.sh %}
{% raw %}
#!/bin/bash

dir=$HOME/Music
cha=`cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename`
sum=`echo $cha | wc -c | tr -d ' '`

for (( i = 1; i < $sum; i=`expr $i + 4` ))
do
    a=`expr $i + 4`
    b=$i"-"$a
    cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename | cut -b $b
    sleep 0.3
done
{% endraw %}
{% endcodeblock %}

`tmux`のステータスラインとかに流れるようにしたいのだけど、面倒くさそう...。`for`はそのまま使えず、数字を保存しておいて、1個ずつ実行していくしかないです。

やってみた感じ、微妙です。

{% codeblock lang:bash ~/Music/script/mplayer_tmux.sh %}
{% raw %}
#!/bin/bash

dir=$HOME/Music
cha=`cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename`
sum=`echo $cha | wc -c | tr -d ' '`
fil=$dir/info.s

if [ -e $fil ]; then
    i=`cat $fil | tail -n 1`
    if [ $i -le $sum ]; then
        a=`expr $i + 4`
        b=$i"-"$a
        cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename | cut -b $b
        echo $a >> $fil
    else
        cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename | cut -b 1-4
        rm $fil
    fi
else
    cat $dir/info.txt | grep FILE | tail -n 1 | xargs basename | cut -b 1-4
    echo 1 > $fil
fi
{% endraw %}
{% endcodeblock %}

一応、GIF、貼っておきます。




