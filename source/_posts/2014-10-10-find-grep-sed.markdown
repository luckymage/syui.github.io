---
layout: post
title: "文字列を検索し、一括削除する方法"
date: 2014-10-10
comments: true
categories: [ programming, shell ]
tags: zsh
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">find, grep, sedを使いました。<!--more--><br clear="all">

画像リンクが切れたので、ブログから画像を削除しました。これくらいのことは、ワンライナーでできそうな気がしたのですが、とっさに思いつきませんでしたので、誰か教えて下さい。

{% codeblock lang:bash ~/find_grep_sed.sh %}
{% raw %}
#!/bin/zsh

tmp=`find . -name "*" | xargs grep $1`

fil=`echo $tmp | cut -d : -f 1`
cha=`echo $tmp | cut -d : -f 2-`
cou=`echo $tmp | wc -l | tr -d ' '`

for (( i=1; i<=$cou;i++ ))
do
    file=`echo $fil | awk "NR==$i"`
    char=`echo $cha | awk "NR==$i"`
    sed -i '' "s#$char##g" $file
done
{% endraw %}
{% endcodeblock %}

こんな感じで使いました。

{% codeblock lang:bash %}
{% raw %}
$ find_grep_sed.sh '<img scr="https://lh'

$ find_grep_sed.sh '<img scr="http://lh'
{% endraw %}
{% endcodeblock %}

