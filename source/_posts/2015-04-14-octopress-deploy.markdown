---
layout: post
title: "Octopressのデプロイ"
date: 2015-04-14
comments: true
categories: blog
tags: octopress
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopressのデプロイの仕組み<!--more--><br clear="all">

Octopressの`deploy`も通ったことなので、ここで、少しだけ仕組みを紹介。

これは、`Rakefile`に書いてありますが、簡単には、`soruce`ディレクトリを`build`してできた`public`ディレクトリから`_deploy`を作り、このブログでいうと、`syui.github.io`リポジトリの`master`ブランチに`deploy`するということになっています。

言葉で説明すると、かなり複雑ですね。しかし、仕組み自体は単純です。

私の場合は、以下のような感じで済ませました。ソースファイルもGitHubの`theme`ブランチに置いてありますし、それを持ってきて、ブログを作ります。

{% codeblock lang:bash %}
$ git clone https://github.com/syui/syui.github.io

$ cd syui.github.io/

$ git checkout theme

$ mkdir _deploy

$ cp -rf .git _deploy

$ cd _deploy

$ git checkout master

$ rake gen_deploy
{% endcodeblock %}

こんな感じでできます。他にももっとスマートな方法がりますが、こちらのほうが確実かと。これは、すでにリポジトリがある場合の手順です。

上記のコマンドでわかると思いますが、要は、`_deploy`に`master`ブランチの`.git`をおけば良いということです。したがって、初めての方は、以下のようなコマンドを使います。

{% codeblock lang:bash %}
$ mkdir _deploy

$ cd _deploy

$ git init

$ git pull origin master
{% endcodeblock %}

場合によっては、強制的な手段で、`public`を`git push`すると良いでしょう。

ただし、`user.github.io`のリポジトリでは、`master`ですが、それ以外は、`gh-pages`になると思われます。

