---
layout: post
title: "ブログの変更点 vol.3"
date: 2014-06-18
comments: true
categories: [blog]
tags: [octopress, github]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログ、カスタマイズする部分も少なくなってきました。<!--more--><br clear="all">


##githubrepo-octopress

`githubrepo-octopress`のタイトルにアイコンフォントを使うことにしました。

デフォルトでは画像が使われているので、綺麗な画面で表示すると、どうにも汚い...。

`watch`とか`fork`とかは今度差し替えるかもしれません。(小さいからいいか)

{% codeblock lang:js ../source/javascripts/jquery.githubRepoWidget.min.js %}
{% raw %}
'<div class="github-box repo">'+'<div class="github-box-title">'+"<h5>"+'<span class="octicon octicon-mark-github" style="font-size: 30px; color:#000; margin-right: 10px;"></span>'+'<a class="owner" href="'+l+'" title="'+l+'">'+a+"</a>"+"/"+'<a class="repo" href="'+c+'" title="'+c+'">'+f+"</a>"+"</h5>"+'<div class="github-stats">'+'<a class="watchers" href="'+c+'/watchers" title="See watchers">?</a>'+'<a class="forks" href="'+c+'/network/members" title="See forkers">?</a>'+"</div>"+"</div>"+'<div class="github-box-content">'+'<p class="description"><span></span> — <a href="'+c+'#readme">Read More</a></p>'+'<p class="link"></p>'+"</div>"+'<div class="github-box-download">'+'<div class="updated"></div>'+'<a class="download" href="'+c+'/zipball/master" title="Get an archive of this repository">Download as zip</a>'+"</div>"+"</div>"
{% endraw %}
{% endcodeblock %}

##GitHub Repos

サイドバーに設置している GitHub Repos の調子がおかしい。

何時頃からだったか忘れました。

上のプラグインを導入してからだったか。多分違います。

新たなリポジトリを`push`してからだったそんな気がします。

現在、READMEを表示しないようにしているのですが、それが影響しているのかもしれません。


<a href="http://blog.fukayatsu.com/2012/11/05/sidebar/" target="_blank">octopressのsidebarにgithub repoとかcoderwallとか表示する - fukayatsu.dev</a>

<a href="http://yoshiori.github.io/blog/2012/07/12/coderwall-badges/" target="_blank">Octopress のサイドバーに Coderwall Badges を表示 - yoshiori.github.io</a>

##URLは大切

今まで適当すぎるネーミングだったのですが、やっぱり大切ですね。

これからは、ある程度の定型文にしていきたいと思います。

普通の記事は、大体、3つの単語から構成するようにしていきたいです。

ちなみに、まとめ記事は1つか2つの単語にします。

リンクを追加している時に、あまりの酷さにショックを受けました。

RSSで配信されている点もあり、変更が困難であることも大きいです。

あと、独自ドメインとってるので、`url`を変更してみました。これは、`{ root_url }`にあたります。

``` css _config.yml
url: http://syui.co
```

まず、`http`を入れないとダメみたいです。また、RSSの`{ site.subscribe_rss }`を見てみたら、`/`が行頭に挿入されておらず、したがって、`url: http:hoge.com/`としてはいけないみたいです。

##Animetion for Firefox

かなり頑張ったのですが、何故か Firefox ではアニメーションが動作しませんでした。

{% codeblock lang:css %}
.hoge {
//animation
background-image: linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
background-image: -weblit-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 90%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);

transition: all 0.3s;
-webkit-transition: all 0.3s;
-moz-transition: all 0.3s;
-ms-transition: all 0.3s;
-o-transition: all 0.3s;

animation: Rotate 0.7s ease-out;
-webkit-animation: Rotate 0.7s ease-out;
-moz-animation: Rotate 0.7s ease-out;
-ms-animation: Rotate 0.7s ease-out;
-o-animation: Rotate 0.7s ease-out;

animation-iteration-count: 1;
-webkit-animation-iteration-count: 1;
-moz-animation-iteration-count: 1;
-ms-animation-iteration-count: 1;
-o-animation-iteration-count: 1;

animation-fill-mode:forwards;
-webkit-animation-fill-mode:forwards;
-moz-animation-fill-mode:forwards;
-ms-animation-fill-mode:forwards;
-o-animation-fill-mode:forwards;
}

@-webkit-keyframes Rotate {
100% {
background-image: linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 10%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%);
}

90% {
background-image: linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 20%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%);
}

80% {
background-image: linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 30%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%);
}

70% {
background-image: linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 40%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%);
}

60% {
background-image: linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 50%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%);
}

50% {
background-image: linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 60%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%);
}

40% {
background-image: linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 70%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%);
}

0% {
background-image: linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%);
background-image: -moz-linear-gradient(to bottom, #f8f8f8 71%,#428bca 100%);
background-image: -ms-linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%);
background-image: -o-linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%);
}
}

@-moz-keyframes Rotate { 100% { background-image: linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 10%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 10%,#428bca 400%); } 90% { background-image: linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 20%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 20%,#428bca 400%); } 80% { background-image: linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 30%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 30%,#428bca 400%); } 70% { background-image: linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 40%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 40%,#428bca 400%); } 60% { background-image: linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 50%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 50%,#428bca 400%); } 50% { background-image: linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 60%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 60%,#428bca 400%); } 40% { background-image: linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 70%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 70%,#428bca 400%); } 0% { background-image: linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%); background-image: -moz-linear-gradient(to bottom, #f8f8f8 71%,#428bca 100%); background-image: -ms-linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%); background-image: -o-linear-gradient(to bottom, #f8f8f8 71%,#428bca 400%); } }
{% endcodeblock %}

ちなみに、 Vim では、範囲指定して`J`を押すと、一行に短縮されます。

よって、各ブラウザに対応したものを書くとき便利です。定形を用意しておいて、`yy`, `J`...。

##Menubar

メニューの各ボックス`li`にリンクを貼りました。画像を使ってた時は調整のため全体にリンクを張ってませんでした。

{% codeblock lang:css %}
li {
  display: block;
  height: 50px; //メニューの縦幅にする
}
{% endcodeblock %}

`display`, `height`、この二つの要素を追加すれば、フォントではなく、ボックスにリンクします。

{% codeblock lang:html %}
{% raw %}
<li><a href="#"></a></li>
{% endraw %}
{% endcodeblock %}


