---
layout: post
title: "Installing Arch Linux on Mac OSX Yosemite with Virtual Box"
date: 2014-12-20
comments: true
categories: [virtual,mac,linux]
tags: [iesd,manjaro,awesome,arch]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">最近、よく Linux でデスクトップで使っているキーバインドと Mac で使っているキーバインドを押し間違えるので、本気で MacBook Air に Arch Linux を入れようか迷っています。ということで、一応、前準備として、 VirtualBox 上で Mac の Yosemite を動かしてみました。<!--more--><br clear="all">

##Arch Linux 上で Yosemite を動かす方法

###iesd

そのままでは、起動ディスクが使えないので、[iesd](https://github.com/ntkme/iesd)を使います。

https://github.com/ntkme/iesd

まず、App Storeからインストールディスクをダウンロードします。ダウンロード完了後、インストール画面を閉じて、`/Applications/`以下に`Yosemite`があることを確認。以下のコマンドを実行します。これらの手順、具体的には、`VM Image`を作るのは、 Mac から行いますので、それまでは、 Mac を起動できる状態にしておいてください。

{% codeblock lang:bash %}
$ cd ~/Downloads

$ gem install iesd

$ iesd -i /Applications/Install\ OS\ X\ Yosemite.app/ -o Yosemite.dmg -t BaseSystem
{% endcodeblock %}

`~/Downloads`に`Yosemite.dmg`が出来上がっていれば完成です。これは、マウントディスクから作られます。失敗した場合は、そのディスクを手動でアンマウントしてから、問題解決後、再度、`iesd`コマンドを実行することになります。

###VirtualBox

次に、`VM Image`を作成します。 VirtualBox を起動し、適当なディスクを作成後、以下のコマンドを実行します。これは、`2013`までのマシンを使っている場合は、必要みたいな感じです。でないと、`Yosemite.dmg`が起動できません。`<vmname>`は任意のものを入れます。

{% codeblock lang:bash %}
$ VBoxManage modifyvm <vmname> --cpuidset 00000001 000306a9 00020800 80000201 178bfbff

$ VBoxManage startvm <vmname>
{% endcodeblock %}

起動後は、ディスクのフォーマットを Mac のものにしなければなりません。したがって、メニューから以下のものを選択し、フォーマットします。英語。

{% raw %}
    "Utilities" -> "Disk Utility…" to launch the Disk Utility
{% endraw %}

フォーマットできたら、そのディスクに Yosemite をインストールしましょう。インストール後は自動で再起動がかかりますので、その時は、`CD/DVD`にある`Yosemite.dmg`をアンマウントしておきます。

これで、ディスクにインストールした Yosemite が起動します。この手順でできた`~/VirtualBox\ VMs/{vmname}`を Arch Linux などをインストールしたマシンにコピーし、 VirtualBox 上で `M-m,A(dd)`します。

![](http://lh6.ggpht.com/-eoyFQic1CyM/VJS_yZCAmwI/AAAAAAAAAKs/_HIlKeZftyc/s0/ArchLinux_on_Mac_OSX_Yosemite.png)

###参考になりそうな記事:

https://ntk.me/2012/09/07/os-x-on-os-x/

http://engineering.bittorrent.com/2014/07/16/how-to-guide-for-mavericks-vm-on-mavericks/

##なぜ Mac を卒業しようと思ったのか

###Mac 歴など

思えば、 Mac を使い始めてからあまりにも長すぎる月日が流れ、もう2,3年も過ぎます。初めての Mac は確か、2011,2012年辺だったです。

しかし、結局のところ、これほど長い時間をかけて使っていても、全くと言っていいほど、パソコンを使いこなせず、 Mac 初心者の状態を抜け出すことができませんでした。

と言っても、これは Mac を卒業しようと思った本質的な理由ではなく、私は基本的に、コンピュータ音痴なので、理由にはなりえません。

###バージョンアップ

では、なぜ Mac を卒業しようと思ったのかというと、年々変化する OS バージョンに対応するのが面倒だからというものです。私が経験しただけでも、これまで、 Mountion Lion, Mavericks, Yosemite など数々のバージョンがありました。しかし、コロコロと変化するインターフェイスやアイコン、そして、機能など初心者にとっては割とどうでもよく、または迷惑な変化に対し、正直、嫌気がさしました。また、バージョンアップに伴う不都合に対応するのも、相当面倒でした。

これらは、 Linux の場合は割りと許容できる要素ではありますが、なぜか Mac では許容できないというか、許容しにくかったです。

今までは、サブノートである MacBook Air(Mid 2011) には、 Linux を入れてたわけですが、メインノートである MacBook Air(Mid 2013)には、Mac で運用していました。

しかし、これからは、メインノートにも Linux を入れることを考えていて、本格的に Linux ユーザーに移行できそうです。

ちなみに、私は、デュアルブートやトリプルブートというものはしません。やったことはあるのですが、結局のところ片方しか使わないので。

###懸念事項

ただし、 Mac から Linux に移行する最大の懸念事項として、 Xcode で開発したくなった場合、果たして、仮想環境下で上手く動作するのかという点です。これらは、一度検証してみなければなりません。

また、表示全体の綺麗さというのが失われてしまうのは、結構厳しいかもしれません。これは、画像やWebページ編集など様々な分野に影響しそうに思われます。

##MacBook Air というマシン

###好きなマシン

ここで、 Linux を使うなら、 MacBook Air というマシンでなくてもいいんじゃないかという声が聞こえてきそうですが、このマシンは、個人的にめちゃくちゃ気に入っているのですね。

その理由は幾つもあるのですが、まずは、外観がシンプルだということ。

そして、 Linux が動作しやすいというところです。実は、 MacBook で Linux を動かすユーザーは結構多くて、有名なマシンほど、快適に動作するし、調整しやすいというところがあります。例えば、以下のようなページも作成されています。

<a href="https://wiki.archlinux.org/index.php/MacBook_%28%E6%97%A5%E6%9C%AC%E8%AA%9E%29" target="_blank">MacBook (日本語) - ArchWiki</a>

###ステッカーなど

あと、 Apple ロゴが気に入らない人は、ステッカーなどがありますので、そちらを貼れば良いと思われます。

<a href="http://www.zazzle.co.jp/linux+%E3%82%B7%E3%83%BC%E3%83%AB" target="_blank">Linuxシール、ステッカー</a>

<a href="http://www.unixstickers.com/" target="_blank">Linux & Coding stickers and merchandise - Unixstickers</a>


<a href="https://www.iconfinder.com/search/?q=archlinux" target="_blank">Archlinux icons - Download 1 free & premium icons on Iconfinder</a>


