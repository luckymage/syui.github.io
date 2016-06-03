---
layout: post
title: "Bootstrapのメニューバーをマウスオーバーで開く"
date: 2014-06-19
comments: true
categories: [blog]
tags: [octopress, bootstrap]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログのカスタマイズです。Bootstrapでは、モバイルに対応したメニューのため、ドロップダウンメニューがクリックで開くようになっています。それを、マウスオーバーで開くようにします。<!--more--><br clear="all">


できるだけクリックしたくないです。更に、モバイルには簡易なメニューに適しているため、ドロップダウンメニューがそれほど必要には思えません。したがって、モバイルでは、タグリンクへの移動のみ対応することにします。

まず、デフォルトでは、以下の様な HTML になっています。

{% codeblock lang:html デフォルト %}
{% raw %}
      <li class="dropdown">
        <a href="{{ root_url }}/blog/categories/tool/" class="dropdown-toggle" data-toggle="dropdown">Tool <b class="caret"></b></a>

        <ul class="dropdown-menu">
  <li><a href="{{ root_url }}/blog/2014/06/15/airgoogleplus/">airgoogleplus</a></li>
  <li><a href="{{ root_url }}/blog/2014/06/12/airchrome/">airchrome.zsh</a></li>
  <li><a href="{{ root_url }}/blog/2014/06/16/icon/">octopress-share-button</a></li>
        </ul>
      </li>
{% endraw %}
{% endcodeblock %}

ここで、`data-toggle="dropdown"`がクリックでドロップダウンメニューを呼び出す命令になります。

この部分を削除した上で、以下のCSSを書きます。

{% codeblock lang:css %}
ul.nav li.dropdown:hover ul.dropdown-menu{
    display: block;
}
a.menu:after, .dropdown-toggle:after {
    content: none;
}
{% endcodeblock %}

私の場合は、表示崩れを懸念しているため、そして、そもそもモバイルでは、ドロップダウンメニューの必要性を理解していないため、以下のように非表示にしています。

{% codeblock lang:css source/assets/bootstrap/dist/css/bootstrap.min.css %}
@media (max-width:767px){.navbar-nav .open .dropdown-menu{display:none;position:static;float:none;width:auto;margin-top:0;background-color:transparent;border:0;box-shadow:none}
{% endcodeblock %}

簡単に説明すると、`@media { .navbar-nav .open .dropdown-menu }`に`display:none`を設定します。

ここでいう`@media`というのは、最大幅を条件にしたレイアウトの設定のこと。

確認していませんので、現時点では、[Octopress-Theme-octostrap3](https://github.com/kAworu/octostrap3)でのみ有効。


