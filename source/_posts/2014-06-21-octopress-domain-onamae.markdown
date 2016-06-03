---
layout: post
title: "このブログで設定していた独自ドメインについて"
date: 2014-06-21
comments: true
categories: [blog]
tags: [octopress, domain, github, dns]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">いきなりアクセスできなくなっていたので、再設定しました。<!--more--><br clear="all">

まず、以下の設定で独自ドメインを適用できるとのことで、この前まで`syui.co`というドメインで運用していました。

<a href="https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider" target="_blank">Tips for configuring an A record with your DNS provider · GitHub Help</a>

しかし、リダイレクトされるものの、内容が全く反映されないので、しばらく独自ドメインの使用は控えることにしました。

具体的には、[お名前.com](http://www.onamae.com/)で設定していた A レコードを削除し、 Octopress の CNAME ファイルを削除しました。

{% codeblock lang:bash %}
$ rm source/CNAME
{% endcodeblock %}

さらに、デフォルト URL も変更していたので、それも元に戻しました。

{% codeblock lang:html _config.yml %}
url: http://syui.github.io
{% endcodeblock %}

これで独自ドメインへのリダイレクトは解除され、`http://syui.github.io`へのアクセスとサイトの表示が復活します。

ここで、`独自ドメイン`を使用する場合は、そのドメインが失効することも考え、設定ファイル`_config.yml`は独自ドメインを使うべきではないと反省しました。

次に、`独自ドメイン`でやりたかったこともひと通りできたので、有効期間はだいぶ残っているものの、取得したドメインを失効しようと思いましたが、`お名前.com`の場合は、これが容易では無いようです。

<a href="http://www.onamae.com/service/dom/dom_change/abolition.html" target="_blank">ドメインの廃止</a>

また、退会についても非常に不親切だとか。

<a href="http://on-ze.com/archives/216" target="_blank">オンズ » ［お名前.com］を退会するのがエラい大変だった件！</a>

正直、当該企業の広告とかを見ていても、`お名前.com`は少し胡散臭さが漂うように感じていました。

よって、ドメインを取得する場合は、`お名前.com`はあまりおすすめではないなというのが、現時点での私の結論です。

設定はすごくやりやすかったのですが、広告と配信メールがとにかくすごかった...。

しかし、独自ドメインを初めて取得してみて、色々と実験できたのは良かったです。

ここで、その成果を以下にまとめていきます。

- お名前.comでのドメイン取得はあまりおすすめではない

- おすすめは、スタードメインとエックスドメインらしい

- ドメインの取得は、Whois情報公開代行を同時に使用しなければ、個人情報が公開されている

- Google+ Pages のカスタム URL は、`.com`または、`.org`で登録するのがおすすめ。なぜなら登録時にドメイン部分の省略が確認されている

- 301 リダイレクトは個別記事に対応するが、転送リダイレクトは個別記事に対応しない

- 301 リダイレクトは、サーバーを設置し、設定ファイルを置かなければならない

- したがって、ドメインの運用、移行などは思った以上にお金と時間がかかる

まず、ドメインの取得は、私が運用するようなブログでは、自己満足の粋を出ないということです。特定の文字列(アドレス)が、ブランド意識を高めるという感じだし、ブログを紹介する際、URLが短いとなんかカッコイイというだけです。

また、トップレベルのドメインでは、検索エンジンからの評価は高いわけですが、アクセス数をそもそもあまり気にしていないし、アフィリエイトをやってるわけでもないので、やっぱり、自己満足の粋を出ないというのが私の考えです。

次に、お名前.comでないのなら、[スタードメイン](http://www.star-domain.jp)と[エックスドメイン](http://www.xdomain.ne.jp/)のどちらがおすすめかは、以下の記事を見る限り、エックスドメインがおすすめみたいです。公式サイトを見てみた印象から言うと、私も同意見。

<a href="http://yoshimo.net/domein_syutoku/" target="_blank">ドメイン取得サイトの有名どころ５社の比較と選び方 | セカンドマネーライフ</a>

さて、サービスの是非を判断するには、解約、退会手順を見てみるのが一番良いと今回の経験から学びましたので、エックスドメインの退会手順を見てみることにしました。

<a href="http://www.xdomain.ne.jp/manual/man_order_quit.php" target="_blank">エックスドメイン マニュアル | ドメイン取得＆無料レンタルサーバー Xdomain(エックスドメイン)</a>

簡単に退会できるみたいですね。エックスドメイン、良さそうですね。


