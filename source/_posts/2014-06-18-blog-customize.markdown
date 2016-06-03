---
layout: post
title: "ブログの変更点 vol.4"
date: 2014-06-18
comments: true
categories: [blog]
tags: [octopress, github, bootstrap]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログのカスタマイズ履歴です。そのうち、まとめます。<!--more--><br clear="all">

##Bootstrap Menubar

この辺で、[Bootstrap](http://getbootstrap.com/)メニューの動作をまとめておきます。

ブログ内で現在地をホバーして教えてくれるのが特徴的なメニューバーですが、カスタマイズが割と面倒です。

自分のブログでは、以下の様な要素が混在しています。

{% codeblock lang:css %}
//現在選択されているボックスのリンク文字
.navbar-default .navbar-nav > .active > a:hover {
color: #fff;

  //Web Font
  .icon-twitter:hover {
  color: #000;
  }
}

//選択されていないボックス内のリンク文字
.navbar-default .navbar-nav > li > a:hover {
color: #428bca;
.icon-twitter:hover{
color: #428bca;
}
}

//選択されているボックス内のリンク文字
.navbar-default .navbar-nav > .active > a {
color: #ccc
}

//選択されていないボックス内のリンク文字
.navbar-default .navbar-nav > a {
color: #999
}

//選択されているボックス
.navbar-nav > .active:hover {
opacity: 0.5;
}

//選択されていないボックス
.navbar-nav:hover {
opacity: 0.5;
}

//ドロップダウンメニュー
.dropdown-menu {
background-color: #fff;
}

//ドロップダウンメニュー内のリンク文字
.dropdown-menu>li>a {
background-color: #000;
}

//ドロップダウンメニュー内のリンクを選択時
.navbar-default .navbar-nav>.open>a, .navbar-default .navbar-nav>.open>a:hover, .navbar-default .navbar-nav>.open>a:focus {
color: #ddd;
}

//ドロップダウンメニューの全体
li.dropdown.open {
background-color: #eee;
}
{% endcodeblock %}

更に厄介なのが、モバイルでの表示です。こちらは対応するにも結構複雑で、調整に時間がかかりました。調整と言っても、何度かコードをいじっていれば分かってくるのですが、これはもうある程度の時間をかけて触ってみないと分からないと思います。

ちなみに、下記は Web Font を利用した場合のモバイルに対応したコードの一例です。

{% codeblock lang:html source/_includes/custom/navigation.html %}
{% raw %}
                <li>
                    <a class="subscribe-rss" href="https://plus.google.com/+SyuiCom" target="_blank" title="subscribe via Google+" rel="publisher">
                      <span class="visible-xs">Google+</span>
                      <span class="hidden-xs"><span class="icon-googleplus"></span></span>
                    </a>
                </li>
{% endraw %}
{% endcodeblock %}

簡単には、`hidden-xs`という`display:none`の要素を用意し、 Web Font は、そこに入れます。

`visible-xs`はその逆で、一定の幅がないと表示されます。

正直、エフェクトを加えれば加えるほど、モバイルの表示がダメになっていったので、それを直すのにかなり時間がかかりました。

メニューなんて誰もクリックしないのに、なんでこんなこだわってるんだろ...。


##Article Post

記事を選択した時、全体をエフェクトさせ、選択した記事をはっきりさせるようにしました。

`shadow-box`を使っているので、[shadow-boxジェネレーター](http://www.bad-company.jp/demos/box-shadow/)が非常に役立ちました。

{% codeblock lang:css %}
article.post:hover {
background-color: #DBDBFF;
opacity: 0.9;
-webkit-transition: 0.3s ease-in-out;
-moz-transition: 0.3s ease-in-out;
-ms-transition: 0.3s ease-in-out;
-o-transition: 0.3s ease-in-out;
transition: 0.3s ease-in-out;
/* border-radius */
border-radius:1px;
-webkit-border-radius:1px;
-moz-border-radius:1px;

/* box-shadow */
box-shadow:rgb(97, 165, 255) 0px 0px 3px 0px inset;
-webkit-box-shadow:rgb(97, 165, 255) 0px 0px 3px 0px inset;
-moz-box-shadow:rgb(97, 165, 255) 0px 0px 3px 0px inset;
}
{% endcodeblock %}

今までのボンヤリしていた感じが解消できて良いです。

ついでに画像の縁も光らせることにしました。今までは、空白の丸枠でした。

{% codeblock lang:css %}
img:not(.no-border) {
/* border-radius */
border-radius:1px;
-webkit-border-radius:1px;
-moz-border-radius:1px;

/* box-shadow */
box-shadow:rgba(49, 127, 230, 0.54902) 0px 0px 7px 4px;
-webkit-box-shadow:rgba(49, 127, 230, 0.54902) 0px 0px 7px 4px;
-moz-box-shadow:rgba(49, 127, 230, 0.54902) 0px 0px 7px 4px;
}
{% endcodeblock %}

でも多分、光らせないほうがカッコイイんだろうなと。

私は今のほうが気に入ってますが、あまりカスタマイズし過ぎると、よりダサくなるのは目に見えてます。


