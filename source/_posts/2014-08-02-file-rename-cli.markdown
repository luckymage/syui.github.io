---
layout: post
title: "Apple Script/Shell Script"
date: 2014-08-02
comments: true
categories: [ browser, os ]
tags: [ mac, cli, shell, apple, chrome, tips ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Apple ScriptとShell Scriptで使ったものをまとめていきます。<!--more--><br clear="all">


##Apple Script

###Chromeで開いているタブのタイトルとURLを取得する

{% codeblock lang:bash %}
{% raw %}
osascript << EOF
tell application "Google Chrome"
    set pageURI to get URL of tab of window 1
    set pageTitle to get title of tab of window 1
    return pageTitle & space & pageURI
end tell
EOF
{% endraw %}
{% endcodeblock %}

###Chromeの読み込み完了を待つ

{% codeblock lang:bash %}
{% raw %}
osascript << EOF
tell application "Google Chrome"
   repeat while loading of active tab of window 1
        delay 0.1
   end repeat
   activate
end tell
EOF
{% endraw %}
{% endcodeblock %}

##Shell Script

###zsh scriptのファイルパス

{% codeblock lang:bash %}
#!/bin/zsh

# スクリプトに記述した場合、現在、スクリプトがあるディレクトリパスを取得する
dir=${0:a:h}
echo $dir

# 現在のディレクトリの一つ上のパスを取得する(上の記述とセットで動作する)
ho1=${dir:h}
echo $ho1

# dir に依存しない形で取得する場合
ho2=${0:a:h:h}
echo $ho2

# スクリプトのファイル名を取得する
fil=${0:a:t}
echo $fil
{% endcodeblock %}


###Chromeでタブのタイトルを取得する

{% codeblock lang:bash %}
$ osascript -e 'tell application "Google Chrome" to get title of tab of window 1'
{% endcodeblock %}

###Chromeで最初のタブを閉じる

{% codeblock lang:bash %}
$ osascript -e 'tell application "Google Chrome" to close first tab of window 1'
{% endcodeblock %}

###iTermにフォーカスを戻す

{% codeblock lang:bash %}
$ osascript -e 'tell application "iTerm" to activate'
{% endcodeblock %}

###区切りを改行に変換する

{% codeblock lang:bash %}
$ echo "hoge, huga" | tr ',' "\n"
{% endcodeblock %}

###ファイルの拡張子を操作する

ポイントは、`ext=${fil##*.}`と`sed -e "s/\.[^.]*$//"`です。

{% codeblock lang:bash %}
# ファイルの拡張子を除く
$ for i in `ls -A`; do echo $i | sed "s/\.[^.]*$//" ;done

# ファイルの拡張子だけ取り出す
$ for i in `ls -A`; do ext=${i##*.}; echo $ext; done
{% endcodeblock %}

ちなみに、ファイルのリネームは以下の様なスクリプトでできます。以下、個人スクリプトの一部を抜粋。

{% codeblock lang:bash %}
{% raw %}
#!/bin/zsh

# file_rename
word1="hoge"
word2="huga"
tit=`ls -A . | sed -e "s/$word1//g" -e "s/$word2//g" -e 's/mylist//g' -e 's/URL.txt//g' -e '/^$/d' -e 's/^/http:\/\/www.hoge.com\//g' -e "s/\.[^.]*$//"`
fil=`ls -A .`
num=`echo $fil | wc -l | tr -d ' '`
for (( i = $num; i > 0; i-- )) do
    inp=`echo $fil | awk "NR==$i"`
    ext=${fil##*.}
    out=`echo $tit | awk "NR==$i"`
    out=`curl -s $out | grep '<title>' | sed -e 's/<title>//g' -e 's/<\/title>//g'`
    out="$out.$ext"
    mv "$inp" "$out"
done
{% endraw %}
{% endcodeblock %}

参考

http://hole.sugutsukaeru.jp/archives/593

###指定した行を抜き出す

{% codeblock lang:bash %}
$ echo "hoge\nhuga" | awk "NR==2"
{% endcodeblock %}

###ページタイトルを取得する

{% codeblock lang:bash %}
{% raw %}
$ curl -s syui.github.io | grep '<title>' | sed -e 's/<title>//g' -e 's/<\/title>//g'
{% endraw %}
{% endcodeblock %}


