---
layout: post
title: "GitHubにリポジトリを作成し、空PUSHをするスクリプト"
date: 2014-07-31
comments: true
categories: [programming]
tags: [git, github]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">たまに必要なことがありますので。<!--more--><br clear="all">

ちなみに、ディレクトリ名でリポジトリを作成します。

<script src="https://gist.github.com/syui/bc28c26c6bf7d7bac9d2.js"></script>

オプションとか付けても良いかもですね。`case`で`$1`を判断します。

{% codeblock lang:bash %}
case $1 in
  a)
            rm -rf .git
            git init
            git add *
            echo $url
            git remote add origin $url
            git commit -m "first commit"
            git push -u origin master
            ;;
  *)
            rm -rf .git
            git init
            echo $url
            git remote add origin $url
            git commit --allow-empty -m "noun"
            git push -u origin master
            ;;
esac
{% endcodeblock %}

