---
layout: post
title: "はてなブックマークのアイコンをちゃんと表示するようにした"
date: 2014-06-19
comments: true
categories: [blog]
tags: [octopress, hatena, icon]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">今まで公式なアイコンじゃなかったので。<!--more--><br clear="all">


####正しい表示



####間違った表示




面倒だったので、似たアイコンでいいやと思っていたのだけど、以下の記事が出てました。


<a href="http://syncer.jp/hatebu-api-matome" target="_blank">【保存版!?】はてブAPIでwebサービスを作りたい全ての人に向けて書きました - Syncer</a>


ということで、まるで自分のこと言われているみたいだったので、修正。

{% codeblock lang:css CSS %}
span.icon-hatena {
  font-size:26px;
  font-weight: bold;
  font-family:'Verdana';
  color: #fff;
}

span.icon-hatena:hover {
  -webkit-transition: 0.3s ease-in-out;
  -moz-transition: 0.3s ease-in-out;
  -o-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
  color: #3366CC;
}
{% endcodeblock %}

{% codeblock lang:html HTML %}
{% raw %}
<a href="http://b.hatena.ne.jp/add?mode=confirm&url={{ site.url }}{{ page.url }}&title={{ page.title }}" target="_blank"><span class="hatena-name">{% if site.share_button_hatena %}<span class="icon-hatena"
style="float: left;
font-size: 20px;
padding-left: 5px;"
>B!</span>{% endif %} Bookmark</span></a>
{% endraw %}
{% endcodeblock %}


