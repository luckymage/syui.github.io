---
layout: post
title: "GitHubに登録する公開鍵を最強クラスにしてみた"
date: 2014-07-05
comments: true
categories: [terminal]
tags: [github, git]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ECDSA鍵の521bitを使用します。<!--more--><br clear="all">

<h2>ECDSA</h2>

`ECDSA`というのは、SSHで使われている鍵の種類で、他に`DSA`,`RSA`があります。

`ECDSA`は、小さいbitを指定しても、強力な暗号化が実行されます。

> 521bit ECDSA鍵は15360bit RSA鍵に相当するそうです

ここで、鍵の指定とbitの指定は以下のオプションで行います。

{% codeblock lang:bash %}
$ ssh-keygen -t ecdsa -b 521
{% endcodeblock %}

デフォルトでは、`RSA`で`2048`が指定されます。

{% codeblock lang:bash %}
$ ssh-keygen -N "" -t rsa -b 2048
{% endcodeblock %}

`-N`はパスフレーズの指定です。指定した場合、GitHubでは、指定したパスフレーズの省略が必要です。

{% codeblock lang:bash %}
$ ssh-add ~/.ssh/id_rsa
{% endcodeblock %}

<a href="http://d.hatena.ne.jp/hnw/20140705" target="_blank">GitHubユーザーのSSH鍵6万個を調べてみた - hnwの日記</a>

<h2>MacのOpenSSHでECDSAを使えるようにする</h2>

まず、Macの`OpenSSH`で`ECDSA`を使えるようにします。

{% codeblock lang:bash %}
$ brew tap homebrew/dupes

$ brew install openssh --with-brewed-openssl --with-keychain-support

$ exec $SHELL
{% endcodeblock %}

好みで以下の設定を行ってください。

{% codeblock lang:bash %}
$ launchctl stop org.openbsd.ssh-agent

$ launchctl unload -w /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist

$ sudo vi /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist
{% endcodeblock %}

そこで、`/usr/bin/ssh-agent`の部分を`/usr/local/bin/ssh-agent`に変更します。

{% codeblock lang:html /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist %}
<string>/usr/local/bin/ssh-agent</string>
{% endcodeblock %}

設定を反映します。

{% codeblock lang:bash %}
# 読み込み
$ launchctl load -w -S Aqua /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist

$ export SSH_AUTH_SOCK=$(launchctl getenv SSH_AUTH_SOCK)
{% endcodeblock %}

##GitHubへの公開鍵の登録

{% codeblock lang:bash %}
$ cd ~/.ssh && ls

$ ssh-keygen -N "" -t ecdsa -b 521 -C "your_email@example.com"

$ pbcopy < ~/.ssh/id_ecdsa.pub
{% endcodeblock %}

あとは、Webから登録するのが良いです。

<a href="https://help.github.com/articles/generating-ssh-keys" target="_blank">Generating SSH Keys · GitHub Help</a>

確認です。成功すると以下のメッセージが出ます。
{% codeblock lang:bash %}
$ ssh -T git@github.com
> Hi username! You've successfully authenticated, but GitHub does not provide shell access.
{% endcodeblock %}

