---
layout: post
title: "Webの高速化を試してみた"
date: 2014-06-30
comments: true
categories: [blog]
tags: [middleman, github, web, speed, css]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Web高速化で一応、AAランクを目指してみました。<!--more--><br clear="all">

<a href="http://syui.github.io/middleman/" target="_blank">http://syui.github.io/middleman/</a>

テーマをイチから作るようなことをしてみました。ただし、シンプルなテンプレートをだいぶ参考にしていますが。

Webの高速化は、以下のサイトを見て、ダメな部分を削っていけば自然に`AA`ランクが取れます。

<a href="http://gtmetrix.com/" target="_blank">http://gtmetrix.com/</a>



ただし、シンプルなテーマを選ぶか、イチから作るかでしか早期に達成するのは難しそうです。

今回は、以前から一度、シンプルなテーマを作ってみたかったこともあり、一石二鳥でしたが、分からない所もたくさんありました。

まず、 Middleman で一般的に使われている変数がまとまっていないので、ソースを見ていくしかなかったです。

また、 PATH と HOVER が難しかったです。

例えば、個別記事全体にリンクを貼るにも、プロジェクトページを使っていると、`/(root)`の記述が使えないため、 PATH 設定が困難を極めるなどしました。しかも、これは、プレビューで確認する事ができない。(推測はできますが

なんとか対応した形が以下の通りです。

{% codeblock lang:html source/index.html.erb%}
{% raw %}
<% page_articles.each_with_index do |article, i| %>
<% if i > 0 %>
    <div class="articles" onclick="location.href=&#34;.<%= article.url %>&#34;;" style="cursor: pointer;">
    </div>
<% end %>
    <div class="articles" onclick="location.href=&#34;.<%= article.url %>&#34;;" style="cursor: pointer;">
        <%= partial '/blog/article', :locals => {:article => article, :digest => true} %>
    </div>
<% end %>
{% endraw %}
{% endcodeblock %}

しかし、タグページだと、何故か URL が二重になるため`.`が使えませんでした。よって、`site_url`を使います。

{% codeblock lang:html source/layouts/tag.html.erb %}
{% raw %}
<ul class="breadcrumbs">
    <li><a href="<%= site_url %>"><span class="icon-home"></span></a></li>
  <li class="current"><a href="<%= tag_path tagname %>"><%= tagname %></a></li>
</ul>

  <% page_articles.each_with_index do |article, i| %>
    <% if i > 0 %>
    <div class="articles" onclick="location.href=&#34;<%= site_url %><%= article.url %>&#34;;" style="cursor: pointer;">
    </div>
    <% end %>
    <div class="articles" onclick="location.href=&#34;<%= site_url %><%= article.url %>&#34;;" style="cursor: pointer;">
        <%= partial '/blog/article', :locals => {:article => article, :digest => true} %>
    </div>
  <% end %>
{% endraw %}
{% endcodeblock %}

