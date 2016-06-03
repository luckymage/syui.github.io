---
layout: post
title: "MacBookの年式を調べるコマンドを作った"
date: 2014-09-27
comments: true
categories: os
tags: [ mac, macbook ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">元となるデータは手動で書いていくしかないので、辛いです。<!--more--><br clear="all">

##json-script

{% githubrepo syui/json-script %}

今後、何かあれば追加していければと思っています。

現在は、以下の様な感じで`MacBook`の年式を調べられます。

{% codeblock lang:bash %}
$ curl -sL https://raw.githubusercontent.com/syui/json-script/master/script/macbook-model-command.sh | sh
{% endcodeblock %}

URLの関係から、`gh-pages`に置こうかなと思いましたが、今のところ置いていません。

> 置きましたが、実行できるかは未検証です。`syui.github.io/script/macbook-model-command.sh`

###MacBookの年式を調べる

年式をコマンドで調べられないのかと思ったのですが、よく分かりませんでした。Webに当たると、機種IDに対応したモデルにて年式が公式ページより書かれているみたいでしたので、それを参照するコマンドを作りました。

{% codeblock lang:bash %}
{% raw %}
$ curl -s http://support.apple.com/kb/{HT1635,HT4132,HT3255} | sed -n '/<tbody/,/<\/tbody>/p' | grep -B 2 `system_profiler SPHardwareDataType | grep "Model Iden" |tr -d ' ' | cut -d : -f 2`  | tr -d '\t' | sed -e 's/<[^>]*>//g' -e '/^$/d'

# test:MacBookPro11,1
$ curl -s http://support.apple.com/kb/{HT1635,HT4132,HT3255} | sed -n '/<tbody/,/<\/tbody>/p' | grep -B 2 "MacBookPro11,1" | tr -d '\t' | sed -e 's/<[^>]*>//g' -e '/^$/d'

# test:MacBook7,1
$ curl -s http://support.apple.com/kb/{HT1635,HT4132,HT3255} | sed -n '/<tbody/,/<\/tbody>/p' | grep -B 2 "MacBook7,1"  | tr -d '\t' | sed -e 's/<[^>]*>//g' -e '/^$/d'
{% endraw %}
{% endcodeblock %}

###JSONの作成

また、ページより作成した`json`を置きました。

{% codeblock lang:bash %}
$ curl -s https://gist.githubusercontent.com/syui/f757c3f860659201c897/raw/macbook-model.json | jq .\"`system_profiler SPHardwareDataType | grep "Model Iden" | tr -d ' ' | cut -d : -f 2`\"
{% endcodeblock %}

`systeminfo`は`peco`とかで選択していくと便利そうです。

{% codeblock lang:bash %}
$ system_profiler -listdatatypes | peco | xargs system_profiler -detailLevel full -xml
{% endcodeblock %}

