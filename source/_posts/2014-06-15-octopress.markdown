---
layout: post
title: "ブログの変更点 vol.1"
date: 2014-06-15
comments: true
categories: [blog]
tags: [octopress, github, html, css]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログの変更点を紹介します。<!--more--><br clear="all">

##ポスト位置を調整する

理由:モバイルで表示した時、幅が開きすぎてたので、幅を狭めました。

{% codeblock lang:bash %}
$ grep -R footer . | percol | cut -d : -f 1 | xargs -J % vim %
{% endcodeblock %}

{% codeblock lang:css sass/partials/_blog.sass %}
article>footer {
padding-bottom: 24px;
margin-top: 0em;
}
{% endcodeblock %}

##メニューアイコンを調整する

理由:鳥アイコン、小さかったので、大きくしました。

{% codeblock lang:css sass/partials/_header.scss %}
header[role=banner] {
    /* fix email / rss icon for bootstrap navbar */
    .navbar-default .navbar-nav > li img {
        height: 18px;
    }
    .navbar-default .navbar-nav>li.active img {
    height: 25px;
    max-width: 40px;
    margin: 0px;
  }
}
{% endcodeblock %}

##ポスト画像を綺麗にする

理由:初回の読み込み速度は多少遅くなりますが、モバイルで表示した時、画質が酷かったので、サーバーに置いたものを使うことにしました。

{% codeblock lang:html 変更前 %}
{% raw %}
<img src="http../images/more.png" alt="phoenix-power" align="left" width="100" height="100">要約<!--more--><br clear="all">
{% endraw %}
{% endcodeblock %}

{% codeblock lang:html 変更後 %}
{% raw %}
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">要約<!--more--><br clear="all">
{% endraw %}
{% endcodeblock %}

##ドロップダウンメニューの設置

理由:誰もメニューなんてクリックしないのだろうけど、自分がクリックするので。

http://bootstrap-live-customizer.com/

{% codeblock lang:html %}
{% raw %}
      <li class="dropdown">
        <a href="#" class="dropdown-toggle" data-toggle="dropdown">Dropdown <b class="caret"></b></a>
        <ul class="dropdown-menu">
          <li><a href="#">Action</a></li>
          <li><a href="#">Another action</a></li>
          <li><a href="#">Something else here</a></li>
          <li class="divider"></li>
          <li class="dropdown-header">Dropdown header</li>
          <li><a href="#">Separated link</a></li>
          <li><a href="#">One more separated link</a></li>
        </ul>
      </li>
{% endraw %}
{% endcodeblock %}

##ドロップダウンメニューをモバイルの表示に対応

理由:モバイルではドロップダウンメニューを使うことはないし、対応するのも面倒くさそうなので、非表示にしました。

{% codeblock lang:css source/assets/bootstrap/dist/css/bootstrap.min.css %}
@media (max-width:767px){.navbar-nav .open .dropdown-menu{display:none;position:static;float:none;width:auto;margin-top:0;background-color:transparent;border:0;box-shadow:none}
{% endcodeblock %}

##メニューバーを調整

理由:active要素が非常に厄介で、hover, focues動作が安定しません。したがって、調整してみました。正直良くわからないので、適当に値を変更。

{% codeblock lang:css sass/partials/_header.scss %}
header[role=banner] {
    /* fix email / rss icon for bootstrap navbar */
    .navbar-default .navbar-nav > li img {
        height: 22px;
        margin: 0px;
    }
    .navbar-default .navbar-nav>li.active img {
    height: 22px;
    max-width: none;
    margin: 0px;
  }
}

.navbar {
margin-bottom: 40px;
min-height: 55px;
}

.navbar-default .navbar-nav>.active>a {
height: 53px;
border-bottom: solid 4px #428bca;
}

.navbar-nav>li {
min-height: 53px;
}

.navbar-nav > li:hover {
max-height: 53px;
border-bottom: solid 4px #428bca;
}

.navbar-nav > .active:hover {
max-height: 50px;
border-bottom: solid 4px #428bca;
}
{% endcodeblock %}

##はてなブログパーツのカスタマイズ

理由:幅が一定未満の場合、サイドバーが下に移動するように設定されているため、はてなブログパーツの幅を画面いっぱいに表示するようにした。

{% codeblock lang:css hatena.scss %}
//.hatena-bookmark-count {
//  margin: 0 !important;
//  padding: 0 !important;
//  border: none !important;
//  font-style: normal !important;
//  font-weight: bold !important;
//  text-decoration: underline !important;
//}
//
//.hatena-bookmark-count strong a:link,
//.hatena-bookmark-count strong a:hover,
//.hatena-bookmark-count strong a:visited {
//  color: #ff0000 !important;
//  background: #FFCCCC !important;
//}
//
//.hatena-bookmark-count em a:link,
//.hatena-bookmark-count em a:hover,
//.hatena-bookmark-count em a:visited {
//  color: #FF6666 !important;
//  background: #FFF0F0 !important;
//}

.hatena-bookmark-widget {
padding: 10px !important;
border:  solid 1px #ddd !important;
width: 100% !important;
margin-bottom: 20px;
}

.hatena-bookmark-widget ul li {
border-bottom:  solid 1px #ddd !important;
}

.hatena-bookmark-widget-body ul {
border: none !important;
background-color: transparent !important;
padding: 10px 10px 0px 10px;
}

.hatena-bookmark-widget-title {
display:none;
}

.hatena-bookmark-widget-footer {
display:none;
}

.hatena-bookmark-widget ul li > a{
color: #428bca !important;
}

.hatena-bookmark-widget-footer {
background: none !important;
border: none !important;
}

.hatena-bookmark-widget-footer a {
background: none !important;
border: none !important;
}
{% endcodeblock %}

