---
layout: post
title: "github-card"
date: 2014-07-06
comments: true
categories: [blog]
tags: [github]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">github-cardを使ってみました。<!--more--><br clear="all">

{% githubrepo pazguille/github-card %}

{% codeblock lang:bash %}
git clone https://github.com/pazguille/github-card ~/Downloads/github-card

cp -rf ~/Downloads/github-card/webcomponent ~/octopress/source/_includes/
{% endcodeblock %}

後は、設定ファイルである`_config.yml`を編集しましょう。

{% codeblock lang:html _config.yml %}
default_asides: [ webcomponent/github-card.html ]
{% endcodeblock %}

`github-card`の設定を分けるのも面倒なので、直接書くことにします。

本体の行末に以下を追記してください。

{% codeblock lang:html source/_includes/webcomponent/github-card.html %}
{% raw %}
<github-card user="username"><github-card>
{% endraw %}
{% endcodeblock %}

後は、読み込みとプレビューです。

{% codeblock lang:bash %}
$ rake generate

$ rake preview
{% endcodeblock %}



気に入らないところは直しましょう。

