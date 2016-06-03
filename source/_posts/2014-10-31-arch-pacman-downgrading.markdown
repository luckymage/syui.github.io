---
layout: post
title: "Arch Linuxのパッケージ復元方法"
date: 2014-10-31
comments: true
categories: linux
tags: [arch, pacman]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">今回は、自分のミスではなく、パッケージに問題があった場合の対処法を記録します。<!--more--><br clear="all">

##状況報告

パッケージをアップグレードしたら、特定のアプリが動かなくなりました。しかし、それに気づかず、キャッシュを削除したため、復元が困難に...。

{% codeblock lang:bash %}
$ sudo pacman -Syuu

$ sudo pacman -Scc
{% endcodeblock %}

ここで、キャッシュを削除していない場合は、パッケージのダウングレードは簡単です。

{% codeblock lang:bash %}
$ sudo pacman -U /var/cache/pacman/pkg/pkgname-olderpkgver.pkg.tar.gz
{% endcodeblock %}

##パッケージ情報の収集

ログを確認し、問題があったパッケージとバージョンを推測したりします。

{% codeblock lang:bash %}
$ cat /var/log/pacman.log

$ pacman -Si ibus
{% endcodeblock %}

##パッケージの検索

スクリプトを使うか、手動で検索することになります。

{% codeblock lang:bash %}
$ sudo pacman -S downgrade

$ sudo downgrade ibus
{% endcodeblock %}

https://aur.archlinux.org/

`downgrade`の簡単なスクリプトを作ってみました。

{% codeblock lang:bash air-downgrade %}
{% raw %}
#!/bin/zsh
list=`cat /var/log/pacman.log | grep $1 | grep upgraded | cut -d ' ' -f 5`
numb=`echo $list | wc -l | tr -d ' '`
for (( i=1; i<=$numb; i++ ))
do
  pack=`echo $list | awk "NR==$i"`
  downgrade $pack
done
{% endraw %}
{% endcodeblock %}

使い方は簡単で、ちゃんと動作した日付を指定します。すると、その日付のパッケージを一括ダウングレードします。ログとか消さない人は、年数も指定したほうが良いかもしれません。

{% codeblock lang:bash %}
$ ./air-downgrade 10-10
{% endcodeblock %}

一応、`yes`と`1`を自動で選択するようにしたスクリプトを公開しておきます。つなげて使うことで、一括ダウングレードできます。

{% githubrepo syui/downgrade %}

##パッケージのインストール

`downgrade`コマンドでインストールしなかった(ダウンロードのみだった)場合。

{% codeblock lang:bash %}
$ sudo pacman -U /var/cache/pacman/pkg/pkgname-olderpkgver.pkg.tar.gz
{% endcodeblock %}

##複数のパッケージをダウングレードしたい場合

<a href="https://wiki.archlinux.org/index.php/Arch_Rollback_Machine_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Arch Rollback Machine</a>を使うと良いかもしれません。

##パッケージを維持するための対策

`-Syu`でアップグレードするときに不便なので、アップデートしないパッケージのリストを作ります。

{% codeblock lang:bash %}
$ sudo vim /etc/pacman.conf

#区切りはスペースを使います
IgnorePkg   = ibus ibus-setup
{% endcodeblock %}

##参考リンク

<a href="https://wiki.archlinux.org/index.php/Pacman_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">pacman (日本語) - ArchWiki</a>

<a href="https://wiki.archlinux.org/index.php/Pacman_Tips_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Pacman Tips (日本語) - ArchWiki</a>

<a href="https://wiki.archlinux.org/index.php/Downgrading_Packages_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Downgrading Packages (日本語) - ArchWiki</a>


##まとめ

問題が起こった場合の復元方法が身につきますので、皆様、OSには、`Arch`を使いましょう。


