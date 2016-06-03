---
layout: post
title: "WindowsでMSYS2を使う"
date: 2015-03-02
comments: true
categories: os
tags: windows, msys
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Cygwinからの移行。<!--more--><br clear="all">

[MSYS2](https://github.com/msys2)

http://msys2.github.io/

{% codeblock lang:bash %}
$ pacman -Syu

$ reset.exe

$ pacman -S zsh vim git tmux
{% endcodeblock %}

[Chocolatey](https://chocolatey.org/)で[MSYS2](https://github.com/msys2)をインストールする場合は、以下のような感じになりそう。


{% codeblock lang:bash %}
{% raw %}
C:\> choco install mingw
{% endraw %}
{% endcodeblock %}


ターミナルは、デフォルトの`mintty`を使っている人が多い感じがしたのですが、個人的には、`Console2`や`ConsoleZ`を使っているので、そちらの方で設定します。

Linuxユーザーは、基本的に、WindowsでもCygwinやMinGWなどを使ってしまいがちですが、個人的には、`PowerShell`を使えるに越したことはないなあと思っているので、微妙なところです。

http://tech.guitarrapc.com/

https://github.com/janikvonrotz/PowerShell-PowerUp

https://github.com/bdukes/PowerShell-Profile/

