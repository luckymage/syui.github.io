---
layout: post
title: "Octopressのgist_tag.rbが動作しない問題について"
date: 2014-06-23 01:44:34 +0900
comments: true
categories: [blog]
tags: [octopress, gist, plugin]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopress に入ってる Gist Tag Plugin は動作しないようです。<!--more--><br clear="all">

[octopress-gist](https://github.com/octopress/octopress-gist)

ということで、以下のコードを参考に書き直します。

{% codeblock lang:bash %}
$ cd ~/octopress/source/plugins/

$ curl -O https://gist.githubusercontent.com/j5ik2o/5550083/raw/gist_tag.rb
{% endcodeblock %}

{% gist 5550083 %}

すると、以下の様な書式が使えるようになります。

{% raw %}
      {% gist 5672127 %}

      {% gist 13411532 some_gist_file_name.rb %}
{% endraw %}

参考:

<a href="http://j5ik2o.me/blog/2013/05/10/gist-tag/" target="_blank">OctopressのGist Tagプラグインを改造してみた - じゅんいち☆かとうの技術日誌</a>

