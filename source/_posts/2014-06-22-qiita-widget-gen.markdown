---
layout: post
title: "Qiita Widget のカスタマイズ"
date: 2014-06-22
comments: true
categories: [blog]
tags: [octopress, qiita, widget, css, javascript, node]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Qiita Widget をカスタマイズしてみました。これだけ配色が浮いてたので...。<!--more--><br clear="all">

私のブログは現在、青系でなので、 Qiita の緑系はちょっと合わなかったのです。

ここで、[Qiita Widget ジェネレーター](https://github.com/tq-jappy/qiita-widget)が公開されています。

`node`や必要なものをインストールします。

{% codeblock lang:bash %}
$ curl -L git.io/nodebrew | perl - setup

$ export PATH=$HOME/.nodebrew/current/bin:$PATH

$ nodebrew install-binary v0.11.13

$ brew install npm

$ npm -g install recess

$ npm -g install coffee-script

$ npm -g install uglify-js
{% endcodeblock %}

使い方は、`Source/style.less, script.coffee`を変更し、コンパイル、ブラウザでの表示確認という感じです。

{% codeblock lang:bash %}
$ git clone https://github.com/tq-jappy/qiita-widget

$ cd !$:t

$ ./compile.php > script.js

$ open example.html
{% endcodeblock %}

最終的には以下のようになりました。アイテム数は、`10`に設定しています。同ファイルの`/items?per_page=10`の部分を変更します。



{% codeblock lang:js source/javascript/qiita.js %}
{% raw %}
  template = "<!DOCTYPE html>\n<html lang=\"ja\">\n<head>\n<meta charset=\"utf-8\" />\n<style type=\"text/css\">\nbody{padding:0;margin:0;font-family:'Trebuchet MS','Arial','Helvetica','ヒラギノ角ゴ Pro W3','Hiragino Kaku Gothic Pro','メイリオ',Meiryo,'ＭＳ Ｐゴシック','MS PGothic',sans-serif;background:#fff;border:0px solid #ddd}.bar{height:30px;overflow:hidden;line-height:30px;text-overflow:ellipsis;white-space:nowrap;vertical-align:middle;background:-webkit-linear-gradient(top,#313a29,#21291a);background:-moz-linear-gradient(top,#313a29,#21291a);background:-ms-linear-gradient(top,#313a29,#21291a);background:-o-linear-gradient(top,#313a29,#21291a);background:linear-gradient(top,#313a29,#21291a);border-bottom:3px solid #59bb0c}.logo{display:block;float:left;width:65px;height:30px;padding:0 10px;margin:0 15px;background:#59bb0c url(/images/qiita_logo.png) center center no-repeat}a.user{font-size:14px;color:#fff;text-decoration:none}a.user:hover{text-decoration:underline}.avatar{width:14px;height:14px;margin-right:3px}.title{color:#117ec6;text-decoration:none;word-wrap:break-word}.title:hover{text-decoration:underline}.tag{display:inline-block;height:14px;padding:0 3px;margin:0 2px;font-size:10px;line-height:14px;color:#fff;text-decoration:none;vertical-align:middle;background-color:#428bca;border-radius:3px}.tag:hover{text-decoration:underline}div#items{padding-bottom: 33px;} div#items.items { background: url(/images/qiita_logo.png) 1px #fff no-repeat; background-position: 50% 99%; } .item{padding:10px 15px;font-size:14px;line-height:18px;border-bottom:1px solid #ddd}\n</style>\n</head>\n<body>\n<div class=\"items\" id=\"items\"></div>\n</body>\n</html>";
{% endraw %}
{% endcodeblock %}

ちなみに、ファイルの配置は所定の場所に置きましょう。

{% codeblock lang:bash %}
$ mv Source/logo.png Source/qiita_logo.png

$ cp !$ ~/octopress/source/images

$ mv script.js qiita.js

$ cp !$ ~/octopress/source/javascript
{% endcodeblock %}

