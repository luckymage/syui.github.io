---
layout: post
title: "Pythonのバージョン管理"
date: 2014-11-22
comments: true
categories: [programming, mac]
tags: python
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">いくつかの自作スクリプトが動作しなくなったので、バージョン管理します。<!--more--><br clear="all">

Pythonをアップデートする度に、起動しなくなるスクリプトが増えていき、さすがに、書きなおすのも面倒になってきたので、バージョン管理することにしました。

動作していたのは、大体、`python 2.6`辺りで、現在は、`python 2.7`にアップデートされています。

MacをMave...何とかに上げてからバージョン管理していなかったのですが、再度。昔は何を使っていたのかも忘れたので、調べるところから。


{% codeblock lang:bash %}
$ python -V
2.7.x

$ brew install pyenv pyenv-virtualenv

$ pyenv install -l

$ pyenv install 2.6.6

$ pyenv shell 2.6.6

$ exec $SHELL

$ python -V
2.6.6
{% endcodeblock %}

| コマンド | 内容 |
| --- | --- |
|$ pyenv install -l | インストール可能なバージョン一覧を表示
|$ pyenv install バージョン番号 | インストール
|$ pyenv uninstall バージョン番号 | アンインストール
|$ pyenv version | 現在のバージョンを表示
|$ pyenv versions | インストール済みバージョン一覧を表示
|$ pyenv shell バージョン番号 | カレントシェルでのバージョン切替
|$ pyenv local バージョン番号 | カレントディレクトリーでのバージョン切替
|$ pyenv global バージョン番号 | システム全体でのバージョン切替


参考:

<a href="http://blog.i97506051502.com/entry/2014/03/25/PythoninMacOSX" target="_blank">Python in Mac OS X - 限りなくクラウドに近いオンプレミス</a>

