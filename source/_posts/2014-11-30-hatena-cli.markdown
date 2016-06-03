---
layout: post
title: "はてなのニュースをコマンドラインから選択する"
date: 2014-11-30
comments: true
categories: shell
tags: zsh
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">hatena-cli<!--more--><br clear="all">


##hatena-cli

<img src="http://lh3.ggpht.com/-HEJ3VLjnSc4/VHr91sB-qfI/AAAAAAAAAIM/QB5P22TZngk/s0/hatena_cli_demo_s.gif">

###まとめ

Mac, Linuxに対応しています。ShellScriptで書かれています。

https://github.com/syui/hatena-cli

{% codeblock lang:bash %}
$ sudo pip install percol

$ brew install gauche

$ git clone https://github.com/syui/hatena-cli

$ cd !$:t

$ ./hatena-cli
{% endcodeblock %}

###解説

まずは、インターフェイスのインストールです。Macでは、`percol`がオススメです。というか、変なバグが存在するので、`percol`しか動きません。これは、`gauche`のスクリプトに影響します。

{% codeblock lang:bash インターフェイスのインストール %}
sudo pip install percol

go get github.com/lestrrat/peco/cmd/peco/
{% endcodeblock %}

設定は、以下のようにセレクトできるようにしておきましょう。`peco`でも`percol`でもできます。

{% codeblock lang:bash ~/.peco/.config.json %}
{
  "Keymap": {
    "C-s": "peco.ToggleSelectionAndSelectNext",
    "C-a": "peco.SelectAll",
    "C-g": "peco.SelectNone",
  }
}
{% endcodeblock %}

