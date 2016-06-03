---
layout: post
title: "git push rejected in Octopress"
date: 2014-07-02
comments: true
categories: [blog]
tags: [git, octopress]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">デプロイできなかった問題が解決しました。<!--more--><br clear="all">


{% codeblock lang:ruby Rakefile %}
- system "git push origin #{deploy_branch}"

+ system "git push origin +#{deploy_branch}"
{% endcodeblock %}

Octopressでは、コマンドスクリプトは、`Rakefile`にまとめられているようですね。

ここを書き換えてやればOKです。

`git`コマンドの`reject`エラーなので、誤差を無視すれば良いみたいでした。

<a href="http://stackoverflow.com/questions/17609453/rake-gen-deploy-rejected-in-octopress" target="_blank">rake gen_deploy rejected in Octopress - Stack Overflow</a>

