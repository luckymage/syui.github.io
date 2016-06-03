---
layout: post
title: "Chromeで開いているタブをHTMLにする"
date: 2014-10-07
comments: true
categories: programming
tags: [applescript, shellscript]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">カドカワ祭りの時、たくさん紹介する都合で作りました。<!--more--><br clear="all">

{% codeblock lang:bash chrome_tab_html.sh %}
{% raw %}
#!/bin/zsh

url=`osascript -e 'tell application "Google Chrome" to get url of tab of window 1' | tr ',' '\n' | tr -d ' '` > /dev/null 2>&1

title=`
osascript << EOF
tell application "Google Chrome"
    set AppleScript's text item delimiters to "\n"
    set pageTitle to get title of tab of window 1
    --get title of tab of window 1
    set txt to pageTitle as text
end tell
EOF
`

count=`echo $url | wc -l | tr -d ' '`

for (( i=1; i <= $count; i++ ))
do
    h_url=`echo $url | awk "NR==$i"`
    h_title=`echo $title | awk "NR==$i"`
    echo "<a href=\"$h_url\" target='_blank'>$h_title</a>"
done
{% endraw %}
{% endcodeblock %}

AppleScriptでリストの区切り文字を変更するには、`set AppleScript's text item delimiters to {hoge}`を使います。


