---
layout: post
title: "Octicons"
date: 2014-06-17
comments: true
categories: [blog]
tags: [octopress, github, css, html]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">GitHubからWeb Font、Icon Fontが登場しました。<!--more--><br clear="all">

{% githubrepo github/octicons %}


{% codeblock lang:bash %}
$ cd ~/octopress/source/

$ curl -o ~/Downloads/octicons.zip -Lk https://github.com/github/octicons/archive/master.zip

$ aunpack ~/Downloads/octicons.zip

$ cp -r ~/Downloads/octicons-master/octicons .

$ vim _includes/head.html
{% endcodeblock %}


あとは、`head`内に、以下のタグを挿入します。
{% codeblock lang:html source/_includes/head.html %}
{% raw %}
<link rel="stylesheet" href="/octicons/octicons.css">
{% endraw %}
{% endcodeblock %}

これで、Icon Fontを使用できるようになったはずです。

####<span class="octicon octicon-mark-github" style="font-size:30px;"></span>

{% codeblock lang:html SAMPLE http://octicons.github.com/icon/mark-github/ LINK %}
{% raw %}
<span class="octicon octicon-mark-github" style="font-size:30px;"></span>
{% endraw %}
{% endcodeblock %}

便利です。もうちょっとバリエーションが増えてくるとよいですね。

