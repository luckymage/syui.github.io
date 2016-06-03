---
layout: post
title: "Apacheのログを抜き出す"
date: 2014-09-08
comments: true
categories: [ shell, os ]
tags: [ zsh, mac ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ちょっとしたスクリプト。<!--more--><br clear="all">

##apache_cut2.sh

###コード

<script src="https://gist.github.com/syui/cd6fd9765bf89644843d.js"></script>

###解説

####スペースを改行に変換し、キーワードの行番号を取得します

{% codeblock lang:bash %}
$ cat $1 | tr ' ' '\n' | nl -n ln | grep $2 | awk 'NR==1' | cut -d ' ' -f 1
{% endcodeblock %}

####cutで該当箇所を抜き出します

{% codeblock lang:bash %}
$ cat $1 | cut -d ' ' -f $key1-$key2
{% endcodeblock %}

####ワンライナー

{% codeblock lang:bash %}
$ for i in `cat $1 | tr ' ' '\n' | nl -n ln | grep $2 | cut -d ' ' -f 1`;do cat $1 | cut -d ' ' -f $i- ;done
{% endcodeblock %}

###使い方

{% codeblock lang:bash%}
{% raw %}
# こんな感じのログファイルがあったとして、
$ cat hoge.log
>
> 192.168.0.1 - - [17/Apr/2014:11:22:33 +0900] "GET /index.html HTTP/1.1" 200 43206 "https://www.google.co.jp/" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36" "https://www.google.co.jp/" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36"

# キーワードから最後まで抜き出す
$ ./apache_cut2.sh hoge.log Moz
>
> "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36" "https://www.google.co.jp/" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36"
"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36"

# キーワードからキーワードまで抜き出す
$ ./apache_cut2.sh hoge.log Moz Chr
>
> "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116
{% endraw %}
{% endcodeblock %}


