---
layout: post
title: "Macのバッテリーを通知する"
date: 2014-09-05
comments: true
categories: os
tags: [ mac, battery ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">たまに忘れがちになるので。<!--more--><br clear="all">

{% githubrepo syui/osx_battery %}

{% codeblock lang:bash %}
$ git clone https://github.com/syui/osx_battery

$ cd !$:t

# 通知
$ ./battery_notfiy.sh &

# バッテリー残量
./battery_current.sh

# json形式でバッテリー情報を出力する
./battery_json.sh

# jqでバッテリー情報を取得
./battery_json.sh | jq .

# jqでバッテリー残量を取得
./battery_json.sh | jq .Current
{% endcodeblock %}

テストは、`battery_notfiy.sh`に書いておきました。テスト箇所、コメントアウトして使ってください。

{% codeblock lang:bash battery_notfiy.sh %}
#!/bin/zsh
dir=${0:a:h}
bat=`$dir/battery_current.sh`

##通知するバッテリーの残量
#not=20

## テスト
not=$((bat - 1))

while [ $bat -gt $not ]
do
    bat=`$dir/battery_current.sh`
    sleep 10
done

growlnotify -a Finder -m "Battery $bat %"
{% endcodeblock %}

現在は、値の場所から情報を取得しているため、場所が変動すると動作しません。よって、本来なら`jq`依存にしたほうが良いかもだけど。

