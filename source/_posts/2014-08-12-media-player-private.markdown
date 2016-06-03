---
layout: post
title: "個人的なメディア環境"
date: 2014-08-12
comments: true
categories: [ private, os ]
tags: [ mac, linux, music]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">個人的なメディアファイルの管理について紹介します。<!--more--><br clear="all">

##きっかけ

この前、`wine`をインストールしたら、パスがおかしくなったみたいで、`mplayer`が動かなくなりました。

{% codeblock lang:bash アップデートと再インストール %}
{% raw %}
$ mplayer
> dyld: Library not loaded: /usr/local/lib/libpng15.15.dylib

$ brew update && brew upgrade

$ brew reinstall mplayer
{% endraw %}
{% endcodeblock %}

そんなこともあり、音楽環境などを考えなおしてみようかなと思ったのですが、やっぱり今のままで全く不便はありませんので、プレイヤーやファイル管理の変更は行いませんでした。

ここで、良い機会なので、個人的な音楽環境などを晒したいと思います。

##音楽


> パソコン : mplayer
>
> スマホ : GoodReader
>
> タブレット : ES ファイルエクスプローラー

私の音楽環境は、非常にシンプルです。ただ、フォルダに音楽ファイルが入れられているだけで、それを`mplayer`で再生します。したがって、スマホやタブレットでも基本、ファイルマネージャーを使って再生します。

{% codeblock lang:bash %}
{% raw %}
$ find `pwd` -maxdepth 1 -mindepth 1 | grep -v "\/\." > mylist

$ mplayer -playlist mylist -novideo -speed 2 -af scaletempo,volnorm -loop 20
{% endraw %}
{% endcodeblock %}

正直、Appleの`iTunes`とかGoogleの`Google Play`もそうですが、全く使う気にならないです。

何故かと言うと、これらのプレイヤーは、余計なことをしすぎなのです。あくまで、私にとってですが。

更に、私自身、iTunesで曲などを購入したことがあるのですが、これらのストアで購入したファイルは、あくまで、特定のアカウントの、かつ特定の環境下での、さらに特定のプレイヤーでしか再生できないようになっています。

これは、電子書籍や動画についても言えることで、こういったものでファイルを管理してしまうと、様々な環境下、特に、Linuxを使用するユーザーにとっては、どうしても使い勝手が悪いものになってしまいます。

私の経験では、iTunesでいくつかの曲を購入したことがありますが、結局のところ、そこで購入し管理していた曲は、いつの間にか聴かなくなっていました。

そして、その時、これは、非常に勿体無いことだなと思いました。多分、今後、私がiTunesで曲を購入することは、多分ないだろうと思います。ボカロ以外で、どうしても聴きたい曲が出てくれば、究極、CDを購入してそこから持ってくるでしょうね。

スマホやタブレットでも、基本、ファイルマネージャーを使用します。そういえば、最近、`ES ファイルエクスプローラー`、盗聴疑惑で目立ってますね。盗聴アプリは、これだけではなく、オープンソース以外の主要アプリはほとんどなので、あまり気にしてませんが。

##動画

> パソコン : VLC, mplayer
>
> タブレット : DICE Player

動画に関しても`mplayer`で再生できます。ただし、音楽は流しっぱなしが多く、動画は選択が多いので、`VLC`を使います。インターフェイスは、コマンドラインで動作するものを使用します。

{% codeblock lang:bash %}
$ /Applications/VLC.app/Contents/MacOS/VLC --rate=2

$ killall -KILL VLC && reset
{% endcodeblock %}

`DICE Player`もアレ関連を気にする人はあまり使わないほうが良いかもです。

##書籍

![](https://lh5.googleusercontent.com/-tovEIM8DCgw/UHlEilChBxI/AAAAAAAABeo/6VyCsBpq-zo/s0/bookmark.png)

> 立ち読み : kindle
>
> パソコン : comix
>
> タブレット : A COMIC VIEWER, Perfect Viewer

`kindle`で購入した本もいくつかあるのですが、やはり、使い勝手が良くないと感じています。

常にインターネットに接続した環境下でしか有効に動作せず、さらには、特定のアカウントやアプリが必要になるからです。

したがって、立ち読みというか、購入検討用にkindleを使うことはあっても、ここで購入することは少なくなりました。

私の場合、オフラインで読むこともあり、更には、お気に入りのビューア、具体的には、`comix`などで読みたいことも多いので、現在は、自炊といって、実物からスキャンした物を使います。実物は、Amazonで注文するか、本屋で購入することにしています。

{% codeblock lang:bash %}
$ comix O'Reilly - C++ Cookbook (2007).zip
{% endcodeblock %}

https://github.com/vhf/free-programming-books/blob/master/free-programming-books.md

また、kindleも含め、ネットで購入できるあらゆるメディアファイルについて言えることですが、ユーザーは、借りているという形態の契約を結んでいることが通常です。

つまり、支払っているお金は、レンタル料であり、売買代金ではないのですね。よって、ここで購入したものは、自分のものではないので、会社側が何らかの都合で貸さないと言えば、すぐにでも購入したはずの本は読めなくなってしまいます。

なので、私の場合は、本に限って言えば、割と実物にこだわっているところがあります。それをスキャンし、タブレットで読むことが多いのです。

しかし、1回しか読まないと言うような本は、わざわざスキャンしないこともあります。

