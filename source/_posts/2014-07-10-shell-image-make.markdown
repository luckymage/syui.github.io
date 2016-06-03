---
layout: post
title: "ブログに載せる画像が多すぎる場合、処理を自動化するスクリプトを書いた"
date: 2014-07-10
comments: true
categories: [programming]
tags: [shellscript]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログに載せる画像が多すぎた場合、書くのを楽にするために。<!--more--><br clear="all">

{% codeblock lang:bash images_markdown.sh %}
{% raw %}
#!/bin/zsh

lhome=${0:a:h:h}
dir=${0:a:h}
dir_e=$1
file=`ls $dir_e | tr -d ' '`
file_n=$lhome/${dir_e}.html
line=`echo $file | wc -l | tr -d ' '`

touch $file_n

for (( i = $line; i > 0; i -- ))
do

    line_n=`echo $file | awk "NR==$i"`

cat << EOF >> $file_n

# ここに書式
![](/$dir/$dir_e/$line_n)

EOF

done

cat $file_n | pbcopy

# ファイルを削除したくない場合は、コメントアウト
rm $file_n
{% endraw %}
{% endcodeblock %}

例えば、以下の様なフォルダがあるとすると、スクリプトを`~/images/`に置き、そこで、`./images_markdown.sh 201407`とします。

{% codeblock lang:bash %}

~/images/201407
├── 01a.png
├── 01b.png
└── 01c.png

0 directories, 3 files
{% endcodeblock %}

`Markdown`形式での画像ファイルがクリップボードに取得されます。

{% codeblock lang:bash %}
# ここに書式
![](/images/201407/01a.png)

# ここに書式
![](/images/201407/01b.png)

# ここに書式
![](/images/201407/01c.png)
{% endcodeblock %}

