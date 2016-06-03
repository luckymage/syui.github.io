---
layout: post
title: "新しいブログの作り方"
date: 2015-01-08
comments: true
categories: blog
tags: [middleman, octopress]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopressのビルドが遅すぎて、手軽にポストできなくなったので、移行を考えています。<!--more--><br clear="all">

##メモブログ

なので、様子見の観点からも、適当なメモブログからはじめました。

このテンプレートというか、ブログは、今まで使い道に困っていて、何かまとめ的な物を作ろうとしたこともありましたが、結局続けられなくて挫折。したがって、今回も、いつまで続けられるか分かりませんが、一応。

http://syui.github.io/middleman/

はじめに言ったように、このブログは、「適当」が基本。気になったリンクとかを張り付けていくのが主になりそうと思っています。また、テンプレートのテストというか、改良というか、そういったものも兼ねての運用になりそうです。

また、話は変わりますが、私がアニメ感想とか読んでいる関係で、私もアニメの感想とか書いてみたのですが、到底続けられませんでした。アニメ系のブログは、毎日のように更新してるブログとか多いのですが、すごすぎる...。

##おすすめブログ

ブログは、[Middleman](https://middlemanapp.com/)か、[Hugo](http://gohugo.io/)で生成するのがオススメっぽいです。

コードは、[GitHub Pages](https://pages.github.com/)にポストするのが定番。

HTMLは、[ERB](https://rubygems.org/gems/html2slim)や[Slim](https://github.com/slim-template/slim/blob/master/README.jp.md)で書く感じ。CSSは、[SCSS](http://sass-lang.com/)です。

記事は、[Markdown](http://kramdown.gettalong.org/)で書くわけですが、パーサーには、[Kramdown](http://kramdown.gettalong.org/)とかかなあ。正直、この辺りどれが良いのかはイマイチ分かってません。

カスタマイズは、[Bootstrap](http://getbootstrap.com/), [Bower](http://bower.io/)などを使うことがあるかもしれません。

アイコンフォントは、[Font Awesome](http://fortawesome.github.io/Font-Awesome/), [IcoMoon](https://icomoon.io/)などを使ってます。

画像アイコンは、[ICONFINDER](https://www.iconfinder.com/)が便利そう。

このブログは、Octopressですが、[Octopress](http://octopress.org/)は、ないです。ビルドが遅すぎですし、メンテナンスされていません。

ちなみに、[Xdomein](http://www.xdomain.ne.jp/)でドメインを取得していますが、正直、GitHub Pagesで運用しているので、リダイレクトするだけのドメイン設定に魅力は感じませんでした。私なら、アクセスする度に飛ばされるのは、あまり嬉しくはないので、使うの止めました。

今後も、自分でサーバー運用しない限り、多分、使うことはないだろうと思います。

##デザインについて

デザインとかもあまり得意ではなく、このブログを見てもらっても分かりますが、一言で言うと、ダサい。

しかし、ここは、もう手遅れなので、デザインを変えるなら、新しいブログでやります。継ぎ接ぎだらけのコードを直す気力が出ません。

##技術力について

私の技術力, パソコン力はゼロです。

私は、HTML, CSSもよく分かってないのに、ブログをやってる人という感じなのでしょうね。

ただし、使用するツールなどで必要になれば、ドキュメントを読んだり、検索したりするくらいはやりますが、実は、その手の本を読んだことも、勉強したこともなかったりします。

今までの私のやり方としては、一言で言うと、下書き。

下書きをざっと書いて、動くようにしてから、コードを綺麗にしていく作業を予定しているのだけど、結局のところ下書きでやめてしまってるという感じ。

なので、このブログも見ての通り、あまり出来が良くなかったりします。

今度があればですが、今度こそ、最低限、読み直しをしたいです。ただ、HTML, CSSを直接読む気力はやっぱり出てこなさそうなので、それ以外で書くつもりです。

