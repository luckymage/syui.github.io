---
layout: post
title: "Vagrant上のCoreOSでRocketを使う"
date: 2015-01-25
comments: true
categories: [os, virtual]
tags: [coreos, vagrant, rocket, docker]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Dockerを使った経緯です。予想したとおり、Docker辺りのツールは、セキュリティ的な問題が来てます。<!--more--><br clear="all">

##CoreOS

`CoreOS`について書かれた記事です。`Docker`について言及されています。

> Dockerのforkとしなかった理由については、「全てが中央のデーモン（プロセス）を通じて実行されるDockerの処理モデルには、セキュリティと再利用性において根本的な欠陥がある。こうした問題に対応しないまま、Dockerの破綻したセキュリティモデルをサポートし続けることはできない」と言い切っている。

http://www.atmarkit.co.jp/ait/articles/1412/02/news108.html

ということで、[Vagrant](https://www.vagrantup.com/)上の[CoreOS](https://coreos.com/)で[Rocket](https://github.com/coreos/rocket)を使ってみました。

簡単に説明すると、`Vagrant`は`VirtualBox`を簡単に扱うものです。ラッパーという短縮スクリプトという感じのツールという印象です。`Docker`に似てる感じはするのですが、バージョン管理的な機能は、`Docker`が必要なのかもですね。

`CoreOS`は、コンテナという概念を用いて運用するOSのことです。コンテナは、使い捨てと独立という要素を意味する感じです。OS自体は、Gentoo Linuxのような必要最小限の構成と、独自の安全なセキュリティアップデートを採用している感じですね。

`Rocket`は、`Docker`の代わりに採用されたものという感じでしょうか。仮想環境の構築運用支援ツール。

ここで、これからやる図、目標としては、以下のような感じになると思います。仮想環境に仮想環境を作るという感じですね。

{% raw %}
    [Mac-Vagrant]-[CoreOS-Rocket]-[http-server]
{% endraw %}

###vagrant

[Vagrant](https://www.vagrantup.com/)は、`homebrew-cask`を使うことでもCUIでのインストールは可能です。

自分で用意してもいいし、他人が作ったのを使ってもいいです。ただし、メンテされてないなどから危険も伴うので、気をつけてくださいと思います。

{% codeblock lang:bash Mac %}
$ brew tap phinze/homebrew-cask

$ brew install brew-cask

$ brew cask install vagrant
{% endcodeblock %}

{% codeblock lang:bash %}
{% raw %}
$ git clone https://github.com/coreos/coreos-vagrant/

$ cd coreos-vagrant

$ vagrant up

$ vagrant ssh
{% endraw %}
{% endcodeblock %}

###rocket(rkt)

{% codeblock lang:bash CoreOS %}
$ wget https://github.com/coreos/rocket/releases/download/v0.2.0/rocket-v0.2.0.tar.gz

$ tar xzvf rocket-v0.2.0.tar.gz

$ ./rocket-v0.2.0/rkt help
{% endcodeblock %}

###appc-spec(actool)

{% codeblock lang:bash CoreOS %}
$ wget https://github.com/appc/spec/releases/download/v0.1.1/appc-spec-v0.1.1.tar.gz

$ tar zxf appc-spec-v0.1.1.tar.gz
{% endcodeblock %}

###golang(go)

{% codeblock lang:bash CoreOS %}
$ wget https://storage.googleapis.com/golang/go1.3.3.linux-amd64.tar.gz

$ sudo mkdir /opt

$ sudo tar zxf go1.3.3.linux-amd64.tar.gz -C /opt/

$ cat << EOF >> ~/.bash_profile
export GOROOT=/opt/go
export GOPATH=~/go
export PATH=$GOROOT/bin:$GOPATH/bin:$PATH
EOF

$ mkdir ~/go

$ exec $SHELL -l

$ go version
{% endcodeblock %}

###http-server

{% codeblock lang:bash CoreOS %}
# actoolでコンテナを作ります
$ git clone https://github.com/syui/hello-aci

$ CGO_ENABLED=0 GOOS=linux go build -a -tags netgo -ldflags '-w' hello-aci/rootfs/bin/hello.go

$ mv hello hello-aci/rootfs/bin/

$ rm -rf hello-aci/.git

$  ./appc-spec-v0.1.1/actool build hello-aci/ hello.aci

# rktでコンテナを起動します
$ sudo ./rocket-v0.1.1/rkt --debug run hello.aci
{% endcodeblock %}

コンテナを落としたいときは、`C-]`を3回押します。

試しにアクセスしてみましょう。アクセスログが表示されると思います。

{% codeblock lang:bash Mac %}
$ vagrant ssh

$ curl 127.0.0.1:5000
{% endcodeblock %}


参考:

http://blog.takady.net/blog/2015/01/13/coreos-rocket/


