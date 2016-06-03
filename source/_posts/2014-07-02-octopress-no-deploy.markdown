---
layout: post
title: "OctopressのDeployが上手くいかないので手動でPushすることにした"
date: 2014-07-02
comments: true
categories: [blog]
tags: [octopress, git]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">`git rebase -i --root`したらおかしくなってしまいました。<!--more--><br clear="all">


##commit logを削除する

{% codeblock lang:bash %}
$ git rebase -i --root

$ git rebase --continue

$ git add -A

$ git commit -a -m "rebase all delete"

$ git log

$ git push origin +master
{% endcodeblock %}


##deploy

{% codeblock lang:bash %}
$ rake gen_deploy
> Everything up-to-date
{% endcodeblock %}

リポジトリが更新されてない...。

##new repository

既存のリポジトリを削除し、同じリポジトリを作成。

{% codeblock lang:bash %}
$ rake generate

$ cd ~/octopress/build

$ git init

$ git add *

$ git commit -a -m "first commit"

$ git remote add origin https://github.com/syui/syui.github.io

$ git push -u origin master
{% endcodeblock %}

##source backup

上の階層に`.git`があることが前提。

{% codeblock lang:bash %}
$ cd ~/octopress/source

$ git add .

$ git commit -m 'your message'

$ git checkout -b source

$ git push origin source
{% endcodeblock %}

